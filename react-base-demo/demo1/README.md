# React tutorial
跟随react教程开发的 tic-tac-toe 游戏。

## Lifting State Up(状态提升)
当需要收集多个子组件中的数据，或者两个子组件之间需要相互通信时，需将它们共享的状态提升到它们的父组件中。父组件可通过`props`将状态传递给子组件，这样可以保持父子组件之间数据的同步。（若在父组件之间修改了`state`中的某个值，那么通过`props`传递给的子组件中的该值也会同时更新）。参见`demo1`中的`squares[i]`。

## 不可变性在react中的重要性
### 简化复杂功能
例如`demo1`中的时间旅行，以及撤销回退恢复等功能会变得简单些。

### 更易跟踪数据变化
跟踪可变对象的数据变化是很困难的，因为可变对象是直接修改的。若要判断出（跟踪）可变对象发生了变化，需要将可变对象与之前（未改动时）的副本进行对比，这种操作会遍历整个对象树。

跟踪不可变对象的数据变化就相对容易了，如果对象变成了一个新对象，那么就可以说这个对象发生变化了。

### 决定React何时重加载
不可变性主要的好处它可以帮助我们在React中创建纯组件。我们可以很轻松的确定不可变数据是否发生了改变，从而确定何时对组件进行重新渲染。

[点这里查看](https://reactjs.org/docs/optimizing-performance.html#examples)如何创建一个纯组件

## Function Components(函数式组件)
函数组件是创建组件的一种简单方式，只包含一个`return`函数，并且不包含`state`。这种方式不用定义一个继承自`React.Component`的类，而是定义一个函数，这个函数接收`props`为参数，然后使用`return`返回需要渲染的元素。相比类，函数组件写起来要简单一些，很多组件都可以用这种方式创建。参见`demo1`中的`Square`组件。

## keys
当我们渲染一组列表时，`React`会存储已渲染列表元素的一些信息。当我们更新列表的时候，`React`需要判断更新的内容。我们可以对列表进行增加、删除、重排序和更新列表元素的内容。当我们对列表做这些操作的时候，`React`通过对比列表元素的`key`去决定对列表中的元素进行创建、销毁或者重新渲染等操作。

`key`是React中特殊的保留属性（还有一个是`ref`, 拥有更高级的特性），当React元素被创建出来的时候，React会提取出`key`属性，然后将Key直接存储在返回的元素中。虽然看起来`key`像是`props`的属性，但是不能通过`this.props.key`访问它的值。React会通过`key`自动判断出哪个组件需要更新。组件是不能访问到它的`key`的。

**强烈推荐每次在构建动态列表时，指定key属性。**如果没有指定任何的 key ，React 会输出一个警告，并且会默认使用数组的索引作为`key`。显示的使用`key = {i}`会消除警告，但是如果想要对列表进行重新排序、新增、删除操作时，把数组索引作为 key 是有问题的。所以大多数场景下并不推荐这种用法。