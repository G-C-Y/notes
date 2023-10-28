PuTTY 作为免费且开源的老牌 SSH 客户端，经常用于 Windows 下连接管理远程服务器。为方便刚接触 VPS 的新手参考使用，本文配合截图介绍 PuTTY 的基础用法及一些设置技巧。
## PuTTY 下载及相关工具包
SSH 客户端这类涉及服务器登录和通信的软件，建议大家尽量用原版（曾有汉化版被曝存在安全后门），PuTTY 官方下载地址 [https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
在下载页提供有集成 PuTTY 及相关工具的完整安装包，也可以视需求单独下载某个程序使用。

| putty.exe | SSH 和 Telnet 客户端（最常使用的） |
| --- | --- |
| pscp.exe | SCP 客户端，命令行下通过 SSH 远程拷贝文件 |
| psftp.exe | SFTP 客户端，命令行下的文件传输会话 |
| puttytel.exe | 一个单纯 Telnet 客户端 |
| plink.exe | PuTTY 后端的命令行工具 |
| pageant.exe | PuTTY、PSCP、Plink 的 SSH 认证代理 |
| puttygen.exe | RSA、DSA、ECDSA 和 EdDSA 密钥生成工具 |

## PuTTY 创建 SSH 会话连接
运行 putty.exe，在程序界面内输入服务器 IP 地址和端口（22 是 SSH 默认端口），选中 SSH 连接类型，设置连接会话名称及点击保存，然后点击 Open 按钮开始连接登录。
[![](https://images.cherryfloris.eu.org/2021/1627027056946-b9483176-72d9-4b3a-878b-da1972e9e140.png)](https://www.hostarr.com/wp-content/uploads/putty-tutorial-1.png)
首次连接会提示服务器指纹，选择是或否。“是”将保存指纹，“否”则不保存。保存后登录同一台服务器将不再提示（如果提示，则表示服务器指纹发生了变化，可能是重装系统所致或连接服务器被冒充）。
[![](https://images.cherryfloris.eu.org/2021/1627027057253-55bffe24-06cf-4d56-84f5-ffd8899c1ff7.png)](https://www.hostarr.com/wp-content/uploads/putty-tutorial-2.png)
之后输入用户名和密码即可登录服务器（输入密码时不会显示输入状态，这是一个安全设计。鼠标右键点击可以粘贴输入）。
[![](https://images.cherryfloris.eu.org/2021/1627027057195-47afb207-f073-43ae-8c71-00a4ced5417b.png)](https://www.hostarr.com/wp-content/uploads/putty-tutorial-3.png)
如果需要注销连接会话，使用 exit 命令或 Ctrl+d 快捷键。
## PuTTY 修改保存设置
估计不少人遇到过这个问题，不知道怎么保存 PuTTY 设置。正确方法是先选中 SSH 会话，然后点击 Load 加载设置，这时就可以开始修改设置，之后点击保存会话设置。
如果需要修改 PuTTY 默认设置，就选中修改 Default Setting 会话。
[![](https://images.cherryfloris.eu.org/2021/1627027057169-007925ee-b2f7-4af9-b932-153639a71ac3.png)](https://www.hostarr.com/wp-content/uploads/putty-tutorial-4.png)
## PuTTY 会话保持时间
当与服务器长时间没数据传输，PuTTY 会自动断开连接。要避免该问题，可以在 Connection 选项 Seconds between keepalives 里开启会话保持功能（非 0 即开启，建议设置 300，单位秒）。
[![](https://images.cherryfloris.eu.org/2021/1627027056895-0a82041b-c8f6-46aa-a7d2-e3f33a68690f.png)](https://www.hostarr.com/wp-content/uploads/putty-tutorial-5.png)
## PuTTY 复制粘贴文本
在 SSH 会话窗口中不能用 Ctrl+C 这样的快捷键（Ctrl+C 作用于终止命令执行），复制粘贴需要依赖鼠标。复制操作先用鼠标左键拖拽选中，然后单击选中部分即可复制（如果复制内容太长，可通过鼠标中键分别点一次首尾字符，这样即会快速选中）。粘贴操作则由单击鼠标右键完成。
对于一些使用鼠标操作的程序，上面方法可能不适用，例如 Links 命令行浏览器。需要先按住 Shift 键，然后再配合鼠标操作。
## PuTTY 窗口内容长度
当打开一个很长内容的文件，或者程序命令不断输出内容，PuTTY 会话窗口只显示最后 2000 行内容。如果需要调整，在 Windows 选项里修改 Lines of scrollback 数值。
[![](https://images.cherryfloris.eu.org/2021/1627027061655-c1bb8a14-7d3f-4bcb-847a-bc0d7d0990db.png)](https://www.hostarr.com/wp-content/uploads/putty-tutorial-6.png)
## PuTTY 保存登录用户名
如果登录服务器习惯用同一个用户账号，可以设置会话默认登录用户名，免去每次输入麻烦。在 Connection 选项 Date 里设置。
[![](https://images.cherryfloris.eu.org/2021/1627027065630-2e620fc2-4c68-484a-93cf-249926545160.png)](https://www.hostarr.com/wp-content/uploads/putty-tutorial-7.png)
PuTTY 没有提供保存登录密码的功能，不过仍有方法实现。首先为 putty.exe 创建一个桌面快捷方式，打开快捷方式属性。在快捷方式目标里添加会话参数，格式如下：
D:\putty.exe -load "会话名称" -l "登录用户名" -pw "登录密码"
## PuTTY 使用私钥登录
这里只介绍 PuTTY 设置密钥登录方法，关于创建密钥对及在服务器端配置，后续会[另开文章介绍](https://www.hostarr.com/login-with-an-ssh-private-key-on-linux/)。
依次打开 Connection -> SSH -> Auth 选项，浏览选中私钥文件，保存设置后即可使用密钥方式登录。
[![](https://images.cherryfloris.eu.org/2021/1627027065565-23df02c7-8972-43a7-88ce-f24972fc53a0.png)](https://www.hostarr.com/wp-content/uploads/putty-tutorial-8.png)
如果登录提示下面错误，是因为 PuTTY 不支持 PEM 格式密钥。需要用 puttygen.exe 程序转换一下。
Unable to use key file "D:\id_rsa" (OpenSSH SSH-2 private key (old PEM format))
运行 puttygen.exe，点击 Load 导入私钥文件（如私钥有设置保护密码，需先输入密码），然后点击 Save private key 另存为 ppk 后缀密钥文件（需要手动输文件后缀名）。
[![](https://images.cherryfloris.eu.org/2021/1627027066639-7d89c2f6-a92c-4fd7-91e2-5bbf4e78fd09.png)](https://www.hostarr.com/wp-content/uploads/putty-tutorial-9.png)
## PuTTY 删除会话配置信息
除了在 PuTTY 选项里删除连接会话外，也可以直接删除软件注册表信息。WIN+R 快捷键打开运行窗口，输入 regedit 打开注册表编辑器，找到PuTTY注册表信息删除。路径如下。
HKEY_CURRENT_USER\Software\SimonTatham\PuTTY
到此，PuTTY 使用方法就介绍到这里了。关于文件传输，建议用支持图形化界面的 SFTP 软件，如 WinSCP、FileZilla 这些，使用体验会好一些。
## putty快捷键
**putty**中**粘贴**：鼠标右键 但是，如果觉得用鼠标**粘贴**和键盘快捷键切换浪费时间的话，**putty**中的 **粘贴**可以使用快捷键：Shift + Insert ，其中”Insert”键就是小键盘区域那个“Delete”键上面那个。
