
算法看起来很简单：
1. 将 `onmouseover/out` 处理器放在元素上。也可以在这里使用 `onmouseenter/leave`，但它们并不常用，而且如果我们使用委托，它们就会无效。
2. 当鼠标光标进入元素时，开始测量 `mousemove` 上的速度。
3. 如果速度慢，则运行 `over`。
4. 之后如果离开了元素，而且 `over` 也被执行了，则运行 `out`。

问题是：“如何测量速度？”

第一个想法是：每 `100ms` 运行一次我们的函数，并测量前一个坐标和新坐标之间的距离。如果它很小，那么速度就很小。

不幸的是，在 JavaScript 中无法获取“当前鼠标坐标”。没有像 `getCurrentMouseCoordinates()` 这样的函数。

获取坐标的唯一方法是监听鼠标事件，就像 `mousemove`。

因此我们可以在 `mousemove` 上设置一个处理器来跟踪坐标并记住它们。然后我们可以比较它们，每 `100ms` 比较一次。

P.S. 请注意：解决方案测试使用 `dispatchEvent` 来查看工具提示是否正确。
