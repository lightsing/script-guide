# Entity

## 方法

### Entity:isDead()
检查一个实体是否已经死亡。如果实体的血量加上血量修正值小于等于0，那么该实体被视为已经死亡。

### Entity:hasEffect(effect)
检查一个实体是否拥有某种效果。如果该实体当前的效果中包含给定的效果，那么返回 `true`；否则，返回 `false`。

#### 参数类型

effect: [EffectType](../effect/effect_type.md)

#### 返回值

boolean

### Entity:removeEffectAction(effect)
移除实体身上的一个效果。如果实体当前的效果中不包含给定的效果，那么会报错。如果成功移除效果，那么返回一个包含事件类型（RemoveEffect）和被移除效果的事件对象。

#### 参数类型

effect: [EffectType](../effect/effect_type.md)

#### 返回值

[`Event`](./event.md#event)

### Entity:giveEffectAction(effect, effect_attrs)
给实体添加一个效果。该方法需要两个参数：效果类型和效果属性。如果成功添加效果，那么返回一个包含事件类型（GiveEffect）和添加的效果的事件对象。

#### 参数类型

effect: [EffectType](../effect/effect_type.md)

effect_attrs: [EffectAttrs](../effect/effect_attrs.md)

#### 返回值

[`Event`](./event.md#event)

### Entity:takeDamageAction(amount, source)
实体受到伤害。该方法需要两个参数：伤害数值和伤害来源。如果实体有防护盾效果，那么会移除防护盾，并返回一个移除效果的事件对象。如果没有防护盾，那么会对实体造成伤害。如果伤害后实体死亡，那么返回一个包含事件类型（Death）和实体的事件对象。如果实体未死，那么返回一个包含事件类型（TakeDamage）、实体、伤害数值和伤害来源的事件对象。

#### 参数类型

amount: integer

source: [Entity](#entity)

#### 返回值

[`Event`](./event.md#event)