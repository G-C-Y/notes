## [Typora编写MarkDown的技巧.md](https://www.yuque.com/attachments/yuque/0/2021/md/21372399/1629969780806-562ea4bb-9fea-417e-8e4b-a5eaa8642039.md?_lake_card=%7B%22src%22%3A%22https%3A%2F%2Fwww.yuque.com%2Fattachments%2Fyuque%2F0%2F2021%2Fmd%2F21372399%2F1629969780806-562ea4bb-9fea-417e-8e4b-a5eaa8642039.md%22%2C%22name%22%3A%22Typora%E7%BC%96%E5%86%99MarkDown%E7%9A%84%E6%8A%80%E5%B7%A7.md%22%2C%22size%22%3A7868%2C%22type%22%3A%22%22%2C%22ext%22%3A%22md%22%2C%22status%22%3A%22done%22%2C%22taskId%22%3A%22u51ec9854-8cc7-4042-bd4f-fc7d7d5750d%22%2C%22taskType%22%3A%22upload%22%2C%22id%22%3A%22u2f41ff36%22%2C%22card%22%3A%22file%22%7D)
## 简介
### MarkDown
Markdown 是一种轻量级标记语言，它允许人们使用**易读易写**的纯文本格式编写文档。它看来更为简明、不易出错且易扩展。而且，它很容易做到只用键盘编辑（这对于不间断的打字有帮助）。Markdown非常适合**大量文本的写作或技术性的文章**，并且只需要很少的时间即可学习。
### Typora
Typora是一款轻量级Markdown编辑器，适用于macOS、Windows和Linux三种操作系统，是一款**免费**软件。与其他Markdown编辑器不同的是，Typora没有采用源代码和预览双栏显示的方式，而是采用所见即所得的编辑方式，实现了即时预览的功能，但也可切换至源代码编辑模式。

