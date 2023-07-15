# 定义卡牌原型 CardPrototype

除去随从实体自动衍生出的卡牌外，你可能还想定义魔法卡。

## 魔法卡

在定义魔法卡原型时，你必须包括以下信息：
- 唯一ID：id（应为唯一的 UUID 字符串）
- 显示名称：name
- 描述文本：description
- 阵营：fraction（请参照 [Fraction](../api/fraction.md) 的文档说明）
- 费用：cost
- 目标类型：target_type（请参照 [CardTargetType](../api/card/card_target_type.md) 的文档说明）

类似于前一节中定义事件监听器的方式，你也需要将卡牌的效果写成一个函数。

以抽四张牌为例，首先定义原型：
```lua
local card = CardPrototype:new {
    id = "707e7257-4e4a-49f0-a0d9-5150b1c63a4a",
    name = "疾跑",
    description = "抽4张牌",
    fraction = Fraction.Apex,
    cost = 6,
    target_type = CardTargetType.None
}
```

在此基础上添加一个函数，其第一个参数 `ctx` 接收游戏上下文，第二个参数 `player` 接收使用卡牌的玩家，第三个参数 `target` 接收卡牌目标实体 ID 。在本例中，我们不需要使用到第三个参数：
```lua
local use = function(ctx, player, _target)
    for _ = 1, 4 do
        coroutine.yield(player.drawCardActions()) -- 执行抽卡
    end 
end
```

然后将该函数添加到卡牌定义上：
```lua
card.use = use
```

结合起来是这样：
```lua
local card = CardPrototype:new {
    id = "707e7257-4e4a-49f0-a0d9-5150b1c63a4a",
    name = "疾跑",
    description = "抽4张牌",
    fraction = Fraction.Apex,
    cost = 6,
    target_type = CardTargetType.None
}

local use = function(ctx, player, _target)
    for _ = 1, 4 do
        coroutine.yield(player.drawCardActions()) -- 执行抽卡
    end 
end
card.use = use

return card
```