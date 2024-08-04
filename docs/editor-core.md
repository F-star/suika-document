---
sidebar_position: 4
---

# 编辑器内核

编辑器内核在 `@suika/core` 包内。

创建 SuikaEditor 对象需要传入的参数：

```ts
interface IEditorOptions {
  /** canvas 元素挂载的 div 容器 */
  containerElement: HTMLDivElement;
  /** 画布的初始宽高 */
  width: number;
  height: number;
  /** 画布距离网页左上脚的偏移值 */
  offsetX?: number;
  offsetY?: number;
  /** 是否打开性能监控器 */
  showPerfMonitor?: boolean;
}
```

创建 SuikaEditor 实例：

```ts
import { SuikaEditor } from '@suika/core';

const editor = new SuikaEditor({
  containerElement: containerDiv,
  width: document.body.clientWidth - leftRightMargin,
  height: document.body.clientHeight - topMargin,
  offsetY: 48,
  offsetX: 240,
});
```

## 子模块

SuikaEditor 下的各个子模块说明：

[模块关系脑图](https://f5b8b9lm1y.feishu.cn/mindnotes/DgJRb2GpGmdGdKnfl3rcJzw6n5e#mindmap)

