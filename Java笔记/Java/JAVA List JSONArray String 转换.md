# JAVA List JSONArray String 转换
**1.List转JSONArray**
```java
List<T> list = new ArrayList<T>();
JSONArray array= JSONArray.parseArray(JSON.toJSONString(list))；
```
**2.JSONArray转List**
```java
JSONArray array = new JSONArray();
List<EventColAttr> list = JSONObject.parseArray(array.toJSONString(), EventColAttr.class);
```
**3.String转JSONArray**
```java
String st = "[{name:Tim,age:25,sex:male},{name:Tom,age:28,sex:male},{name:Lily,age:15,sex:female}]";
JSONArray tableData = JSONArray.parseArray(st);
```
# java提取json字符串中的值
```java
JSONObject json = JSON.parseObject(recv);
Object storePath = json.getJSONObject("data").get("storePath");
```
```java
public class Test {
	public static void main(String[] args) {
		String resultStr = "{\"status\": 0,\"message\": \"query ok\","+
				"\"result\": {\"address\": \"北京市海淀区镜桥\","+
				"\"address_component\": {\"nation\": \"中国\",\"province\": \"北京市\","+
				"\"city\": \"北京市\",\"district\": \"海淀区\","+
			"\"street\": \"镜桥\",\"street_number\": \"镜桥\"}}}";
		
		JsonParser jp = new JsonParser();
		//将json字符串转化成json对象
            JsonObject jo = jp.parse(resultStr).getAsJsonObject();
            //获取message对应的值
            String message = jo.get("message").getAsString();
            System.out.println("message：" + message);
            //获取address对应的值
            String address = jo.get("result").getAsJsonObject().get("address").getAsString();
            System.out.println("address：" + address);
            //获取city对应的值
            String nation = jo.get("result").getAsJsonObject().get("address_component")
        						.getAsJsonObject().get("nation").getAsString();
            System.out.println("nation：" + nation);
	}
}
```
