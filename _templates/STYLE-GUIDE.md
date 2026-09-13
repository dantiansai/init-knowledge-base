---
title: "STYLE-GUIDE"
type: doc
tags:
  - meta/style
status: "stable"
last_updated: "2026-09-14"
---

# 样式指南 · Editorial

编辑风样式（`Editorial for Knowledge Base`）的活样式表。这一页本身就是样例 —— 在 Obsidian 里打开它，看到什么样式，知识库里就是什么样式。

> **定位**：中文出版物的版面感。标题走衬线承担「版面」职责，正文走黑体保证屏幕可读性；表格只留横线（三线表），引用去底色只留竖线；界面用发丝线分区，用一道 2px 强调色短线标记当前位置。

---

## 一、色彩系统

| 用途 | 明色「宣纸」 | 暗色「夜墨」 |
|------|-------------|-------------|
| 纸面底色 | `#FCFBF7` | `#1B1A18` |
| 侧栏 / 凹陷面 | `#F3F1EA` | `#141312` |
| 抬起面（代码块） | `#FFFFFF` | `#232120` |
| 正文墨色 | `#23211C` | `#E6E2D8` |
| 次级文字 | `#6E6A60` | `#9B958A` |
| 发丝线 | `#E4E0D6` | `#302D29` |
| 强调（胭脂） | `#A34A52` | `#E0919A` |
| 高亮（蜂蜜金） | `rgba(245,201,122,.42)` | `rgba(245,201,122,.20)` |

语义色全部压到出版级低饱和：朱 `#B4453F` / 赭 `#C07A3E` / 琥珀 `#A8871F` / 苔绿 `#4F7A52` / 青 `#3E7A78` / 墨蓝 `#3F6484` / 紫檀 `#7A5A86`。

---

## 二、排版层级

### 这是 H3（黑体，1.2em）

正文 16px，行高 1.8，字距 +0.012em —— 中文长文在这个组合下最省力。栏宽 42rem（约 34 个汉字/行），是屏幕阅读的舒适上限。

**加粗用 650 字重**而不是 700，避免中文字面糊成一团。*斜体*走真斜体，`行内代码`走等宽 + 浅底。

#### 这是 H4（1.06em，黑体）

##### 这是 H5（0.97em，压暗）

###### 这是 H6（0.88em，字距拉开，最淡）

**排序**：H1 带一道短胭脂线 → H2 带上方发丝线（像印刷品的分栏线）→ H3 起转为黑体。层级靠字体族和线来区分，不靠大小硬撑。

---

## 三、列表与任务

无序列表：

- 第一层，圆点压到最淡
- 第二层
  - 第三层，缩进参考线也压到几乎看不见
- 回到第一层

有序列表（编号用衬线 + 胭脂色，是版面里少数允许「出声」的地方）：

1. 界定研究问题
2. 收集来源并评估可信度
3. 交叉验证，标记冲突
4. 形成判断并留存推理链

任务列表：

- [x] 已完成的条目会压暗并划掉
- [ ] 未完成条目保持常态
- [x] 复选框是 2px 圆角的方块，不是圆点

---

## 四、表格（三线表）

| 维度 | 旧样式 | 编辑风 | 收益 |
|------|--------|--------|------|
| 边框 | 全网格线 | 只有三条横线 | 视觉噪音大幅下降 |
| 表头 | 灰底 + 蓝字 | 无底 + 1.5px 主分隔线 | 像学术出版物 |
| 行分隔 | 1px 灰线 | 1px 发丝线 | 密集数据依然可读 |
| 悬停 | 整行灰底 | 极淡强调色底 | 定位不打断阅读 |
| 第一列 | 与正文同 | 加重为行标题 | 扫读更快 |

> 数字列建议手写 `<td align="right">`，会自动启用等宽数字对齐。

---

## 五、全部 Callout 类型

> [!note] 笔记 / info / 笔记
> 墨蓝。左侧 2px 实色竖线 + 一圈发丝描边，底色只留 4.5% 透明度。

> [!abstract] 摘要 / summary / tldr
> 青。适合放在页面顶部的「一句话总结」。

> [!todo] 待办
> 青。与摘要同色系。

