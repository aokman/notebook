#### Carve 节点的用途
Carve 节点适用于任何表面（Face）或曲面（Surface）类型的基元（Primitive），无论是多边形、Bezier 亦或是 NURBS。该节点在这些基元的参数域 (U/V) 上进行提取、切片、切割操作。

##### 1. Extract（提取）
从基元上提取**点**或**截面**。（最有用）

##### 2. Slice（截取）
通过设置 First U=0, Second U=1 可以截取截面上的一段。（很有用）

##### 3. Cut（切割）
可以把截面（单个基元）的每一段边缘切割成一个基元。（操作线段时有用，例如：栏杆）

**注意：** Carve 节点会把闭合的面转换成开放的面，导致面不再被渲染。可以通过 Geometry Spreadsheet 的 Primitive 页签中的 intrinsics:closed 属性查看基元的开闭性。处理后的基元类型可以通过 intrinstics:typename 查看。

#### 表面（Face）和曲面（Surface）的区别
表面（Face）是一种几何基元（Prim对象），包含一个存储顶点（Vertex对象）的一维数组。这些顶点的使用方式取决于面的类型；例如，Polygon使用这些顶点来定义多边形的边，而Bezier Curve和NURBS Curve则将它们用作控点。

曲面（Surface）是一种几何基元（Prim对象），包含一个存储顶点（Vertex对象）的二维数组。这些顶点的使用方式取决于曲面的类型：例如，Mesh使用这些顶点来定义四边形网格，而Bezier Surface和NURBS Surface则将它们用作控点。 

表面和曲面都是参数化方程，表面是折线或曲线围成的面，用一个参数U就可以表达，曲面是由多边形或参数曲面构成的体，需要用UV两个参数来表达。

为了方便理解，表面≈曲线，曲面=曲面