近期接手一个需求，需求转成代码实现就是需要在一个接口实现很多参数传递的同时加上文件上传，考虑到参数比较多，参数封装成body上传，文件用单独的 MultipartFile 接收；前端死活对接不出来，在这里对前端同学表示歉意，是在下的错；这里解释一下原因和比较简单的处理方式。

1.问题接口展示和故障说明
```java
@PostMapping("/create")
public ApiResultBean postTest(HttpServletRequest request,
                              @RequestBody PayOrderCreateReqDto payOrderCreateReqDto,
                              @RequestParam(value = "applyFiles") MultipartFile applyFiles
    )
```
从代码层面看一点问题没有，但是这里引入一下http的知识：

HTTP请求分为了消息头和消息体，头信息里面的Content-Type字段定义了消息体的请求格式，接口里面声明  @RequestBody 的参数只能设置为 "Content-Type: application/json"，而 MultipartFile 参数只能设置为"Content-Type: multipart/form-data"，上述两种格式并不是兼容的，那问题就来了，前端请求的时候 Content-Type 怎么设置，无论哪种格式都是错的。

2.解决方式
1）.前端统一格式"Content-Type: multipart/form-data"，把结构体拆分成参数，把参数传递过去，接收后再组装结构体，举例如下：
```java
@PostMapping("/create")
public ApiResultBean postTest(HttpServletRequest request,
                              @RequestParam(value = "name") String name,
                              @RequestParam(value = "id") String id,
                              @RequestParam(value = "applyFiles") MultipartFile applyFiles
    )
```
2）.前端统一格式"Content-Type: multipart/form-data"，结构体在前端传递的时候统一转成json字符串，后端接收以后用Gson转成结构体，举例如下：
```java
@PostMapping("/create")
public ApiResultBean postTest(HttpServletRequest request,
                              @RequestParam(value = "dtoJson") String payOrderCreateReqDto,
                              @RequestParam(value = "applyFiles") MultipartFile applyFiles
    ) {
        Gson gson = new Gson();
        PayOrderCreateReqDto toDto = gson.fromJson(payOrderCreateReqDto,PayOrderCreateReqDto.class);
        return null;
    }
```
以上方式比较简陋，仅分享个人处理方法。
3.修改上传文件大小限制
SpringBoot 默认上传文件大小 1M，实际使用可能会突破这个限制，所以需要在配置文件中配置上传文件大小，配置如下：
```java
spring:
servlet:
multipart:
max-file-size: 10MB # 设置单个文件的大小为10M
max-request-size: 50MB # 设置总上传的数据大小为50M
```

