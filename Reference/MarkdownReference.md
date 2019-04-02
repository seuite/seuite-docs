# Markdown For SEUITE

本文由 [**EncofComic**](https://github.com/encofcomic) 于 2019/3/20 编写完成，[**Sciroccogti**](https://github.com/Sciroccogti) 于 2019/3/29 翻译完成，[**EncofComic**](https://github.com/encofcomic) 于 2019/4/2 校对完成。

## 概览

**Markdown** 由 [Daring Fireball](http://daringfireball.net/) 设计而成；这里是[原指南](http://daringfireball.net/projects/markdown/syntax)。不过，各个编辑器和解析器的**Markdown**语法都有所不同。**SEUITE**选用 [GitHub Flavored Markdown][GFM] 为标准。

[TOC]

## 块元素

### 段落与换行符

Markdown 中，一个**段落**是指数行连续的文本，而空行被用来划分**段落**。然而在 SEUITE 里，你无需空行，直接换行即可划分出一个新的**段落**。

同时按下 `Shift` + `Return` 可以创建单个换行符，以实现换行而不分段。而在大多数其它的 markdown 解析器中，这种单个换行符会被忽略，你可以在行末空两格，或插入 `<br/>` 来实现换行而不分段。

### 标题

我们在行首使用1到6个 `#` 号来标记标题，依次对应1至6级标题。例如：

```markdown
# 这是1级标题

## 这是2级标题

###### 这是6级标题
```

输入 `#` 后接标题内容，并按下 `Return`，即可新建一个标题。

### 块引用

Markdown 使用电子邮件样式的 `>` 符来标记**块引用**。它们表示为：

```markdown
> 这是一个包含两段的块引用。 这是第一段。
>
> 这是第二段。Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.



> 这是另一个带有一个段落的块引用。 有三个空行分隔两个块引用
```

输入 `>` 后接你的引用内容将会生成一个引用块。若要在引用内嵌入另一个引用，只需输入两级 `>` 。

### 列表

输入 `* 列表项1` 将创建无序列表，其中 `*` 可以用 `+` 或 `-` 替换。

输入 `1. 列表项1` 将创建有序列表。它们的 markdown 代码如下：

```markdown
## 无序列表
*  红
*  绿
*  蓝

## 有序列表
1. 红
2. 绿
3. 蓝
```

### 任务列表

任务列表是有 `[ ]`（未完成）或 `[x]`（已完成）标记的列表。例如：

``` markdown
- [ ] 任务列表项
- [ ] 使用列表的语法
- [ ] 支持正常的**格式**，@提及，引用#1234 
- [ ] 未完成项
- [x] 已完成项
```

只需单击项目前的框即可更改*已完成/未完成*状态

### （围栏式）代码块

SEUITE 仅支持 [GitHub Flavored Markdown][GFM] 中的代码围栏，而不支持 markdown 中原生的代码块。

使用代码围栏非常简单：输入\`\`\`符并回车。可以在\`\`\`后写上语言标识符以开启语法高亮。

``` markdown
这是一个例子。
```

### 数学公式块

你可以用 **MathJax** 来渲染 *$L^AT_EX$*。

输入`$$`并回车来添加数学表达式，这将启用一个支持 *$TeX/L^AT_EX$* 的输入区。例如： 

$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$

在 markdown 代码中，数学公式块由一对`$$`标记：

``` markdown
$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$
```

你的编辑器可能需要启用一些插件来正确渲染该组件。

### 表格

输入 `| 标题一  | 标题二 |` 并按 `Return` 键将会新建一个两列的表格。

在表格被创建后，将光标移至表格上会打开表格工具栏，你可以在其中调整表格，对齐或删除表格。你也可以用内容菜单来复制和添加。删除单个列/行。

表格的完整语法如下所示，不过由于 SEUITE 将会自动生成表格的 markdown 代码，你无需理解代码的全部细节。

在markdown源代码中，它们像这样：

``` markdown
|   标题一   |  标题二   |
| --------- | --------- |
| 单元格内容 | 单元格内容 |
| 单元格内容 | 单元格内容 |
```

你还可以在表格中使用行内的 markdown ，诸如链接、粗体、斜体或删除线。

还有，通过在标题行中使用`:`，可以设定该列的对齐方式：左对齐，右对齐，或居中：

``` markdown
|  左对齐  |    居中    | 右对齐 |
| :------ |:----------:| -----:|
| 第三栏是 | 啰嗦的文字~ | $1600 |
| 第二栏是 | 中心格      |   $12 |
| 斑马条纹 | 很整洁呢    |    $1 |
```

最左侧的冒号表示左对齐的列; 最右侧的冒号表示右对齐的列; 两边都有一个冒号表示居中的列。

### Footnotes

``` markdown
你可以像这样创建脚注[^脚注]。

[^脚注]：这是**脚注**的*文本*。
```

将生成：

你可以像这样创建脚注[^脚注]。
[ ^脚注 ]：这是**脚注**的*文本*。

将鼠标悬停在“脚注”上标上可查看脚注的内容。

### 分割线

在空行上输入`***`或`---`并按`Return`将会绘制一条分割线：

---

### 目录 (TOC)

输入 `[toc]` 并按 `Return` 键将会生成一个“目录”块，它将提取全文的所有标题，并且能够自动更新。 

## Span 元素

Span 元素将在输入后即刻解析并呈现。当光标移至这些 span 元素上时将会把它们展开为 markdown 源码。以下是各个 span 元素的语法解释。

### 链接

Markdown支持两种链接样式：内联和参考。

在这两种样式中，链接文本都由[方括号]分隔。

要创建内联链接，请在链接文本的结束方括号后紧跟一组普通括号，并将你想要链接指向的URL，以及链接的可选标题放在括号内。例如：

``` markdown
这是[示例](http://example.com/ "标题")内联链接。

[该链接](http://example.net/) 没有标题属性。
```

会生成：

这是[示例](http://example.com/ "标题")内联链接。(`<p>示例 <a href="http://example.com/" title="标题">`)

[该链接](http://example.net/) 没有标题属性。(`<p><a href="http://example.net/">该链接</a>没有`)

#### 页内跳转链接

**你可以将跳转目标指向标题**, 这将创建一个书签，允许你在单击后跳转到该部分。例如：

按住`Ctrl`(在Mac上：`⌘`)的同时单击[此链接](#块元素)将会跳转至标题`块元素`。

#### 参考链接

参考样式链接使用第二组方括号，在其中放置你选择的标签以标识链接：

``` markdown
这是[一个示例][id]参考样式链接
```

随后，在文档中的任一位置，你可以单独在一行上定义链接标签，如下所示：

```markdown
[id]: http://example.com/  "可选标题"
```

在SEUITE中，它们将被渲染为：

这是[一个示例][id]参考样式链接

[id]: http://example.com/  "可选标题"

隐式链接名称快捷方式允许你省略链接的名称，在这种情况下，链接文本本身将用作名称。只需使用一组空的方括号——例如，将“Google”一词链接到 google.com 网站，可以简写为：

``` markdown
[Google][]
```

随后定义链接：

```markdown
[Google]: http://google.com/
```

在SEUITE中，单击该链接将展开它以进行编辑，同时，`⌘`+单击将在Web浏览器中打开超链接。

### 网址

SEUITE允许你将URL作为链接插入，由 <尖括号> 包围。

`<i@SEUITE.io>` 显示为<i@SEUITE.io>。

SEUITE还会自动链接标准网址。 例如： www.google.com 。

### 图片

图像具有与链接类似的语法，但它们在链接前需要额外的`！`。插入图像的语法如下所示：

``` markdown
![替代文字](/path/to/img.jpg)

![替代文字](/path/to/img.jpg "可选标题")
```

你可以使用拖放操作来从图像文件或Web浏览器插入图像。你可以通过单击图片来修改 markdown 源代码。如果使用拖放操作添加的图像与你当前编辑的文档位于同一目录或子目录中，则将使用相对路径。

如果你使用 markdown 搭建网站，你可能需要在头信息中用参数`SEUITE-root-url`为你的本地预览指定一个 URL 前缀。例如，在头信息中输入`SEUITE-root-url:/User/Abner/Website/SEUITE.io/`，然后在 SEUITE 中`![alt](/blog/img/test.png)`将会被当作`![alt](file:///User/Abner/Website/SEUITE.io/blog/img/test.png)。

更多详情请见[此处](https://support.SEUITE.io/Images/).

### 强调

Markdown 把星号(`*`)以及下划线(`_`)作为强调的标记。被一对`*` `_`包围的文本在编译时会由HTML 标记`<em>`包围例如：

``` markdown
*单对星号*

_单对下划线_
```

生成：

*单对星号*

_单对下划线_

GFM会忽略代码和名称单词中常见的下划线，像这样：
> wow_great_stuff
>
> do_this_and_do_that_and_another_thing.

使用反斜杠来避免星号或下划线被编译为强调标记：

``` markdown
\*本文本被一对可见星号包围\*
```

SEUITE 推荐使用`*`作为强调标记。

### 加粗

一对双 `*` 或 `_` 会使得它们包围的内容在编译时由HTML标签 `<strong>` 标记，例如：

``` markdown
**双星号**

__双下划线__
```

output:

**双星号**

__双下划线__

SEUITE推荐使用 `**` 作为加粗标记。

### 代码

用一对 ` 包围**行内代码**来显示它。与预格式化的代码块不同，行内代码不会分段。例如：

``` markdown
Use the `printf()` function
```

将生成：

Use the `printf()` function

### 删除线

GFM 加入了用来显示删除线的语法，而原生 markdown 并没有。

`~~Mistaken text.~~` 显示为~~Mistaken text.~~

### 下划线

下划线由原始 HTML 实现。

`<u>Underline</u>` 显示为<u>Underline</u>

### 表情符号 :smile:

用 `:emoji:` 来输入表情符号

同时，也支持直接输入 UTF-8 的表情符号，请参考 [Emoji 表情符号大全](/reference/emojireference)。

### 行内数学公式

用 `$` 来包围 TeX 代码。例如：`$\lim_{x \to \infty} \exp(-x) = 0$` 会渲染为$\lim_{x \to \infty} \exp(-x) = 0$

要开启行内数学公式的行内预览，请输入 `$` 后按 `ESC`，再输入 TeX代码。

更多详情请见[此处](http://support.SEUITE.io/Math/).

## HTML

你可以使用 HTML 来实现纯 markdown 不支持的格式。例如，使用 `<span style="color:red">this text is red</span>` 来添加红字。

### 嵌入内容

有些网站提供基于iframe的嵌入代码，你也可以将其粘贴到SEUITE中。 例如：

```Markdown
<iframe height='265' scrolling='no' title='Fancy Animated SVG Menu' src='http://codepen.io/jeangontijo/embed/OxVywj/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'></iframe>
```

### 视频

你可以使用`<video>` HTML 标签来嵌入视频。例如：

```Markdown
<video src="xxx.mp4" />
```

### 其它HTML支持：

更多详情请见[此处](http://support.typora.io/HTML/).

[GFM]: https://help.github.com/articles/github-flavored-markdown/