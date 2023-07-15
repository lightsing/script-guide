# Card

### Card:useActions(ctx, [target])

当前玩家使用本卡，要求玩家手中必须有这张卡，并且 `CardPrototype:canUse` 为 `true`。

#### 参数类型

- `ctx`: [`GameContext`](../game.md#gamecontext)
- `target`: 可选参数，ID。当卡牌的 [`target_type`](./card_target_type.md) 为以下的值时，无需提供 `target` 参数：
    - [`CardTargetType.None`](./card_target_type.md#cardtargettypenone)
    - [`CardTargetType.SelfHero`](./card_target_type.md#cardtargettypeselfhero)
    - [`CardTargetType.EnemyHero`](./card_target_type.md#cardtargettypeenemyhero)


#### 返回值

[[`Event`](../event/event.md)]