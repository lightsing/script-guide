# CardTargetType

## 枚举值

### CardTargetType.SelfMinion

卡目标为己方随从

### CardTargetType.SelfHero

卡目标为己方玩家

### CardTargetType.Self

卡目标为己方实体（玩家&随从）

### CardTargetType.EnemyMinion

卡目标为敌方随从

### CardTargetType.EnemyHero

卡目标为敌方玩家

### CardTargetType.Enemy

卡目标为敌方实体（玩家&随从）

### CardTargetType.AnyMinion

卡目标为任意随从

### CardTargetType.AnyHero

卡目标为任意玩家

### CardTargetType.Any

卡目标为任意实体（玩家&随从）

### CardTargetType.None

该卡没有目标

## 方法

### CardTargetType.exist(ctx, target_type)

检查卡的目标类型是否存在，当类型为 `None` 是，也返回 `true`。

#### 参数类型

- `ctx`: [`GameContext`](../game.md#gamecontext)
- `target_type`: [`CardTargetType`](#cardtargettype)

#### 返回值

boolean

### CardTargetType.isValidTarget(ctx, target_type, target)

检查给定的目标是否满足当前的目标类型

#### 参数类型

- `ctx`: [`GameContext`](../game.md#gamecontext)
- `target_type`: [`CardTargetType`](#cardtargettype)
- `target`: UUid

#### 返回值

boolean