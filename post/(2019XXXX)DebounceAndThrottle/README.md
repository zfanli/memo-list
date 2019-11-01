# EP1 JavaScript 中的防抖和节流到底是什么？

使用 JavaScript 进行前端开发，就绕不开防抖和节流的话题。理解和使用它们可以有效的改善前端性能和提升用户体验。

先做一个简单的定义，然后我们再来进行详细的示例解释。

**防抖**

防抖指的是在一连串触发的事件中，只需要对第一次或者最后一次进行执行的情况，对其他的事件进行压制。理解成一个 CD 时间就好，但是这个 CD 区分前摇和后摇：前摇的时候，需要等待指定的时间结束才会执行动作，期间任何重复的调用将会刷新计时；后摇则先执行动作，此后一段时间的重复调用会被抑止，直到时间过去才可以重新调用。

**节流**

节流是指在高频发事件中，间隔一定时间执行一次操作，对其他同时间段发生的事件进行抑止。节流的概念类似上面说到的 CD 后摇的防抖，也叫立即执行防抖，唯一的区别就是第一次执行的时机：节流会在指定时间内先进行抑止，抑止结束之后再执行；但是立即执行防抖会马上执行然后再抑止。

解释太抽象，看不懂？没关系，接下来我们详细示例解释。我们先来看看防抖。

### 什么是防抖（debounce）？

看看下面这张图，搜索框使用了防抖之后，只有在用户停止输入后才会真正访问服务器进行搜索，并提示相关的可选项。

![debounceSample](./debounceSample.gif)

> R：这是 wolframalpha.com 的搜索框。不得不说为了用户体验，大多数情况网站会使用节流而不是防抖来处理搜索。

之前说到防抖的作用是对于一连串事件，只执行一次实际操作并且抑止其他事件。这里可以看出来，只有当用户输入完成之后，搜索框才开始和服务器进行交互执行真正的搜索操作，而非每次按键都触发一次搜索。这样做避免了过多无效的服务器请求，也减少了浏览器的负担，反映到用户体验上就是更流畅的 UI 和更精准的结果。

或许你还是不明白为什么要这样做，我们来还原一下没有防抖时的情况。