- Typora删除了预览窗口，以及所有其他不必要的干扰，取而代之的是实时预览。
- Markdown的语法因不同的解析器或编辑器而异，Typora使用的是[GitHub Flavored Markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/)。
### 下载地址
Typora下载地址：[https://www.typora.io/#windows](https://www.typora.io/#windows)
## 1.Typora常用快捷键

- 加粗： Ctrl/Cmd + B
- 标题： Ctrl/Cmd + H
- 插入链接： Ctrl/Cmd + K
- 插入代码： Ctrl/Cmd + Shift + C
- 行内代码： Ctrl/Cmd + Shift + K
- 插入图片： Ctrl/Cmd + Shift + I
- 无序列表： Ctrl/Cmd + Shift + L
- 撤销： Ctrl/Cmd + Z
- 一级标题：快捷键为Crtl + 1，多级标题以此类推
- 切换原文和语法：Ctrl/Cmd + /
## 2.块元素
### 换行符
在markdown中，段落由多个空格分隔。在Typora中，只需回车即可创建新段落。
### 标题级别
# 一级标题 快捷键为 Ctrl + 1## 二级标题 快捷键为 Ctrl + 2......###### 六级标题 快捷键为 Ctrl + 6
### 引用文字
> + 空格 + 引用文字
引用效果
### 无序列表
使用 * + - 都可以创建一个无序列表

- AAA
- BBB
- CCC
### 有序列表
使用 ‘1.’+‘空格’ 2. 3. 创建有序列表
写法：1. AAA

1. AAA
2. BBB
3. CCC
### 任务列表
- [ ] 不勾选
- [x] 勾选

- 不勾选
- 勾选
### 代码块
在Typora中插入程序代码的方式有两种：使用反引号 `（~ 键）、使用缩进（Tab）。

- 插入行内代码，即插入一个单词或者一句代码的情况，使用 code 这样的形式插入。
- 插入多行代码输入3个反引号（`） + 回车，并在后面选择一个语言名称即可实现语法高亮。

java
public class Hello{ public static void main(String[] args) { System.out.println("hello!"); } }
python
def helloWorld(): print("hello, world!")
### 数学表达式
当你需要在编辑器中插入数学公式时，可以使用两个美元符 $$ 包裹 TeX 或 LaTeX 格式的数学公式来实现。根据需要加载 Mathjax 对数学公式进行渲染。 
按下 $$，然后按下回车键，即可进行数学公式的编辑。
$$ \mathbf{V}_1\times\mathbf{V}_2 = \mathbf{X}_3 $$


### 插入表格
输入 | id | name | number |并回车。即可创建一个列表；快捷键 Ctrl + T弹出对话框；也可直接复制表粘贴进来。

| id | name | number |
| --- | --- | --- |
| 1 | kxds | 101 |

### 脚注
[^1]:脚注内容
你可以创建一个脚注，像这样1.
 [ **1**]  脚注内容
注意：该例子脚注标识是1，脚注标识可以为字母数字下划线，但是暂不支持中文。脚注内容可为任意字符，包括中文。
### 分割线
输入 *** 或者 --- 再按回车即可绘制一条水平线，如下：

---

### 目录（TOC）
输入 [toc] 然后回车，即可创建一个“目录”。TOC从文档中提取所有标题，其内容将自动更新。
Typora支持TOC自动生成目录
[toc]
## 3.跨度元素
跨度元素即图片，网址，视频等，在Typora中输入后，会立即载入并呈现。
### 链接
这是一个带有标题属性的 [链接]([https://www.typora.io/](https://www.typora.io/) "标题")这是一个没有标题属性的 [链接][https://www.typora.io/](https://www.typora.io/))
这是一个带有标题属性的[链接](https://www.typora.io/).这是一个没有标题属性的[链接](https://www.typora.io/).
**注：ctrl+鼠标右键访问链接**
### 网址
Typora允许用<括号括起来>, 把URL作为链接插入。
百度：<www.baidu.com>
百度：[www.baidu.com](http://eip.teamshub.com/www.baidu.com)
### 图片
![显示的文字](C:\Users\Hider\Desktop\echart.png) ![显示的文字](C:\Users\Hider\Desktop\echart.png “图片标题”)
除了以上2种方式之外，还可以直接将图片拖拽进来，自动生成链接。
### 斜体
使用 *单个星号* 或者 _单下划线_ 可以字体倾斜。快捷键 Ctrl + I
_斜体_
### 加粗
使用 **两个星号** 或者 __两个下划线__ 可以字体加粗。快捷键 Ctrl + B
**加粗**
### 加粗斜体
使用***加粗斜体***可以加粗斜体。
**_加粗斜体_**
### 代码标记
标记代码使用大于符。
>使用该 printf()功能
使用该 printf()功能
### 删除线
使用~~删除线~~ 快捷键 Alt + Shift + 5
~~删除线~~
~~删除线~~
### 下划线
\下划线 -- 无法执行
参考另一篇文章，可执行。
通过<u>下划线的内容</u> 或者 快捷键Ctrl + U可实现下划线
下划线的内容
### 表情符号
Github的Markdown语法支持添加emoji表情，输入不同的符号码（两个冒号包围的字符）可以显示出不同的表情。
:smile
### 下标
H~2~O (需在设置中打开该功能)
H2O
可以使用 <sub>文本</sub>实现下标。
H<sub>2</sub>O
H2O
### 上标
X^2^(需在设置中打开该功能)
X2
可以使用<sup>文本</sup>实现上标。
X<sup>2</sup>
X2
### 高亮
==高亮==(需在设置中打开该功能)
我是最重要的
### 文本居中
使用 <center>这是要居中的内容</center>可以使文本居中
这是要居中的文本内容
### 转义
Markdown 使用了很多特殊符号来表示特定的意义，如果需要显示特定的符号则需要使用转义字符，Markdown 使用反斜杠转义特殊字符：
**文本加粗**** 正常显示星号 **
Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：
\ 反斜线 ` 反引号 * 星号 _ 下划线 {} 花括号 [] 方括号 () 小括号 **# 井字号** + 加号 - 减号 . 英文句点 ! 感叹号
## 4.HTML
支持HTML
不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。
目前支持的 HTML 元素有：<kbd> <b> <i> <em> <sup> <sub> <br>等 ，如：
使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑 <kbd> </kbd> -- 白色框框
效果：使用 Ctrl+Alt+Del 重启电脑
 -- 白色框框
### 嵌入内容
支持iframe-based嵌入代码
<iframe src="//www.runoob.com"></iframe>
#### 视频
< video src=”[https://typora.io/img/beta.mp4](https://typora.io/img/beta.mp4)” />
## 5.参考
参考链接1：[Typora入门（中文版）](https://www.simon96.online/2018/10/18/Typora%E5%85%A5%E9%97%A8%EF%BC%88%E4%B8%AD%E6%96%87%E7%89%88%EF%BC%89/)
