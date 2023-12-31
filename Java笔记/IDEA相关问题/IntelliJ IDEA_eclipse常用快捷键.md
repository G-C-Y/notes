### IntelliJ IDEA/eclipse常用快捷键
#### 快速跳转到实现类：Ctrl + Alt + 鼠标左键
#### 查找：Ctrl + F
使用 Ctrl + F 快捷键，可以看到单词出现的次数。如下图
![image.png](https://images.cherryfloris.eu.org/2021/1628666575881-c1a3622a-676c-487e-b0cf-8215a81c8731.png)
#### 替换Ctrl + r
场景：在某一个类中，当想知道某个单词都出现在什么地方时，或者你发像某一个变量名字写错了，但已经有很多了，想要批量替换。
当我们想要批量修改这两个变量名的时候，当搜索到后，点击下图中的按钮后，就可以同时操作所有的name
![image.png](https://images.cherryfloris.eu.org/2021/1628666628147-bbf04293-53a3-40f2-8381-f9086b369633.png)

注意
注意一：这是模糊查询，会把所有name以及包含name的都找到,所以在批量替换的时候要小心。
如下图，点完操作所有后，会同时修改这四处的name，显然 name_LiSi中的name是不应该被修改的
![image.png](https://images.cherryfloris.eu.org/2021/1628666642875-5768f41d-c330-43f0-abaf-341e6b03fab9.png)
注意二：对变量名或者是方法名的修改，只是在当前类中修改了。 如果其他类也用到了被修改的变量名或者方法名，那么在当前类中修改后，也要去其他类中再次修改。
#### 全局替换Ctrl + shift + r
#### 查看实现类和接口：Ctrl + H
使用方法：比如ApplicationContext，把光标放在上边，按 Ctrl+H ，就可以看到它的与它有关的类和接口。
![image.png](https://images.cherryfloris.eu.org/2021/1628666657292-43c7f229-1524-4992-b9eb-001be77187c6.png)
#### new对象快捷键 ：Alt + Enter
例如：我们new对象 User user = new User(); 全写很麻烦。
使用方法： 我们先写 new User()，然后使用 Alt + Enter快捷键，再按enter就可以了。
也可以这样写：写完 new User() ，然后写.var，再按enter也可以补全。
#### 代码自动对齐：Ctrl+Alt+L
例如：我们写的代码有的空格太多，什么的。
使用方法： 可以直接在当前类中全部使用，也可以选中一部分使用。
#### 整个项目查找：双击Shift
如果我们想要查找某个类，直接双击Shift，输入后选择后，按enter进入。
#### 直接换行：Shift+Enter
假如我们在一行代码的中间，想要换行，可以使用这个快捷键。
#### 复制当前行：Ctrl + D

### eclipse常用快捷键
#### eclipse切换背景主题
Window –> Preferences –> General –>Appearance –> Theme。直接换到“Dark”主题就行。
#### 自动补全 Alt+ /
例如：输入syso+快捷键+enter即出现System.out.println();
    输入main+快捷键+enter即出现	public static void main(String[] args) {	}
#### 复制一行Ctrl+Alt+↑
**1几个最重要的快捷键**
代码助手:Ctrl+Space（简体中文操作系统是Alt+/）
快速修正：Ctrl+1
单词补全：Alt+/
打开外部Java文档：Shift+F2

显示搜索对话框：Ctrl+H
快速Outline：Ctrl+O
打开资源：Ctrl+Shift+R
打开类型：Ctrl+Shift+T
显示重构菜单：Alt+Shift+T
上一个/下一个光标的位置：Alt+Left/Right 
上一个/下一个成员（成员对象或成员函数）：Ctrl+Shift+Up/Down
选中闭合元素：Alt+Shift+Up/Down/Left/Right
删除行：Ctrl+D
在当前行上插入一行：Ctrl+Shift+Enter
在当前行下插入一行： Shift+Enter
上下移动选中的行：Alt+Up/Down

组织导入：Ctrl+Shift+O

**2 定位** 
**2.1行内定位** 
行末/行首：End/Home
前一个/后一个单词：Ctrl+Right/Left
**2.2文件内定位** 
跳到某行：Ctrl+L
上下滚屏：Ctrl+Up/Down
上一个/下一个成员（成员对象或成员函数）：Ctrl+Shift+Up/Down
快速Outline：Ctrl+O 
**2.3跨文件定位** 
打开声明：F3
打开资源：Ctrl+Shift+R
打开类型：Ctrl+Shift+T
在workspace中搜索选中元素的声明：Ctrl+G
在workspace中搜索选中的文本：Ctrl+Alt+G
在workspace中搜索选中元素的引用：Ctrl+Shift+G
打开调用层次结构：Ctrl+Alt+H
快速层次结构：Ctrl+T
反悔：Ctrl+Z
**2.4其它** 
上一个/下一个光标所在位置：Alt+Left/Right
上一个编辑的位置：Ctrl+Q 

**3 选中** 
**3.1行内选中** 
选中到行末/行首：Shift+End/Home
选中上一个/下一个单词：Ctrl+Shift+Left/Right
**3.2文件内选中** 
选中闭合元素：Alt+Shift+Up
恢复到上一个选中：Alt+Shift+Down
选中下一个/上一个元素：Alt+Shift+Right/Left 

**4 定位/选中/操作同时** 
删除行：Ctrl+D
删除下一个/上一个单词：Ctrl+Delete/Backspace
删除到行末：Ctrl+Shift+Delete
在当前行上插入一行：Ctrl+Shift+Enter
在当前行下插入一行： Shift+Enter
上下移动选中的行：Alt+Up/Down
拷贝选中的行：Ctrl+Alt+Up/Down 

**5其它的代码编辑类快捷键** 
保存：Ctrl+S
保存所有：Ctrl+Shift+S
下一个命中的项（搜索之后）：Ctrl+.
注释：Ctrl+/
添加导入：Ctrl+Shift+M
显示快捷键帮助：Ctrl+Shift+L
变为大/小写：Ctrl+Shift+X/Y

**6 重构** 
显示重构菜单：Alt+Shift+T
重构-改变方法签名：Alt+Shift+C
重构-移动：Alt+Shift+V
重构-重命名：Alt+Shift+R 

**7 编辑器、视图、透视图切换** 
下一个编辑器：Ctrl+F6
下一个视图：Ctrl+F7
下一个透视图：Ctrl+F8
最大化当前视图或编辑器：Ctrl+M
激活编辑器：F12 

**8 Debug** 
F5：Step Into（debug）
F6：Step over（debug）
F7：Step return（debug）
F8：Resume（debug）
F11：debug上一个应用（debug） 

**9 Up/Down/Right/Left类快捷键** 
Ctrl
前一个/后一个单词：Ctrl+Right/Left
上下滚屏：Ctrl+Up/Down
Alt
上一个/下一个光标的位置：Alt+Left/Right
上下移动选中的行：Alt+Up/Down
Shift
选中上一个/下一个字符：Shift+Left/Right
选中上一行/下一行（从当前光标位置开始）：Shift+Up/Down
Ctrl+Shift
上一个/下一个成员（成员对象或成员函数）：Ctrl+Shift+Up/Down
选中上一个/下一个单词：Ctrl+Shift+Left/Right
Alt+Shift
选中闭合元素：Alt+Shift+Up
恢复到上一个选中：Alt+Shift+Down
选中下一个/上一个元素：Alt+Shift+Right/Left
拷贝选中的行：Ctrl+Alt+Up/Down
Ctrl+Alt
拷贝选中的行：Ctrl+Alt+Up/Down 

**10 F类快捷键** 
F2：显示提示/重命名
F3：打开选中元素的声明
F4：打开选中元素的类型继承结构
F5：刷新
F5：Step Into（debug）
F6：Step over（debug）
F7：Step return（debug）
F8：Resume（debug）
F11：debug上一个应用（debug）
F12：激活编辑器

Ctrl+1 快速修复(最经典的快捷键,就不用多说了)
Ctrl+D: 删除当前行 
Ctrl+Alt+↓ 复制当前行到下一行(复制增加)
Ctrl+Alt+↑ 复制当前行到上一行(复制增加)
Alt+↓ 当前行和下面一行交互位置(特别实用,可以省去先剪切,再粘贴了)
Alt+↑ 当前行和上面一行交互位置(同上)
Alt+← 前一个编辑的页面
Alt+→ 下一个编辑的页面(当然是针对上面那条来说了)
Alt+Enter 显示当前选择资源(工程,or 文件 or文件)的属性
Shift+Enter 在当前行的下一行插入空行(这时鼠标可以在当前行的任一位置,不一定是最后)
Shift+Ctrl+Enter 在当前行插入空行(原理同上条)
Ctrl+Q 定位到最后编辑的地方
Ctrl+L 定位在某行 (对于程序超过100的人就有福音了)
Ctrl+M 最大化当前的Edit或View (再按则反之)
Ctrl+/ 注释当前行,再按则取消注释
Ctrl+O 快速显示 OutLine
Ctrl+T 快速显示当前类的继承结构
Ctrl+W 关闭当前Editer
Ctrl+K 参照选中的Word快速定位到下一个
Ctrl+E 快速显示当前Editer的下拉列表(如果当前页面没有显示的用黑体表示)
Ctrl+/(小键盘) 折叠当前类中的所有代码
Ctrl+×(小键盘) 展开当前类中的所有代码
Ctrl+Space 代码助手完成一些代码的插入(但一般和输入法有冲突,可以修改输入法的热键,也可以暂用Alt+/来代替)
Ctrl+Shift+E 显示管理当前打开的所有的View的管理器(可以选择关闭,激活等操作)
Ctrl+J 正向增量查找(按下Ctrl+J后,你所输入的每个字母编辑器都提供快速匹配定位到某个单词,如果没有,则在stutes line中显示没有找到了,查一个单词时,特别实用,这个功能Idea两年前就有了)
Ctrl+Shift+J 反向增量查找(和上条相同,只不过是从后往前查)
Ctrl+Shift+F4 关闭所有打开的Editer
Ctrl+Shift+X 把当前选中的文本全部变味小写
Ctrl+Shift+Y 把当前选中的文本全部变为小写
Ctrl+Shift+F 格式化当前代码
Ctrl+Shift+P 定位到对于的匹配符(譬如{}) (从前面定位后面时,光标要在匹配符里面,后面到前面,则反之)

下面的快捷键是重构里面常用的,本人就自己喜欢且常用的整理一下(注:一般重构的快捷键都是Alt+Shift开头的了)
Alt+Shift+R 重命名 (是我自己最爱用的一个了,尤其是变量和类的Rename,比手工方法能节省很多劳动力)
Alt+Shift+M 抽取方法 (这是重构里面最常用的方法之一了,尤其是对一大堆泥团代码有用)
Alt+Shift+C 修改函数结构(比较实用,有N个函数调用了这个方法,修改一次搞定)
Alt+Shift+L 抽取本地变量( 可以直接把一些魔法数字和字符串抽取成一个变量,尤其是多处调用的时候)
Alt+Shift+F 把Class中的local变量变为field变量 (比较实用的功能)
Alt+Shift+I 合并变量(可能这样说有点不妥Inline)
Alt+Shift+V 移动函数和变量(不怎么常用)
Alt+Shift+Z 重构的后悔药(Undo)

编辑
作用域 功能 快捷键 
全局 查找并替换 Ctrl+F 
文本编辑器 查找上一个 Ctrl+Shift+K 
文本编辑器 查找下一个 Ctrl+K 
全局 撤销 Ctrl+Z 
全局 复制 Ctrl+C 
全局 恢复上一个选择 Alt+Shift+↓ 
全局 剪切 Ctrl+X 
全局 快速修正 Ctrl1+1 
全局 内容辅助 Alt+/ 
全局 全部选中 Ctrl+A 
全局 删除 Delete 
全局 上下文信息 Alt+？
Alt+Shift+?
Ctrl+Shift+Space 
Java编辑器 显示工具提示描述 F2 
Java编辑器 选择封装元素 Alt+Shift+↑ 
Java编辑器 选择上一个元素 Alt+Shift+← 
Java编辑器 选择下一个元素 Alt+Shift+→ 
文本编辑器 增量查找 Ctrl+J 
文本编辑器 增量逆向查找 Ctrl+Shift+J 
全局 粘贴 Ctrl+V 
全局 重做 Ctrl+Y 

 
查看
作用域 功能 快捷键 
全局 放大 Ctrl+= 
全局 缩小 Ctrl+- 

 
窗口
作用域 功能 快捷键 
全局 激活编辑器 F12 
全局 切换编辑器 Ctrl+Shift+W 
全局 上一个编辑器 Ctrl+Shift+F6 
全局 上一个视图 Ctrl+Shift+F7 
全局 上一个透视图 Ctrl+Shift+F8 
全局 下一个编辑器 Ctrl+F6 
全局 下一个视图 Ctrl+F7 
全局 下一个透视图 Ctrl+F8 
文本编辑器 显示标尺上下文菜单 Ctrl+W 
全局 显示视图菜单 Ctrl+F10 
全局 显示系统菜单 Alt+- 

 
导航
作用域 功能 快捷键 
Java编辑器 打开结构 Ctrl+F3 
全局 打开类型 Ctrl+Shift+T 
全局 打开类型层次结构 F4 
全局 打开声明 F3 
全局 打开外部javadoc Shift+F2 
全局 打开资源 Ctrl+Shift+R 
全局 后退历史记录 Alt+← 
全局 前进历史记录 Alt+→ 
全局 上一个 Ctrl+, 
全局 下一个 Ctrl+. 
Java编辑器 显示大纲 Ctrl+O 
全局 在层次结构中打开类型 Ctrl+Shift+H 
全局 转至匹配的括号 Ctrl+Shift+P 
全局 转至上一个编辑位置 Ctrl+Q 
Java编辑器 转至上一个成员 Ctrl+Shift+↑ 
Java编辑器 转至下一个成员 Ctrl+Shift+↓ 
文本编辑器 转至行 Ctrl+L 

 
搜索
作用域 功能 快捷键 
全局 出现在文件中 Ctrl+Shift+U 
全局 打开搜索对话框 Ctrl+H 
全局 工作区中的声明 Ctrl+G 
全局 工作区中的引用 Ctrl+Shift+G 

 
文本编辑
作用域 功能 快捷键 
文本编辑器 改写切换 Insert 
文本编辑器 上滚行 Ctrl+↑ 
文本编辑器 下滚行 Ctrl+↓ 

 
文件
作用域 功能 快捷键 
全局 保存 Ctrl+X 
Ctrl+S 
全局 打印 Ctrl+P 
全局 关闭 Ctrl+F4 
全局 全部保存 Ctrl+Shift+S 
全局 全部关闭 Ctrl+Shift+F4 
全局 属性 Alt+Enter 
全局 新建 Ctrl+N 

 
项目
作用域 功能 快捷键 
全局 全部构建 Ctrl+B 

 
源代码
作用域 功能 快捷键 
Java编辑器 格式化 Ctrl+Shift+F 
Java编辑器 取消注释 Ctrl+\ 
Java编辑器 注释 Ctrl+/ 
Java编辑器 添加导入 Ctrl+Shift+M 
Java编辑器 组织导入 Ctrl+Shift+O 
Java编辑器 使用try/catch块来包围 未设置，太常用了，所以在这里列出,建议自己设置。
也可以使用Ctrl+1自动修正。 

 
运行
作用域 功能 快捷键 
全局 单步返回 F7 
全局 单步跳过 F6 
全局 单步跳入 F5 
全局 单步跳入选择 Ctrl+F5 
全局 调试上次启动 F11 
全局 继续 F8 
全局 使用过滤器单步执行 Shift+F5 
全局 添加/去除断点 Ctrl+Shift+B 
全局 显示 Ctrl+D 
全局 运行上次启动 Ctrl+F11 
全局 运行至行 Ctrl+R 
全局 执行 Ctrl+U 

 
重构
作用域 功能 快捷键 
全局 撤销重构 Alt+Shift+Z 
全局 抽取方法 Alt+Shift+M 
全局 抽取局部变量 Alt+Shift+L 
全局 内联 Alt+Shift+I 
全局 移动 Alt+Shift+V 
全局 重命名 Alt+Shift+R 
全局 重做 Alt+Shift+Y
# **eclipse快捷键以及使用技巧大全**
1. 打开MyEclipse 6.0.1,然后“window”→“Preferences”
2. 选择“java”,展开,“Editor”,选择“Content Assist”。
3. 选择“Content Assist”,然后看到右边,右边的“Auto-Activation”下面的“AutoActivation triggers for java”这个选项。其实就是指触发代码提示的就是“.”这个符号。
4.“Auto Activation triggers for java”这个选项,在“.”后加abc字母,方便后面的查找修改。然后“apply”,点击“OK”。
5. 然后,“File”→“Export”,在弹出的窗口中选择“Perferences”,点击“下一步”。
6. 选择导出文件路径,本人导出到桌面,输入“test”作为文件名,点击“保存”。
7. 在桌面找到刚在保存的文件“test.epf”,右键选择“用记事本打开”。
8. 可以看到很多配置MyEclipse 6.0.1的信息
9. 按“ctrl + F”快捷键,输入“.abc”,点击“查找下一个”。
10. 查找到“.abc”的配置信息如下:
11. 把“.abc”改成“.abcdefghijklmnopqrstuvwxyz(,”,保存,关闭“test.epf”。
12. 回到MyEclipse 6.0.1界面,“File”→“Import”,在弹出的窗口中选择“Perferences”,点击“下一步”,选择刚在已经修改的“test.epf”文件,点击“打 开”,点击“Finish”。该步骤和上面的导出步骤类似。
13. 最后当然是进行代码测试了。随便新建一个工程,新建一个类。在代码输入switch,foreach等进行测试。你立即会发现,果然出了提示,而且无论是敲哪个字母都会有很多相关的提示了,很流畅,很方便。
**总结:**
“Auto Activation triggers for java”这个选项就是指触发代码提示的的选项,把“.”改成
“.abcdefghijklmnopqrstuvwxyz(,”的意思,就是指遇到26个字母和.,(这些符号就触发代码提示功能了。
顺便说一下,修改类名,接口名等以不同颜色高亮的,可以这样配置在“java”→“enditor”→“syntac”,右边展开“java”→“classes”,勾上“Enable”这个选项,选择自己喜欢的颜色即可。
当然还有其他相关的颜色配置。具体就不说啦。其实,在“Preferences”这个东西,有很多可以配置的东西,使得MyEclipse 优化的,具体的就要各个人根据自己个人喜好去配置了。
