# Graphics 组件参考

Graphics 组件提供了一系列绘画接口，这些接口参考了 canvas 的绘画接口来进行实现。

## 路径

| 方法 |   功能说明
| -------------- | ----------- |
| [moveTo (x, y)](../graphics/moveTo.md)  | 把路径移动到画布中的指定点，不创建线条
| [lineTo (x, y)](../graphics/lineTo.md) | 添加一个新点，然后在画布中创建从该点到最后指定点的线条
| [bezierCurveTo (c1x, c1y, c2x, c2y, x, y)](../graphics/bezierCurveTo.md) | 创建三次方贝塞尔曲线
| [quadraticCurveTo (cx, cy, x, y)](../graphics/quadraticCurveTo.md) | 创建二次贝塞尔曲线
| [arc (cx, cy, r, a0, a1, counterclockwise)](../graphics/arc.md) | 创建弧/曲线（用于创建圆形或部分圆）
| [ellipse (cx, cy, rx, ry)](../graphics/ellipse.md) | 创建椭圆
| [circle (cx, cy, r)](../graphics/circle.md) | 创建圆形
| [rect (x, y, w, h)](../graphics/rect.md) | 创建矩形
| [close ()](../graphics/close.md) | 创建从当前点回到起始点的路径
| [stroke ()](../graphics/stroke.md) | 绘制已定义的路径
| [fill ()](../graphics/fill.md) | 填充当前绘图（路径）
| [clear ()](../graphics/clear.md) | 清楚所有路径

## 颜色，样式

| 属性 |   功能说明
| -------------- | ----------- |
| [lineCap](../graphics/lineCap.md) | 设置或返回线条的结束端点样式
| [lineJoin](../graphics/lineJoin.md) | 设置或返回两条线相交时，所创建的拐角类型
| [lineWidth](../graphics/lineWidth.md) | 设置或返回当前的线条宽度
| [miterLimit](../graphics/miterLimit.md) | 设置或返回最大斜接长度
| [strokeColor](../graphics/strokeColor.md) | 设置或返回笔触的颜色
| [fillColor](../graphics/fillColor.md) | 设置或返回填充绘画的颜色

更多关于 **Graphics** 的信息请前往 [绘画](../graphics/index.md)

<hr>

继续前往 [RichText 组件参考](richtext.md) 说明文档。
