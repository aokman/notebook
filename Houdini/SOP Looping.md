通常情况下，Houdini 按照从上到下的顺序执行几何网络中的节点，将每个节点的输出传递到下一个节点的输入，直到某个开启了 **Display/Render** 标志位的节点才会结束执行。然而，在某些情况下，需要在循环中**多次执行**同一组节点链，这时 Houdini 的循环结构体就变得非常有用了。

**注意**：多次执行同一组节点链的意思是，如果节点链中的节点的某些参数包含表达式，这些表达式也会被重新评估。

**提示**：节点链中的节点可以将 Foreach Metadata 节点的属性用于表达式的评估。

Houdini的循环是通过 Block Begin 和 Block End 两个节点实现的。根据两个节点的参数选择不同分为 For-Loop 和 For-Each 两类。在网络编辑器的Tab菜单中内置了常用的循环节点设置。

##### For-Loop
在指定物体上，重复执行一组操作，直至指定次数。此时，
1、输入端 Block Begin 节点的 Method 参数只能选：
① Fetch Feedback：每次循环计算基于上次的计算结果
② Fetch Input：每次循环计算基于原始输入数据
2、输出端 Block End 节点的 Iteration Method 参数只能选：
① By Count：用数字自定义循环次数
 
##### For-Each
对指定物体的分件和控点，

输出端 Block End 节点的 Gather Method 参数：
1、Feedback Each Iteration：输出最后一次循环计算的结果
2、Merge Each Iteration：输出合并每次循环计算的结果