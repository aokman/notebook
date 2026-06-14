# Houdini Skin 节点总结

`Skin` 节点用于把多条曲线连接成面。它常用于从一组轮廓线、截面线、内外边界线生成连续的 surface 或 polygon 面。

## 作用

`Skin` 会读取输入中的多条 curve primitive，并把相邻曲线连接起来。

例如：

```text
curve A
curve B
```

经过 `Skin` 后，会在两条曲线之间生成一圈面片。

在围墙案例里：

```text
inside 边线 + outside 边线 -> Skin -> 墙体底面
```

然后再接 `PolyExtrude`，就可以生成有厚度、有高度的墙体。

## 原理

`Skin` 判断“有多少条曲线”，主要看输入 geometry 里有多少个 curve primitive。

例如：

```text
Primitive 0 = curve A
Primitive 1 = curve B
Primitive 2 = curve C
```

它会按 primitive 顺序连接：

```text
curve A -> curve B
curve B -> curve C
```

两条曲线之间的连接，基本是按顶点或点的顺序一一对应：

```text
curve A: A0 -- A1 -- A2 -- A3
curve B: B0 -- B1 -- B2 -- B3
```

`Skin` 会连接：

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

## 使用方法

多条曲线通常都从 `Skin` 的第一个输入端子输入。也就是先把曲线合并成一个 geometry stream：

```text
curveA ┐
curveB ├─ Merge / 同一个节点输出 -> Skin
curveC ┘
```

而不是把不同曲线分别接到不同输入端口。

使用时注意：

- 每条曲线最好是一个独立 primitive。
- Primitive 顺序决定连接顺序。
- 曲线点数最好一致。
- 曲线方向最好一致。
- 闭合曲线的起点最好对应。
- 点顺序不一致时，面会扭曲或交叉。

## 常用辅助节点

- `Merge`：把多条曲线合成一个输入流。
- `Sort`：调整点或 primitive 顺序。
- `Reverse`：反转曲线方向。
- `Resample`：统一曲线点数或分布。
- `PolyExpand2D`：生成 inside/outside 边线，再交给 `Skin` 连接成面。

## 当前围墙网络示例

当前围墙网络的逻辑是：

```text
curve1
-> PolyExpand2D 生成 inside / outside 两条边线
-> Skin 把两条边线连接成墙体底面
-> PolyExtrude 向上挤出 1 米
```

