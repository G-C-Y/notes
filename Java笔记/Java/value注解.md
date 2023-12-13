注意
不能作用于静态变量（static）；

不能作用于常量（final）;

不能在非注册的类中使用（类需要被注册在spring上下文中，如用@Service,@RestController,@Component等）；

使用这个类时，只能通过依赖注入的方式，用new的方式是不会自动注入这些配置的。

配置文件

```
# oncon相关配置  
oncon:  
  app:  
    appid: yx_2eaef45c214fe8e4  
    secret: 32f3abcadc668e4f8f3a67fe40bd078a  
    openid: gz_85af9c59b640a6ed  
    baseurl: http://jk.teamshub.com
```
如果是controller文件中用直接注入就可以

```
@RestController  
public class InrScrSrcController {  
    @Value("${sap.baseurl}") //证券融通平台url  
    private String baseurl;
    @ApiOperation("内部券源推送")  
    @PostMapping("/pushInrScrSrc/v1.0")  
    public String pushInternalStock() {  
        String signCode = taskJob.getSignCode();  
        String res = baseurl + "/hchz-boot/out/yiyun/pushInternalStock";  
        signCode = signCode.replace("+", "%2B");  
        String result = httpClientRequest("signCode="+signCode, res);  
        return result;  
    }  
}
```

如果是普通类中使用

```
@Service
public class YXInterfaceCallUtil {  

    private static String baseUrl;  
    private static String appKey;  
    private static String appSecret;  
  
    @Value("${oncon.app.appid}")  
    private String appid;  
    @Value("${oncon.app.secret}")  
    private String secret;  
  
    @Value("${oncon.app.baseurl}")  
    private String baseurl;  
  
    @PostConstruct  
    public void getAppid() {  
        appKey = this.appid;  
    }  
    @PostConstruct  
    public void getSecret() {  
        appSecret = this.secret;  
    }  
    @PostConstruct  
    public void getBaseurl() {  
        baseUrl = this.baseurl;  
    }  
  
    public static String getOldToken() throws ApiException {  
        String tokenUrl = baseUrl + "/oncon-service/token";  
        TeamshubClient client = new DefaultTeamshubClient(tokenUrl);  
  
        OapiGetOldTokenRequest request = new OapiGetOldTokenRequest();  
        request.setHttpMethod("POST");  
        request.setContentTypeFormData();  
        request.setAppKey(appKey);  
        request.setAppSecret(appSecret);  
        request.setGrantType(grantType);  
        
        OapiGetOldTokenResponse response = client.execute(request);  
        accessTokenOld = response.getAccessToken();  
        return accessTokenOld;  
    }
}
```