> [!tip] 提示 / hint / important
> 琥珀。适合放「此处的坑」。

> [!success] 成功 / check / done
> 苔绿。

> [!question] 问题 / faq / help
> 紫檀。

> [!warning] 警告 / caution / attention
> 赭石。

> [!danger] 危险 / error / bug / fail
> 朱。

> [!example] 示例
> 紫檀。

> [!quote] 引用 / cite
> 这个变体会自动切换到衬线字体，当引文用。

> [!sidenote] 页边注
> 变成页边批注。

> [!caption] 图注
> 变成居中小字。

折叠式（标题末尾加 `-` 默认折叠）：

> [!faq]- 点开看答案
> 折叠状态的箭头会旋转，展开高度不跳动。

---

## 六、版式扩展示例

### 6.1 多栏

> [!multi-column]
>
>> [!note]+ 左栏
>> 用 `> [!multi-column]` 包住若干子 callout，子块按可用宽度自动等分，放不下就换行。
>
>> [!warning]+ 中栏
>> 指定栏数：`> [!multi-column|2col]`、`3col`、`4col`。
>
>> [!success]+ 右栏
>> 窄屏（< 640px）自动退回单栏。

### 6.2 浮动批注框

（在右侧）语法：`> [!info|right-medium] 内容`。尺寸可选 `small` / `medium` / `large`，方向可选 `left` / `right`。

> [!info|right-medium] 右侧浮动
> 这段文字会被放在正文右侧，正文自动绕排。
> 窄屏下自动取消浮动，回到正常流。

### 6.3 页边注

正文继续推进，页边出现一条带顶线的批注。

> [!sidenote] 边注
> Tufte 式页边批注：只留一条顶线，字号 0.82em，适合放「补充说明」「我的怀疑」这类不影响主线的信息。

### 6.4 图片画廊

在一个 callout 上加 `gallery` 元数据，内部图片自动排成等高裁切网格：

````markdown
> [!note|gallery]
> ![[图一.png]]
> ![[图二.png]]
> ![[图三.png]]
````

### 6.5 图片题注

图片下面紧跟一行斜体，会自动变成居中图注：

````markdown
![[关于-LLM-的架构.png]]

*图 1 · 知识编译管线的三层结构*
````

---

## 七、代码

行内：`--line-width: 42rem`。

代码块右上角会显示语言标签：

```yaml
title: "示例"
type: concept
complexity: ⭐⭐⭐☆☆
status: "draft"
```

```python
def compile_to_wiki(raw_path: Path, wiki_root: Path) -> list[str]:
    """把 raw/ 下的资料编译进 wiki/ 并回写双链"""
    pages: list[str] = []
    for doc in iter_documents(raw_path):
        page = render_page(doc)
        pages.append(write(wiki_root, page))
    return pages
```

---

## 八、链接与标签

