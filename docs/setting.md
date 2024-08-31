---
sidebar_position: 7
---

# 配置项

配置项在 Setting 类。

完整配置如下：

```ts
{
  // 画布背景色
  canvasBgColor: '#f4f4f4',
  // 创建第一个 stroke 时的颜色值
  firstStroke: {
    type: PaintType.Solid,
    attrs: { r: 0, g: 0, b: 0, a: 1 },
  } as IPaint,
  // stroke 宽度
  strokeWidth: 1,

  // 创建第一个 fill 时的颜色值
  firstFill: {
    type: PaintType.Solid,
    attrs: { r: 217, g: 217, b: 217, a: 1 },
  } as IPaint,
  // 已经有至少一个 fill 时，再创建一个 fill 的颜色值
  addedPaint: {
    type: PaintType.Solid,
    attrs: { r: 0, g: 0, b: 0, a: 0.2 },
  } as IPaint,

  // 创建星形图形时的默认内径值
  defaultStarInnerScale: 0.3819660246372223,

  // 包围盒描边色
  guideBBoxStroke: '#1592fe',
  // 包围盒线宽
  guideBBoxStrokeWidth: 1.2,

  // 选区描边色
  selectionStroke: '#0f8eff',
  // 选区填充色
  selectionFill: '#0f8eff33',
  // 框选策略
  selectionMode: 'intersect' as 'intersect' | 'contain',

  // 点选时容差，点选更容易
  selectionHitPadding: 4,
  // 悬停在图形面板的图形上，画布中的图形是否要高亮
  highlightLayersOnHover: true,
  // 悬停高亮描边宽度
  hoverOutlineStrokeWidth: 2,
  // 悬停高亮描边色
  hoverOutlineStroke: '#1592fe',

  // 选中图形高亮线宽
  selectedOutlineStrokeWidth: 1,

  /******** transform control handle ********/
  handleStroke: '#1592fe',
  handleFill: '#fcfcfc',
  handleStrokeWidth: 2,
  handleSize: 7,
  neswHandleWidth: 10, // north/east/south/west handle width

  /********* text ********/
  defaultFontSize: 12,
  textFill: [
    {
      type: PaintType.Solid,
      attrs: { r: 0, g: 0, b: 0, a: 1 },
    },
  ] as IPaint[],

  lockRotation: Math.PI / 12, // 旋转时，通过 shift 约束旋转角度为该值的整数倍。

  /*********** zoom *************/
  zoomStep: 0.2325,
  zoomMin: 0.015625,
  zoomMax: 256,
  zoomLevels: [
    0.015625, 0.03125, 0.0625, 0.125, 0.25, 0.5, 1, 2, 4, 8, 16, 32, 64, 128,
    256,
  ],

  drawGraphDefaultWidth: 100, // drawing graphics default width if no drag
  drawGraphDefaultHeight: 100, // default height

  /**** ruler ****/
  enableRuler: true,
  minStepInViewport: 50, // 视口区域下的最小步长
  rulerBgColor: '#fff',
  rulerStroke: '#e6e6e6',
  rulerMarkStroke: '#c1c1c1',
  rulerWidth: 20, // 宽度
  rulerMarkSize: 4, // 刻度高度

  /**** pixel grid ****/
  enablePixelGrid: true,
  snapToGrid: true, // 是否吸附到网格
  minPixelGridZoom: 8, // draw pixel grid When zoom reach this value
  pixelGridLineColor: '#cccccc55', // pixel grid line color

  gridViewX: 1,
  gridViewY: 1,
  gridSnapX: 1,
  gridSnapY: 1,

  dragBlockStep: 4, // drag handler will not happen if move distance less this value

  // 画布相对页面左上角的位置
  offsetX: 0,
  offsetY: 0,

  /**** zoom ****/
  // 缩放为适应画布时，图形包围和到画布边缘的边距
  zoomToFixPadding: 32, // base viewport coord
  // 缩放是否反向
  invertZoomDirection: false, // zoom in/out direction

  // 通过方向键移动选中图形，移动的距离
  smallNudge: 1,
  // 大幅移动选中图形的距离
  bigNudge: 10,
  // 移动图形会创建历史记录，此为节流时间
  moveElementsDelay: 500,

  // reference line
  refLineTolerance: 4,
  refLineStroke: '#f14f30ee',
  refLineStrokeWidth: 1,
  refLinePointSize: 5,

  /**** tool ****/
  // 工具使用完，比如绘制完矩形，是否留在当前工具，不回到选择工具
  keepToolSelectedAfterUse: false,
  pencilCurveFitTolerance: 1,

  /******** path control handle ******/
  pathLineStroke: '#a4a4a4',

  /**** angle ****/
  angleBase: { x: 0, y: -1 }, // no use now

  flipObjectsWhileResizing: true,

  continueClickMaxGap: 350, // millisecond
  continueClickDistanceTol: 5,
};
```