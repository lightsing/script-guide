# 事件

## 事件类型 EventType

你需要通过全局常量来访问这些事件类型：

- 实体死亡：`EventType.Death`
- 玩家丢弃卡牌（包括使用）：`EventType.DiscardCard`
- 实体获得效果：`EventType.GiveEffect`
- 当前玩家变更：`EventType.PlayerChanged`
- 新实体生成：`EventType.Spawn`
- 玩家获得新卡牌：`EventType.ReceiveCard`
- 实体效果移除：`EventType.RemoveEffect`
- 实体受到伤害：`EventType.TakeDamage`

## 创建事件

通过 `Event:new` 来创建事件，不同的事件有不同的值需要填入，请务必小心。

以下是一个例子：

```lua
Event:new {
    event_type = EventType.Death,
    id = "4d4c9983-20de-43ff-8a39-da815583d6d9"
}
```

## 事件值

### EventType.Death
### EventType.DiscardCard
### EventType.GiveEffect
### EventType.PlayerChanged
### EventType.Spawn
### EventType.ReceiveCard
### EventType.RemoveEffect
### EventType.TakeDamage