- 已存在的页面：[[index]] — 细下划线 + 淡胭脂底，hover 时下划线转实
- 尚不存在的页面：[[还没有这一页]] — 虚线，提示「有待补上」
- 外部链接：[Karpathy 的 LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — 墨蓝 + 右上箭头

标签走发丝描边方签：`#meta` `#meta/style` `#待整理`

关键词高亮：==被标记的句子会垫一层蜂蜜金==，深色文字保证对比度。

---

## 九、版式模式（cssclass）

在笔记 frontmatter 里声明，可以叠加：

```yaml
---
cssclass: wide-page cards
---
```

| cssclass | 效果 |
|----------|------|
| `wide-page` | 整页满宽，Dataview 仪表盘和大表格用 |
| `wide-table` | 只放宽表格，正文保持舒适栏宽 |
| `wide-dataview` | 只放宽 Dataview 结果块 |
| `narrow-page` | 收窄到 34rem，专注写作 |
| `columns-2` / `columns-3` | 正文分栏，适合 MOC、索引、术语表 |
| `list-2col` | 顶层列表变双栏 |
| `cards` | 顶层列表变卡片网格，每一项成为一张带描边的卡 |
| `article` | 成稿模式：隐藏属性区，行高提到 1.9 |
| `drop-cap` | 首段首字下沉 |
| `sticky-heading` | H2 滚动吸顶，长文里始终知道自己在哪一章 |
| `marginal` | 整页的 blockquote 变成页边批注 |
| `no-inline-title` | 隐藏文件名标题（正文自带 H1 时用） |

`cards` 和 `list-2col` 也支持行内标签写法，在列表项里写 `#cards` 或 `#cols2` 即可。

---

## 十、设计 Token

想改配色或字体，只改 `01-foundation.css` 顶部的变量即可，其余九个文件全部跟着走。

| Token | 值 | 说明 |
|-------|-----|------|
| `--ed-font-body` | PingFang SC → Hiragino Sans GB → … | 正文黑体 |
| `--ed-font-display` | Charter → Iowan Old Style → Songti SC → … | 标题衬线 |
| `--ed-font-mono` | SF Mono → MesloLGS NF → … | 等宽 |
| `--ed-accent` | `#A34A52` / `#E0919A` | 强调色（胭脂） |
| `--radius-s/m/l` | 2 / 3 / 4px | 圆角几近归零 |
| `--line-width` | `42rem` | 阅读栏宽 |
| `--line-height-normal` | `1.8` | 正文行高 |

---

## 十一、图表配色（Mermaid / Markmap / Canvas）

图表不写死颜色，**源码里只声明语义 class，色值全交给 CSS**：

```mermaid
flowchart LR
    A["原始资料"] --> B["ingest 编译"]
    B --> C["wiki 知识库"]

    class A blue
    class B green
    class C cyan
```

可用语义 class：`blue` `cyan` `green` `yellow` `orange` `red` `purple`，以及 `solid`（实心强调，用于起点/终点/关键决策）。

> **不要写 `classDef xxx fill:var(--x)` 或 `fill:rgba(...)`** —— Mermaid 的 classDef 只接受简单色值，写变量或 rgba 会直接抛解析错误、整张图渲染失败。也**不要写 `style 节点 fill:#hex`**，那样会绕过主题、暗色下必然失配。

其余图表类型（时序图、思维导图、类图、状态图、ER 图、甘特图、饼图、旅程图、时间线、象限图、GitGraph、XY 图）以及 Canvas 白板、Markmap 思维导图的配色，都由 `07-diagrams.css` 统一挂在同一套色板上，无需逐个处理。

---

## 十二、文件清单

`.obsidian/snippets/` 下 10 个片段，按加载顺序编号：

| 文件 | 职责 |
|------|------|
| `01-foundation.css` | 色彩 / 字体 / 圆角 / 度量 token |
| `02-typography.css` | 标题层级、段落、列表、表格、引用、图片、分隔线 |
| `03-callouts.css` | Callout 语汇 + 多栏 / 画廊 / 浮动 / 边注 / 信息框 |
| `04-components.css` | 双链、外链、标签、代码、属性区、嵌入 |
| `05-layout.css` | 按笔记切换的版式模式 |
| `06-chrome.css` | 侧边栏、标签页、状态栏、悬浮预览、图谱、打印 |
| `07-diagrams.css` | 把图表 token（`--wiki-mmd-*` / `--wiki-mk-*` / `--wiki-cv-*`）接到编辑风色板 |
| `08-mermaid.css` | Mermaid 全图表类型样式（覆盖 12 类图） |
| `09-markmap.css` | Markmap 思维导图 |
| `10-canvas.css` | Canvas 白板 |

> `08` / `09` / `10` 内部 token 命名沿用 `--wiki-*`，由 `07` 统一重新赋值到编辑风色板 —— 图表层与编辑风完全解耦，升级 Mermaid / Markmap / Canvas 的样式时直接覆盖这三个文件即可，不用碰编辑风的任何一处。

另有一套 **Nord 冷色版**样式（`wiki-reading` / `wiki-callouts` / `wiki-components`）归档在 `.obsidian/snippets-legacy/`，扩展名为 `.css.disabled`。Obsidian 只加载 `snippets/` 目录下扩展名为 `.css` 的文件，所以它们不会生效。想换用冷色版：先把 `01`–`06` 移出 `snippets/`，再去掉那三个文件的 `.disabled` 后缀并移回 `snippets/`。
