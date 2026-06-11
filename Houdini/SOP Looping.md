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
对指定物体的分件（Piece）和控点（Point）。此时，
1、输入端 Block Begin 节点的 Method 参数只能选：
① Extract Piece or Point：每次循环计算基于分件或控点（早期版本叫 Fetch Piece or Point）
2、输出端 Block End 节点的 Iteration Method 参数只能选：
① By Pieces or Points：根据分件或控点来决定循环次数

##### 分件（Piece）
Houdini中的几何体的本质非常纯粹，就是一堆基元（Primitive）的集合。要把这些杂乱的基元织成“分件A”和“分件B”，全靠一个约定：拥有相同属性值的基元，就属于同一个分件。这个属性通常被命名为 piece、name、class 或 path。属性的类型可以是整数，也可以是字符串。这是一种非常灵活、以属性驱动的方式。

##### 输出端 Block End 节点的 Gather Method 参数
1、Feedback Each Iteration：输出最后一次循环计算的结果
2、Merge Each Iteration：输出合并每次循环计算的结果
这两个选项对 For-Loop 和 For-Each 都生效。

##### Block End 节点的第二个输入端子
细心的用户会发现 Block End 节点有两个输入端子。这个输入端子只在 For-Each 循环的情况下有效，用于指定的分件的输入源。

你也可以使用 Piece Block Path 参数来指定分件的输入源，一般是一个 Block Begin 节点。此时，Block End 节点会把 Block Begin 的唯一输入端子作为分件的输入源读取分件数据。Houdini 预设的 For-Each 节点使用的都是这种模式。

当 Block End 节点的第二个输入端子连接了一个输入源，这时 Piece Block Path 参数就会失效，Piece Block Path 参数的输入框会被隐藏。此时，即使 Block Begin 节点的输入端子上没有连接任何节点，也不影响正常遍历分件。

参考：
1、[Looping in geometry networks](https://www.sidefx.com/docs/houdini/model/looping.html)
2、[Understanding pieces](https://www.sidefx.com/docs/houdini/nodes/sop/attribfrompieces.html#understanding-pieces)
3、[这可能是B站最容易理解的Houdini循环系统](https://www.bilibili.com/video/BV1Fq4y1T7J7)