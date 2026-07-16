# 像素头像生成器

一个基于 HTML Canvas 的单文件像素头像生成器。无需安装依赖、无需启动服务器，直接使用浏览器打开即可生成、编辑并导出头像。

页面使用 **32 × 32 逻辑像素网格**进行编辑，每个逻辑像素对应导出图片中的 8 × 8 像素，因此最终 PNG 尺寸固定为 **256 × 256**。

## 功能

- 根据随机种子生成可复现的像素头像
- 支持画笔、橡皮、区域填充和颜色吸取
- 支持 1、2、3 像素画笔尺寸
- 支持左右镜像绘制
- 支持显示或隐藏编辑网格
- 支持撤销和重做，最多保留 60 个历史状态
- 支持导出和导入 JSON 编辑数据
- 支持导出无网格的 256 × 256 PNG
- 支持鼠标、触控屏及移动端布局
- 所有数据均在浏览器本地处理，不会上传到服务器

## 快速开始

找到项目中的 [`pixel-avatar-generator.html`](./pixel-avatar-generator.html)，双击后使用 Chrome、Edge 或 Firefox 打开。

也可以在项目目录中使用 PowerShell：

```powershell
Start-Process .\pixel-avatar-generator.html
```

该项目没有外部依赖，不需要执行 `npm install`，也不需要本地 Web 服务器。

## 使用方法

### 1. 生成头像

1. 在“随机种子”输入框中填写名称、编号或任意文本。
2. 点击“生成头像”。
3. 相同的种子会生成相同的头像。
4. 点击种子输入框右侧的 `↻` 按钮，可创建新种子并立即生成头像。

### 2. 编辑头像

| 工具 | 作用 |
| --- | --- |
| 画笔 | 使用当前颜色绘制像素 |
| 橡皮 | 将像素恢复为透明 |
| 填充 | 将相邻且颜色相同的区域整体替换为当前颜色 |
| 取色 | 从画布上读取一个已有颜色 |

可以通过颜色选择器或下方调色板设置当前颜色，通过画笔下拉框选择 1、2、3 像素画笔。

“镜像绘制”开启时，在画布一侧绘制的内容会同步到另一侧，适合快速制作对称头像。“显示网格”只影响编辑预览，不会出现在导出的 PNG 中。

### 3. 撤销和重做

可以直接点击“撤销”和“重做”按钮，也可以使用以下快捷键：

| 操作 | Windows / Linux | macOS |
| --- | --- | --- |
| 撤销 | `Ctrl + Z` | `Command + Z` |
| 重做 | `Ctrl + Y` 或 `Ctrl + Shift + Z` | `Command + Shift + Z` |

### 4. 保存编辑数据

点击“导出数据”会下载 `pixel-avatar.json`。该文件包含随机种子、网格尺寸和全部像素颜色，可用于继续编辑。

点击“导入数据”并选择之前导出的 JSON 文件，即可恢复头像。当前版本仅接受 32 × 32 网格数据。

### 5. 导出 PNG

点击“下载 PNG”即可获得头像图片。文件名格式为：

```text
pixel-avatar-随机种子.png
```

导出的图片尺寸固定为 256 × 256，编辑网格不会被导出。使用橡皮或“清空画布”产生的空白区域会保持透明。

## 项目文件

```text
.
├── pixel-avatar-generator.html  # 页面、样式和全部交互逻辑
└── README.md                    # 使用说明
```

`pixel-avatar-generator.html` 内部包含完整的 HTML、CSS 和 JavaScript，移动或分享时只需要携带这一个文件。

## 自定义

头像生成和画布参数位于 HTML 文件底部的 `<script>` 中：

```javascript
const OUTPUT_SIZE = 256;
const GRID_SIZE = 32;
const CELL_SIZE = OUTPUT_SIZE / GRID_SIZE;
const MAX_HISTORY = 60;
```

- `OUTPUT_SIZE`：导出图片的宽度和高度。
- `GRID_SIZE`：逻辑像素网格尺寸。
- `MAX_HISTORY`：撤销历史的最大数量。
- `PALETTE`：页面中显示的常用颜色。

修改 `GRID_SIZE` 时，应确保 `OUTPUT_SIZE / GRID_SIZE` 为整数，并注意旧版 JSON 数据将无法直接导入。

## 浏览器兼容性

建议使用较新版本的 Chrome、Edge 或 Firefox。浏览器需要支持 Canvas、Pointer Events、FileReader、Blob 和 `HTMLCanvasElement.toBlob()`。

如果点击下载后没有出现文件，请检查浏览器是否阻止了本地页面下载。

