
在对网页抓包中发现,返回的很多网页是经过压缩的,比如访问谷歌首页,返回的头文件中包含Content-Encoding gzip

使用gzip可以省下很多网页流量,在网速一定的情况下,可以提高访问效率,我们用java访问时如何可以得到gzip的返回,并且我们如何解析返回的gzip呢?

我们以访问http://www.baidu.com/为例  
我们用URL的openStream方法直接访问时并不返回gzip压缩数据,这是因为时候返回gzip需要判断浏览器是否支持gzip压缩,所以我们请求数据的时候在http请求头中添加支持gzip的请求头就可以  
添加conn.setRequestProperty(“Accept-Encoding”, “gzip,deflate”);就告诉服务器你的浏览器支持gzip解压了


```
URL url = new URL("http://www.baidu.com/");
HttpURLConnection conn = (HttpURLConnection) url.openConnection();
conn.setRequestProperty("Accept-Encoding", "gzip,deflate");
conn.connect();

InputStream in = conn.getInputStream();

BufferedReader bin = new BufferedReader(new InputStreamReader(in, "GB2312"));
String s = null;
while((s=bin.readLine())!=null){
	System.out.println(s);
}
bin.close();
```


 

**没有conn.setRequestProperty(“Accept-Encoding”, “gzip,deflate”);不会出现乱码

**加上conn.setRequestProperty(“Accept-Encoding”, “gzip,deflate”);就是乱码,这是因为服务器对返回内容进行了gzip压缩的缘故,我们只要判断返回头是否包含Content-Encoding gzip,就可以判断是不是压缩过的数据,对待压缩后的数据我们只需进行gzip解压就好了

只需将上面的代码加上

```
GZIPInputStream gzin = new GZIPInputStream(in);
并将
BufferedReader bin = new BufferedReader(new InputStreamReader(in, "GB2312"));
改为
BufferedReader bin = new BufferedReader(new InputStreamReader(gzin, "GB2312"));
```


当然是否需要gzip解压,只判断返回数据头是否包含Content-Encoding gzip就可以了