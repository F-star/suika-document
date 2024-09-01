---
sidebar_position: 5
---

# 类

## 编辑器类 Editor

编辑器入口类。下面挂载各种子模块。

## 工具管理类 ToolManager

工具管理类。

可注册具体的工具类，切换工具。

切换工具会调用工具类的生命周期钩子。

从工具 A 切换为工具 B，会调用工具 A 的 onInactive 方法，然后调用工具 B 的 active 方法。

当鼠标和键盘事件发生时，会改为调用工具 B 对应的方法。

## 工具类 Tool

工具类。

需要注册到工具管理类中。

工具类需要实现接口为：

```ts
export interface ITool extends IBaseTool {
  hotkey: string | IKey;
  type: string;
  cursor: ICursor;
  onMoveExcludeDrag: (event: PointerEvent, isOutsideCanvas: boolean) => void;
  getDragBlockStep?: () => number;
}

export interface IBaseTool {
  onActive: () => void;
  onInactive: () => void;
  onStart: (event: PointerEvent) => void;
  onDrag: (event: PointerEvent) => void;
  /**
   * end (after drag)
   * @param event
   * @param isDragHappened is drag happened
   * @returns
   */
  onEnd: (event: PointerEvent, isDragHappened: boolean) => void;
  /** init state when finish a drag loop */
  afterEnd: (event: PointerEvent, isDragHappened: boolean) => void;
  onCommandChange?: () => void;
  /** space key toggle */
  onSpaceToggle?: (isSpacePressing: boolean) => void;
  /** shift key toggle */
  onShiftToggle?: (isShiftPressing: boolean) => void;
  /** alt key toggle */
  onAltToggle?: (isAltPressing: boolean) => void;
  /** viewport x or y change */
  onViewportXOrYChange?: (x: number, y: number) => void;
  /** canvas drag active change */
  onCanvasDragActiveChange?: (isActive: boolean) => void;
}
```

实现的工具类有以下几种

### 选择工具类

选择工具类因为行为过多，需使用 **策略模式分** [将不同行为分支分为多种策略](https://mp.weixin.qq.com/s/lXv5_bisMHVHqtv2DwflwA)，这些策略会抽象为子类；

1. SelectMoveTool：移动图形类，管理图形的移动逻辑；
2. DrawSelectionBox：绘制矩形选区类，当鼠标在空白区域按下然后拖拽，会产生一个选区；
3. SelectRotationTool：旋转选中图形类；
4. SelectResizeTool：缩放选中图形类。现在扩展为支持自定义控制点，自定义控制点的逻辑需要在图形类中实现。

### 绘制图形类

绘制图形类有两种，一种是形式固定的，就是按下移动释放，得到两个点，依此得到 x、y、width、height。

可以用这 4 个属性表达的图形，它们的绘制逻辑就是相同的，比如绘制矩形、椭圆、正多边形、星形。对此我们要使用模板模式，抽象一个名为 `DrawGraphTool` 的抽象类，让它们继承即可。

不同的地方只是传入的图形对象不同。

另一种则是更灵活的图形，它们不依赖 x、y、width、height。比如绘制文字、钢笔工具。这些就无法去继承实现 `DrawGraphTool` 了。

已经实现的图形类。

继承 DrawGraphTool 类的工具类：

1. DrawRectTool：绘制矩形类；
2. DrawEllipseTool：绘制椭圆类；
3. DrawLineTool：绘制直线类；
4. DrawRegularPolygonTool：绘制椭圆类；
5. DrawStarTool：绘制星形类；

其它没有继承

1. ToolDrawText