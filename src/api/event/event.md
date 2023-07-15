# Event

事件是只读的，尝试修改其中的内容会导致 `RuntimeError`。

事件的类型存储在 `event_type` 键中。

### 事件值

根据事件类型的不同，其会包含不同的键值：

#### EventType.Death

- `entity`: 死亡的 [`Entity`](../entity/entity.md) 的视图
- `source`: 伤害来源的 [`Entity`](../entity/entity.md) 的视图


#### EventType.DiscardCard

- `player`: 丢弃卡牌的 [`Player`](./player.md#player) 的视图
- `card`: 被丢弃的 [`Card`](../card/card.md) 的视图


#### EventType.GiveEffect

- `entity`: 被给与效果的 [`Entity`](../entity/entity.md) 的视图
- `effect`: 被给与的 [`EffectType`](../effect/effect_type.md)
- `effect_attrs`: 被给予的效果的属性值 [`EffectAttrs`](../effect/effect_attrs.md) 的视图

#### EventType.PlayerChanged
#### EventType.Spawn
#### EventType.ReceiveCard

- `player`: 收到卡牌的 [`Player`](./player.md#player) 的视图
- `card`: 收到的 [`Card`](../card/card.md) 的视图

#### EventType.RemoveEffect

- `entity`: 被移除效果的 [`Entity`](../entity/entity.md) 的视图
- `effect`: 被移除的 [`EffectType`](../effect/effect_type.md)

#### EventType.TakeDamage

- `entity`: 死亡的 [`Entity`](../entity/entity.md) 的视图
- `source`: 伤害来源的 [`Entity`](../entity/entity.md) 的视图
- `amount`: 受到的伤害点数 `integer`