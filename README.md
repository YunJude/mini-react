# mini-react
最近参加了mini-react游戏副本，一群人一起完成同样的任务会碰撞出不同火花，看看别人是怎么思考的，参考下。每天完成一个功能并且实现是合理并且很有收获的。通过实际应用场景来思考功能的实现。一小步一小步的完成任务会很有成就感。并且不会有那种一看到的大量代码放弃的想法。

# 结课总结
我们先是实现了使用vite实现对jsx的支持，之后设计了render / initChildren等函数来 实现react的fiber，以及简单的任务调度。实现集中commit和函数组件支持 function Component 之后实现简单的dom更新和children的初步更新，新增和删除 update , 最后是 useState 和 useEffect 。还有面试问react原理要怎么回答。

1. createRoot和render的初步实现
从最原始的通过使用简单的js的document Api创建 dom，到抽象出虚拟vdom对象 ，再到最后的 jsx语法。
render使用递归的方式实现dom的创建，当层级非常非常深的时候循环n+可能会出现页面渲染卡顿，原因就是render 的执行时间过长，超过了浏览器一帧一帧渲染视图的时间，我们知道执行js会阻塞dom 渲染，因此会有卡顿问题出现。

2. Fiber
更新的流程有了大概的了解。我理解的fiber是，​fiber​在整个react架构的整个流程都至关重要。可以说，无论是react的初次渲染还是后续的更新，都是以fiber​作为最小任务进行执行。​fiber​其实就是保存了一个节点在各个执行流程中所需要的各种信息，所代表的真实dom节点，与父/子/兄弟节点之间的关系，更新相关的信息，优先级。
通过 js 的 requestIdleCallback 函数实现，传入一个函数，函数会接收一个 IdleDeadline 参数，他提供了 timeRemaining() 方法用于获取当前执行的空闲时间，利用空闲时间来执行渲染工作

3. 实现functionComponent
实现Function Component，根据函数生成Dom，并且可以传入props，过程中需要注意，由于function component 本身没有Dom，在寻找父容器和兄弟节点时，需要采用循环向上的方式。

4. 实现简单的dom更新和children的初步更新，新增和删除。

5.实现简单的useState和useEffect
实现 useEffect 存起来 effecthooks 调用时机，在 commitWork 之后执行commitEffectHook 依次遍历找到对应的节点两种情况初始化、依赖项有没有改变。
