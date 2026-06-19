**Ends** 节点用于控制曲线或曲面首尾两端点的开闭，以及NURBS的首尾是否固定在原来的位置。

#### Close U / Close V
控制 U / V 方向的首尾连接方式。
No Change：不改变当前开闭状态。
Open：删除首尾连线，从而使首尾开放。
Close Straight：用直线连接首尾，从而闭合首尾。
Close Rounded：用平滑方式连接首尾，从而闭合首尾。仅对 NURBS 有效，对于折线来说还是用直线连接首尾。
Unroll with New Points：在尾端创建一个新的点位和首端连接，尾端和新的点位不连接，从而使首尾开放。
Unroll with Shared Points：在尾端创建一个新的顶点和首端连接，尾端和新的顶点连接，从而使首尾开放。

#### Clamp U / Clamp V
用于 NURBS，控制端点是否固定在原来的端点位置。

No Change：不改变当前端点状态。
Clamp：固定端点，让端点固定在原来的位置。
Unclamp：释放端点，让 NURBS 按自身平滑方式计算端部。

#### Preserve Shape U / Preserve Shape V
在执行闭合或固定端点时，尽量保持原来的形状不变，减少形状被拉扯或变形。仅对 NURBS 有效。

#### Unreal Engine 插件
与Houdini曲线不同，封闭的Unreal样条曲线并不是作为一个封闭曲线创建的，而是作为一个在起始点和结束点相同的开放曲线创建的。如果你的HDA通常期望一个封闭曲线（定义一个多边形），你可以使用"Ends"节点，并将"Close U"参数设置为"Close Straight"，以确保你的曲线输入是封闭的。