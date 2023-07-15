# 玩家


## Player

### Player:drawCardActions()
玩家抽牌的行动。

如果牌堆中没有剩余的卡片，那么玩家会进入疲劳状态，并且受到相当于疲劳值的伤害，然后返回一个包含受伤事件的事件列表。如果牌堆中还有卡片，那么会抽取牌堆中的最后一张卡，然后返回调用`receiveCardAction(card)`方法的结果。

#### 参数类型

N/A

#### 返回值

[[Event](./event.md#event)]

### Player:receiveCardActions(card)
玩家接收卡片的行动。

这个方法接受一个类型为`Card`的参数。它会首先创建一个包含`ReceiveCard`事件和该卡片的事件，并添加到一个事件列表中。然后，如果手牌的数量少于最大手牌数量，那么会将卡片添加到手牌中。否则，会创建一个包含`DiscardCard`事件和该卡片的事件，添加到事件列表中。最后返回事件列表。


#### 参数类型

card: [Card](./card.md#card)

#### 返回值

[[Event](./event.md#event)]