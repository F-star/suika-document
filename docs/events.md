---
sidebar_position: 6
---

# 事件

Editor 类的各个子类管理着自己的状态，当这些状态发生变化时，会通过事件订阅发布的方式通知其他模块，这样以实现模块间的解耦。


## 用法

比如当编辑器的画布缩放比（zoom）改变时，会通过 'zoomChange' 事件通知给业务组件，让其更新 UI 上的 zoom 值。

```ts
const updateZoom = (zoom: number) => {
  // ...
  setZoom(zoom);
};

// 组件初始化时需要主动获取状态（因为此时没有事件发生）
updateZoom(editor.zoomManager.getZoom())

// 订阅事件
editor.zoomManager.on('zoomChange', updateZoom);

// 组件销毁时，记得取消监听
editor.zoomManager.off('zoomChange', updateZoom);
```

## Editor

```ts
interface Events {
  destroy(): void; // 编辑器销毁事件
}
```

## ZoomManger

editor.zoomManager

```ts
interface Events {
  // 画布缩放比 zoom 发生改变
  zoomChange(zoom: number, prevZoom: number): void;
}
```

## CanvasDragger

editor.canvasDragger

```ts
interface Events {
  // 画布拖拽状态 是否激活
  activeChange(active: boolean): void;
}
```

## ImageManager

editor.imageManger

```ts
interface Events {
  // 图片添加
  added(img: HTMLImageElement): void;
}
```

## SelectedBox

```ts
interface Events {
  // 光标是否在选中框上悬停
  hoverChange(isHover: boolean): void;
}
```

## SelectElements

```ts
interface Events {
  // 选中图形改变
  itemsChange(items: SuikaGraphics[]): void;
  // 悬停图形改变
  hoverItemChange(
    item: SuikaGraphics | null,
    prevItem: SuikaGraphics | null,
  ): void;
  // 高亮图形改变
  //一般是悬停在图形上才高亮，但 hover 在图形面板上也希望高亮
  highlightedItemChange(
    item: SuikaGraphics | null,
    prevItem: SuikaGraphics | null,
  ): void;
}
```

## Setting

```ts
interface Events {
  // 设置改变，会拿到所有的属性值的浅拷贝
  update(attrs: SettingValue): void;
}
```

## CommandManager

```ts
interface Events {
  // 历史记录列表发生变化
  change(status: IHistoryStatus): void;
  // 执行命令前的事件钩子
  beforeExecCmd(): void;
}

interface IHistoryStatus {
  canRedo: boolean;
  canUndo: boolean;
}
```

## Document

```ts
interface Events {
  // 场景树的图形发生变化，包括图形属性变更、添加图形、删除图形
  sceneChange(
    ops: {
      added: Map<string, GraphicsAttrs>;
      deleted: Set<string>;
      update: Map<string, Partial<GraphicsAttrs>>;
    },
    source: string,
  ): void;
}
```

## HostEventManager

editor.hostEventManager

原生事件的封装。

```ts
interface Events {
  // 按下/释放 shift 键
  shiftToggle(press: boolean): void;
  // 按下/释放 alt 键
  altToggle(press: boolean): void;
  // 按下/释放空格键
  spaceToggle(press: boolean): void;
  // 右键菜单
  contextmenu(point: IPoint): void;
}
```

## MouseEventManager

浏览器 Pointer 事件封装。

```ts
interface Events {
  // 按下/释放 滚轮键
  wheelBtnToggle(press: boolean, event: PointerEvent): void;
  // 光标位置更新
  cursorPosUpdate(pos: IPoint | null): void;
  // 鼠标按下
  start(event: IMouseEvent): void;
  // 鼠标释放
  end(event: IMouseEvent): void;
  // 移动（拖拽状态时不触发）
  move(event: IMousemoveEvent): void;
  // 拖拽
  drag(event: IMousemoveEvent): void;
  // 连击
  comboClick(event: IMouseEvent): void;
}
```

## PathEditor

路径编辑器

```ts
interface Events {
  // 是否激活
  toggle: (active: boolean) => void;
}
```

## SceneGraph

```ts
interface Events {
  // 渲染
  render(): void;
}
```

## ToolManager

```ts
interface Events {
  // 切换工具事件
  switchTool(type: string): void;
  // 设置可用工具时触发（不能切换到非可用工具）
  changeEnableTools(toolTypes: string[]): void;
}
```