# golang-concurrency-tricks

## Channel Hints

1. Do not close a channel from a receiver goroutine. Closing the channel from a receiver could make future sender goroutines to panic.

2. If a channel has multiple senders, do not close the channel from a sender goroutine. Closing the channel from a sender could make future sender goroutine to panic.

3. It is not required to close an unused channel. If no goroutine is left referencing the channel, it will be gargabe collected.

> Note that it is only necessary to close a channel if the receiver is looking for a close.  Closing the channel is a control signal on the channel indicating that no more data follows.

https://groups.google.com/forum/#!msg/golang-nuts/pZwdYRGxCIk/qpbHxRRPJdUJ

4. Do not close a channel more than once because it would panic.

5. Channels work better enclosed in a select.

> If you are ever using a channel outside of a select in production code, you are probably doing it wrong.  

https://groups.google.com/d/msg/golang-nuts/LM648yrPpck/j5eHsPc2AwAJ

6. If you need bidirectional communication between two goroutines, consider using two unidirectional channels. Then any side will be able to use the close idiom to signal termination.

7. Beware: one sender goroutine risks blocking indefinitely when writing on a channel if there is no receiver left.

* Repository: git clone https://github.com/udhos/golang-concurrency-tricks.git
* Web URL: http://udhos.github.io/golang-concurrency-tricks
