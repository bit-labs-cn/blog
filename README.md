### Exchange 交换机
1. 其实就是数据分发规则，根据某个规则把数据发送到指定的队列

### Queue 队列
+ 就是队列


### RoutingKey 路由键
+ 转发规则
> 假设有一个 direct 的交换机，有一个名为 user_register 的路由键，一个 user_register 的队列
> 那么这个交换机就会把消息通过 user_register 路由键的匹配，发送到 user_register 队列

### Bind 绑定
+ 将队列与路由键绑定
> 假设有一个 direct 交换机  有一个名为 user_register 的路由键，一个 user_reg 的队列  
> bind (user_register, user_reg)  
> 这样交换机就会把 user_register 路由键上的数据转发到  user_reg 这个队列

### 一次只消费一条数据
`$Channel.Qos(1, 0, true)`


### 结论
1. 如果批量消费数据，假设消费 10 条数据，如果这 10 条一条都没有进行 ack，那么该消费者不能再获取到新的消息
1. 如果批量消费数据，假设消费 10 条数据，如果 ack 了一条，则该消费者会立刻补一条。
1. 创建队列不指定交换机，默认绑定到 `amqp default`

## 交换机类型
```


RabbitMQ是一个消息代理，支持多种类型的交换机用于路由消息到队列。下面是RabbitMQ支持的交换机类型及其特点：

1. Direct Exchange（直接交换机）
   直接交换机是最简单的一种交换机类型，它根据消息的 routing key 将消息路由到与之绑定的队列。如果一个队列和交换机都绑定了同一个 routing key，那么消息会被路由到这个队列中。
   
2. Fanout Exchange（扇型交换机）
   扇型交换机会将收到的所有消息路由到绑定到它上面的所有队列中。无论是哪个队列，都会收到相同的消息。

3. Topic Exchange（主题交换机）
   主题交换机与直接交换机类似，但是它支持使用通配符将消息路由到多个队列中。它使用带有通配符的 routing key 匹配消息，并将消息路由到所有匹配的队列中。例如，"*.red.*" 匹配任何 routing key 由三个单词组成，且第二个单词是 "red" 的消息。

4. Headers Exchange（头交换机）
   头交换机使用消息的 header 信息来进行路由，而不是使用 routing key。在绑定队列时，可以指定一组 key-value 键值对，如果消息的 header 信息中也包含了相同的 key-value，则该消息会被路由到该队列中。

以上是 RabbitMQ 支持的交换机类型及其特点。选择适当的交换机类型可以帮助开发人员更好地处理消息，并提高消息传递的效率。
```
