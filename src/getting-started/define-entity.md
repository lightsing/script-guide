# 定义实体原型 EntityPrototype

在定义一个实体原型时，你必须包括以下信息：
- 唯一ID：id（应为唯一的 UUID 字符串）
- 显示名称：name
- 描述文本：description
- 阵营：fraction（请参照 [Fraction](../api/fraction.md) 的文档说明）
- 血量：hp
- 攻击力：attack

实体原型有一些默认值，如果这些默认值符合你的期待，你无需特别提供：
- 冲锋：charged；默认值为 `false`
- 嘲讽：taunt；默认值为 `false`
- 圣盾：shield；默认值为 `false`
- 衍生卡牌定义：is_card；默认值为 `true`

如果实体原型是衍生卡牌，你还需要提供以下信息：
- 费用：cost

## 定义无监听器的实体原型

许多随从，特别是中立随从，没有特殊能力，也不会对事件做出响应。

下面是一个例子：
```lua
local definition = EntityPrototype:new {
    id = "f463db29-6a1b-4b3d-9af4-a6540ec63c11",
    name = "1/1",
    description = "1/1冲锋",
    fraction = Fraction.Neutral,
    hp = 1,
    attack = 1,
    charged = true,
    cost = 1,
}

return definition
```

## 定义非衍生卡牌的实体原型

有些随从不以卡牌形式存在，但可能会由于其他效果被召唤到场上。在这种情况下，你需要明确设置 `is_card = false`。

下面是一个例子：
```lua
local definition = EntityPrototype:new {
    id = "4cdb4a11-e631-44cb-bd11-d55a9df673d7",
    name = "1/1",
    description = "1/1",
    fraction = Fraction.Neutral,
    hp = 1,
    attack = 1,
    is_card = false,
}

return definition
```

## 定义有监听器的实体原型

首先，你需要额外添加一个 `listener` 值，该值告诉引擎这个实体会监听哪些事件。我们以亡语为例进行解释。

首先，按照前面的方式定义实体原型：
```lua
local definition = EntityPrototype:new {
    id = "f96acaf7-537b-4222-b282-2f7382ac4a46",
    name = "2/1",
    description = "2/1亡语：抽一张牌",
    fraction = Fraction.Neutral,
    hp = 2,
    attack = 1,
    cost = 2,
}
```

然后，我们需要定义事件发生时的行为：
```lua
local on_death = function(ctx, event, entity)
    -- 在这里定义亡语的行为
end
```

可以看到，我们定义了一个函数，它接收三个参数，分别是游戏上下文 `ctx`、当前事件 `event` 以及接收该事件的实体 `entity`。

通过 `ctx`，我们可以操作游戏内部的状态，而 `event` 告诉我们具体发生了什么事件。
由于原型定义和实体是分开的，所以第三个参数 `entity` 会传入实际由该原型创建的实体。

在这个例子中，我们首先需要检查是否是由自身产生的事件：
```lua
if event.id ~= entity.id then
    return
end
```

接下来，我们执行亡语的行为：
```lua
local player = ctx.getEntityOwner(entity) -- 找到实体的所有者
player.drawCardActions() -- 执行抽卡
```

但这还不够，因为抽卡可能会引发事件：
- 当成功抽卡时，会触发 `ReceiveCard` 事件
- 当手牌已满时，会触发 `ReceiveCard` 和 `DiscardCard` 事件
- 当没有牌可抽时，会因疲劳受到伤害：
  - 如果玩家没有圣盾，会触发 `TakeDamage` 事件
  - 如果玩家有圣盾，会触发 `RemoveEffect` 事件

虽然看起来很复杂，但你不必过于担心，你只需将引发的事件直接返回给引擎即可：
```lua
local player = ctx.getEntityOwner(entity) -- 找到实体的所有者
return player.drawCardActions() -- 执行抽卡
```

你可能会好奇为什么这里的 `drawCard` 没有参数指定抽几张卡。
原因是，多次抽卡的行为可能会被其他实体打断。

例如，有一个实体的定义是“每当玩家抽一张卡，获得+1/+1”，显然这个“+1/+1”的效果应在每张卡到手后立即发生。

那么，如何编写这种能力呢？以下是一个抽四张卡的例子：
```lua
local player = ctx.getEntityOwner(entity) -- 找到实体的所有者
for _ = 1, 4 do
  coroutine.yield(player.drawCardActions()) -- 执行抽卡
end 
```

这里的 `coroutine.yield` 会将事件返回给引擎，并暂时放弃执行权，以便引擎可以让其他实体进行操作。

之后我们需要设置 `listener`，将亡语的监听器添加到定义上：
```lua
definition.listener[EventType.Death] = on_death
```

全部的内容整合在一起是这样的：
```lua
local definition = EntityPrototype:new {
    id = "f96acaf7-537b-4222-b282-2f7382ac4a46",
    name = "2/1",
    description = "2/1亡语：抽四张牌",
    fraction = Fraction.Neutral,
    hp = 2,
    attack = 1,
    cost = 2,
}

local on_death = function(ctx, event, entity)
  local player = ctx.getEntityOwner(entity) -- 找到实体所属的玩家
  for _ = 1, 4 do
    coroutine.yield(player.drawCardActions()) -- 执行抽卡
  end
end

definition.listener[EventType.Death] = on_death

return definition
```

就是这样，有关如何操作游戏状态的更多内容，请参考 API 章节。