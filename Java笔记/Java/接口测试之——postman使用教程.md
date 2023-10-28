# Postman介绍
Postman是google开发的一款功能强大的网页调试与发送网页HTTP请求，并能运行测试用例的的Chrome插件。其主要功能包括：
**模拟各种HTTP requests**
从常用的 GET、POST 到 RESTful 的 PUT 、 DELETE …等等。 甚至还可以发送文件、送出额外的 header。
**Collection 功能（测试集合）**
Collection 是 requests的集合，在做完一個测试的時候， 你可以把這次的 request 存到特定的 Collection 里面，如此一來，下次要做同样的测试时，就不需要重新输入。而且一个collection可以包含多条request，如果我们把一个request当成一个test case，那collection就可以看成是一个test suite。通过collection的归类，我们可以良好的分类测试软件所提供的API.而且 Collection 还可以 Import 或是 Share 出來，让团队里面的所有人共享你建立起來的 Collection。
**人性化的Response整理**
一般在用其他工具來测试的時候，response的内容通常都是纯文字的 raw， 但如果是 JSON ，就是塞成一整行的 JSON。这会造成阅读的障碍 ，而 Postman 可以针对response内容的格式自动美化。 JSON、 XML 或是 HTML 都會整理成我们可以阅读的格式
**内置测试脚本语言**
Postman支持编写测试脚本，可以快速的检查request的结果，并返回测试结果
**设定变量与环境**
Postman 可以自由 设定变量与Environment，一般我们在编辑request，校验response的时候，总会需要重复输入某些字符，比如url，postman允许我们设定变量来保存这些值。并且把变量保存在不同的环境中。比如，我們可能会有多种环境， development 、 staging 或 local， 而这几种环境中的 request URL 也各不相同，但我们可以在不同的环境中设定同样的变量，只是变量的值不一样，这样我们就不用修改我们的测试脚本，而测试不同的环境。
### 优点：
1、支持用例管理
2、支持get、post、文件上传、响应验证、变量管理、环境参数管理等功能
3、支持批量运行
4、支持用例导出、导入
5、支持云端保存用例【付费用户】
可以说POSTMAN满足了HTTP接口测试的大部分功能，只有少部分的功能不被支持，比如：请求流程的控制；前面说了这么多，接下来我们就看看POSTMAN的安装与使用吧。
## 1、安装Postman
Postman作为一个chrome的插件，你可以打开chrome，在chrome webstore里面找到。当然，如果是在国内，你需要翻墙，否则的话，你只能百度一下，搜索postman的安装包自己安装到chrome上（这里就不赘述了，有很多类似的文章）。这里需要提一下的是，你可以不用打开chrome而直接使用Postman，具体的方法是：
选项->更多工具->扩展程序
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951180286-89716bd4-15e9-454f-97e1-172a2db8ace2.webp#clientId=u37044515-ad8c-4&from=paste&id=ub5142cac&originHeight=687&originWidth=901&originalType=url&ratio=1&status=done&style=none&taskId=u3bb1ccbb-38be-4a1a-9782-55a708b4d51)详细信息->创建快捷方式->‘全部勾上’ ，这样你就可以在任何地方启动你的Postman了
这里也可以直接一键安装[postman](https://www.getpostman.com/apps)，与谷歌插件使用一样
## Postman sending requests
安装好之后，我们先打开Postman，可以看到界面分成左右两个部分，右边是我们后头要讲的collection，左边是现在要讲的request builder。在request builder中，我们可以通过Postman快速的随意组装出我们希望的request。一般来说，所有的HTTP Request都分成4个部分，URL, method, headers和body。而Postman针对这几部分都有针对性的工具。
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951214661-824f562d-3b25-47d7-a94d-352e74d933c2.webp#clientId=u37044515-ad8c-4&from=paste&id=u7e873082&originHeight=464&originWidth=723&originalType=url&ratio=1&status=done&style=none&taskId=u9d068f17-1662-4cb2-b6c3-85da6d262c5)
#### 2、新建一个项目
直接点击左边栏上面的添加目录图标来新增一个根目录，这样就等于新建了一个项目，我们可以把一个项目或一个模块的用例都存放在这个目录之下，并且在根目录之下我们还可以在建立子目录来进行功能用例的细分，具体见下图。
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951244378-a4df0232-c833-43bf-b11c-32d4b07909b6.webp#clientId=u37044515-ad8c-4&from=paste&id=u7c18e782&originHeight=522&originWidth=672&originalType=url&ratio=1&status=done&style=none&taskId=u414012f8-38df-4e65-ac8e-4f1601ea572)
#### 新增一个用例
创建了项目目录后我们就可以新建用例了，具体是点击右侧区域的+号来新增一个空用例的模板，也可以通过复制一个已有用例来达到新建一个用例的目的，2种方法见下：
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951378585-e1c89c53-20b3-40aa-94f3-68e2abf4b67c.webp#clientId=u37044515-ad8c-4&from=paste&id=ue7bcc962&originHeight=555&originWidth=971&originalType=url&ratio=1&status=done&style=none&taskId=u68ad2e43-cdb8-4baf-86b7-5a254fab490)
#### 3、添加请求信息
新建的用例请求内容为空，我们需要添加相应的请求信息，这部分的操作都在右侧的信息区域，一般流程如下：
选择一个请求方法，如：get或post
填写请求的url，如：http://www.baidu.com
如果是get则请求参数直接写在url后，用？连接
如果是post则请求添加在body中
点击“send”发送请求
查看请求响应内容
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951390384-d9f05841-7afc-4cae-878a-bee6e8413412.webp#clientId=u37044515-ad8c-4&from=paste&id=u5b1aeddd&originHeight=697&originWidth=1078&originalType=url&ratio=1&status=done&style=none&taskId=uf83c31c1-2cf9-4c84-8706-34b9d17edfc)
#### 4、post请求参数
post请求的主要的特点是把请求数据放在body中，而非url后
那我们就需要编辑Request Body，Postman根据body type的不同，提供了4中编辑方式：
form-data
x-www-form-urlencoded
raw
binary
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951404313-685799a3-a636-44d9-bf88-99ef2feae43e.webp#clientId=u37044515-ad8c-4&from=paste&id=ua108c998&originHeight=315&originWidth=1060&originalType=url&ratio=1&status=done&style=none&taskId=u90e02cfe-4810-44c4-b905-bc73c2f0147)
上面的样例是post方式传输普通参数，如果我们需要发送带文件的请求时，就要改下请求格式了，具体如下：
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951441173-3160cf01-514c-4087-b4b4-98e7a74090b6.webp#clientId=u37044515-ad8c-4&from=paste&id=u3d975d2b&originHeight=304&originWidth=857&originalType=url&ratio=1&status=done&style=none&taskId=ube72dde5-4dae-478f-9003-928238a980d)
注意上面标红框的内容，都是必须要对应上。
#### 5、添加头信息
有些时候请求时还需要一些特定的头信息，postman同样可以完美的支持，直接点击Headers标签就可以进行请求头的信息设置
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951466760-7e4f022d-696c-4ba3-a4bf-9ffd4eb36ab4.webp#clientId=u37044515-ad8c-4&from=paste&id=u1024a719&originHeight=97&originWidth=806&originalType=url&ratio=1&status=done&style=none&taskId=uf6b56156-f6af-478c-baa0-ba59a54b4cb)
#### 6、预处理和结果检查
预处理主要是对一些环境变量之类的进行设置，相当于数据初始化；如图：
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951487457-8e501102-5cbc-4ab2-b884-5b0b85f37b46.webp#clientId=u37044515-ad8c-4&from=paste&id=ua98b00fb&originHeight=477&originWidth=1040&originalType=url&ratio=1&status=done&style=none&taskId=u41ba83d8-012e-4e45-8ce2-bfefa926fa0)
响应处理就是对响应结果进行分析和验证，比如检查code是不是200，内容是不是等于具体某个值，是否包含特定的值等等。
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951515875-9c65f709-4b81-4594-8cd1-65fb7fdeeab4.webp#clientId=u37044515-ad8c-4&from=paste&id=u8631d87f&originHeight=428&originWidth=1040&originalType=url&ratio=1&status=done&style=none&taskId=u72df88fa-2e74-4162-8915-191a5106244)
因为预处理和结果检查都是使用js作为脚本语言，所以你还可以进行任意的js可以实现的场景，来辅助测试。
#### 7、全局变量与环境变量
全局变量我们可以自己在预处理和结果处理2个脚本环境里进行赋值，在具体的测试数据里我们就可以直接使用，具体的使用方法是为：{{variable_key}}；比如你在脚本中可以设置全局变量：
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951564920-b1f6e2fe-bb04-4c0b-a710-c827a0d50fb7.webp#clientId=u37044515-ad8c-4&from=paste&id=u7b70450b&originHeight=30&originWidth=834&originalType=url&ratio=1&status=done&style=none&taskId=u91c82b3d-53a7-42bd-a90a-5ef27c0c3ff)
那么在用例数据项里面我就可以这样使用，{{username}}，用来代表具体的tester值，具体见下图
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951577380-328d5382-32a6-4127-a7d3-6100a4a3ce18.webp#clientId=u37044515-ad8c-4&from=paste&id=u5e3815c8&originHeight=210&originWidth=939&originalType=url&ratio=1&status=done&style=none&taskId=ufb9dcbaf-65af-4253-9aef-69f4a49a6ff)
而环境变量的设置可使用与全局变量基本一样，只是环境变量我们还有另外一个入口可以进行设置，那就是环境配置管理中，我们可以预先建立若干和与环境相关的一套变量，根据实际的测试需求在执行前选择对应的环境变量模板，这样可以快速切换测试服务器与线上服务器之前的环境差异。比如：配置2套环境变量模板，一套url是测试环境，另一套为线上环境，根据测试对象不同我们选择不同的环境变量模板就行了，而不再需要修改测试数据中的url了。
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951600165-6cb19d73-2353-47f3-bfff-9f0584ce6c1b.webp#clientId=u37044515-ad8c-4&from=paste&id=u833ab856&originHeight=84&originWidth=826&originalType=url&ratio=1&status=done&style=none&taskId=ufff9eef7-7afd-4ec3-93e3-b2e6fe3d157)
上面我们就把请求的host提取出来，然后在不同环境变量模板里使用不同的url值，后面我们就可以通过选择不同的环境变量模板来进行对应的请求测试
#### 8、导出用例为代码
POSTMAN还有一个很赞的地方就是导出用例为CODE，即如果你编写好了用例之后可以通过点击“Generate Code”来一键生成代码，并且还有好多语言和类库可以选择，帧的是棒棒哒！
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951627267-5eaa3af0-2af6-4328-8cd6-a696697e5e64.webp#clientId=u37044515-ad8c-4&from=paste&id=uc606e9c4&originHeight=673&originWidth=1092&originalType=url&ratio=1&status=done&style=none&taskId=ub85dfe12-9c8e-467f-a1b6-8d8234f9bc6)
#### 9、批量执行用例
最后我们再来看看POSTMAN的批量执行功能，这个功能由单独的runner来负责的，我们需要在另外的界面进行操作，具体如下：
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951654463-2c25769a-b31d-474f-9d7e-d63aeca87666.webp#clientId=u37044515-ad8c-4&from=paste&id=ubc307d71&originHeight=640&originWidth=664&originalType=url&ratio=1&status=done&style=none&taskId=u156644ce-a931-4df1-8c77-34adee2befb)
依次点击上面的按钮就会出现runer界面，如下直接点击“Start Test”即可
![](https://cdn.nlark.com/yuque/0/2021/webp/21372399/1631951739743-2b9e28fc-3f57-4cc7-9e8a-b0478ab771a4.webp#clientId=u37044515-ad8c-4&from=paste&id=u667736e9&originHeight=700&originWidth=1060&originalType=url&ratio=1&status=done&style=none&taskId=uc0093c1b-d1f9-46b8-908e-088f16c391b)
#### 另推荐同类型软件：Apipost，中文界面比较友好
