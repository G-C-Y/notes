
前段时间与杭研联调遇到protobuffer数据转换的Base64字符串在发到后端出现异常的问题，调查了一下发现base64里的+号发过去变成了空格，进一步查找发现是由于我们的数据是附在url，实际上是url转换造成的，其实我们应该对parameter做转码处理，再通过url发送才不会出现这样的问题。

**网上解决方案**

前台处理 ：java方法：URLEncoder.encode(str,"UTF-8");js 方法encodeURIComponent(str);

后台处理：URLDecoder.decode(str,"UTF-8");

经测试，编码形式 会改变一些其他字符，例如 “=”变成了“%3D”

**解决方案：JAVA 后端对字符串进行替换**

url = url.replaceAll(" ","+");

经过测试，成功。
或者是，前端通过请求头方式去控制。

- base64加密参数Http传输

base64中，加号（+）是base64编码的一部分，如果将+号转变为空格，就会导致解密失败。

现在应该很清楚为什么base64后，通过http请求后，数据丢失的原因了吧。

1、Base64加密后的数据：

```
gLi5lSf1FW+r1nuhjheOlA2vYlbt1U9kOKnGPPG/LZU+J7qlqUSckCtGfRiQkkqgfZHwEGaBZkpGWuIyZ+tCegU8xj85Xp7bG3Fyfd6k=
```
在对Base64加密进行http传输时，后台收到的数据会出现空格的现象。如下


```
gLi5lSf1FW r1nuhjheOlA2vYlbt1U9kOKnGPPG/LZU J7qlqUSckCtGfRiQkkqgfZHwEGaBZkpGWuIyZ tCegU8xj85Xp7bG3Fyfd6k=
```

这就导致传输的数据和接收的数据不一致，导致解密失败

2、base64 http请求，如何将+号进行urlEncode

设置http请求头（对参数进行urlEncode操作）   
Content-Type: application/x-www-form-urlencoded

3、Base64 urlEncode后：

```
gLi5lSf1FW%2r1nuhjheOlA2vYlbt1U9kOKnGPPG/LZU%2J7qlqUSckCtGfRiQkkqgfZHwEGaBZkpGWuIyZ%2tCegU8xj85Xp7bG3Fyfd6k=
```

4、后台接收的数据：

```
gLi5lSf1FW+r1nuhjheOlA2vYlbt1U9kOKnGPPG/LZU+J7qlqUSckCtGfRiQkkqgfZHwEGaBZkpGWuIyZ+tCegU8xj85Xp7bG3Fyfd6k=
```

这时，接收的base64数据和传输的是结果一致，可以正常解密了。

- 什么是：application/x-www-form-urlencoded

简单的讲就是form表单提交。   
浏览器会对form表单的数据进行url编码，把form数据转换成一个字串（name1=value1&name2=value2…），然后把这个字串append到url后面，用?分割，加载这个新的url

如果表单有加号（+），url编码后会变为%2，这时后接收数据后，对参数解码后转变为+号   
如果表单有空格，url编码后会变为+，后台接收数据化，解码变为空格