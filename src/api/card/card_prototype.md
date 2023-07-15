# CardPrototype

### CardPrototype:canUse(ctx)

检查当前玩家是否可以使用这张卡。

#### 参数类型

- `ctx`: [`GameContext`](../game.md#gamecontext)

#### 返回值

boolean

### CardPrototype:isValidTarget(ctx, target)

`CardTargetType.isValidTarget(ctx, card.target_type, target)` 的简便写法。

参见 [`CardTargetType.isValidTarget`](./card_target_type.md#cardtargettypeisvalidtargetctx-target_type-target)