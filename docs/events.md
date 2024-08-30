---
sidebar_position: 6
---

# 事件

Editor 类的各个子类管理着自己的状态，但它们发生变化时，会通过事件订阅发布的方式通知其他模块，实现模块间的解耦。


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

## zoomManger

`editor.zoomManager`

```ts
interface Events {
  zoomChange(zoom: number, prevZoom: number): void; // 画布缩放比 zoom 发生改变
}
```

...