**Skin** 节点适用于把多条曲线（Curve）连接成面。它常用于从一组轮廓线、截面线、内外边界线生成连续的面。这些曲线的类型可以不同，Polygon、Bezier 和 NURBS 都是有效的类型。

#### 工作原理
**Skin** 会读取**输入端子1**中的多条曲线基元，并按照基元排列顺序，把相邻曲线连接起来。

也就是说，**Skin** 判断“有多少条曲线”参与计算，主要看**输入端子1** Geometry SpreadSheet 的基元列表中有多少个曲线。

例如，在**输入端子1** Geometry SpreadSheet 的基元列表中：

```text
基元0 = Curve A
基元1 = Curve B
基元2 = Curve C
```

此时，会按照以下顺序进行连接：

```text
Curve A -> Curve B
Curve B -> Curve C
```

两条曲线之间的点具体怎么连，取决于每条曲线内的点顺序。
```text
Curve A: A0 -- A1 -- A2 -- A3
Curve B: B0 -- B1 -- B2 -- B3
```

**Skin** 会连接：

```text
A0 <-> B0
A1 <-> B1
A2 <-> B2
A3 <-> B3
```

并生成面片：

```text
A0, A1, B1, B0
A1, A2, B2, B1
A2, A3, B3, B2
```

多条曲线都需要从 **Skin** 的**输入端子1**输入。因此，需要先把所有曲线合并成一个 Geometry Stream：

```text
Curve A ┐
Curve B ├─ Merge / 同一个节点输出 -> Skin
Curve C ┘
```

而不是把不同曲线分别接到不同输入端口。

#### **Skin** 的输入端子
仅**输入端子1**连了输入时，**Skin**执行「线性蒙皮」（Linear-skinning），在横截面之间蒙皮，得到经典的直纹蒙皮面。

当**输入端子2**也连了输入时，**Skin**执行「双线性蒙皮」（Bi-linear skinning），把第一个输入作为 U 横截面，把第二个输入作为 V 横截面，在它们之间做交叉线蒙皮。