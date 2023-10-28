# 我的解决办法：
controller层加依赖
```java
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.0.17.Final</version>
</dependency>
```
加异常类
```java
package com.thingshub.ifactory.tmom.controller;

import com.thingshub.common.model.ResponseModel;
import org.springframework.http.HttpStatus;
import org.springframework.validation.ObjectError;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import java.util.List;

@RestControllerAdvice
public class TmomExceptionHandler {

    @ResponseStatus(HttpStatus.OK)
    @ExceptionHandler(RuntimeException.class)
    public ResponseModel handleException(RuntimeException ex){
        ex.printStackTrace();
        return ResponseModel.of(HttpStatus.INTERNAL_SERVER_ERROR.value(), ex.getMessage());
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseModel<?> handleMethodArgumentNotValidException(MethodArgumentNotValidException methodArgumentNotValidException) {
        List<ObjectError> errors = methodArgumentNotValidException.getBindingResult().getAllErrors();
        return ResponseModel.of(501, errors.stream().findFirst().get().getDefaultMessage());
    }
}
```
# ![image.png](https://images.cherryfloris.eu.org/2022/1646803797365-16393e72-e1f5-471f-8d67-c4f9790bfe7f.png)
# 参考原文：
## 校验非空的注解@NotNull怎么取得自定义的message
**所有的Controller 都写这样的代码就要封装成异常类**
```java
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseBody;
/**
 * @author ：lsy
 * @date ：Created in 2020/7/23 10:13
 * @modified By：
 */
@ControllerAdvice
public class ControllerException {
    private final static String EXCEPTION_MSG_KEY = "Exception message : ";
    @ResponseBody
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public Object handleValidException(MethodArgumentNotValidException e) {
        //日志记录错误信息
       // log.error(Objects.requireNonNull(e.getBindingResult().getFieldError()).getDefaultMessage());
        //将错误信息返回给前台
       // return BaseResult.fail(500, Objects.requireNonNull(e.getBindingResult().getFieldError()).getDefaultMessage());
        return e.getBindingResult().getFieldError().getDefaultMessage();
    }
}
```
原文链接：[https://www.yisu.com/zixun/614358.html](https://www.yisu.com/zixun/614358.html)

## @valid 不生效_SpringBoot 中使用 @Valid 注解 + Exception 全局处理器优雅处理参数验证
原文链接：[https://blog.csdn.net/weixin_39971132/article/details/111169396?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0.pc_relevant_default&spm=1001.2101.3001.4242.1&utm_relevant_index=3](https://blog.csdn.net/weixin_39971132/article/details/111169396?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0.pc_relevant_default&spm=1001.2101.3001.4242.1&utm_relevant_index=3)
