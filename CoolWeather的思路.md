# CoolWeather的思路

## 1.创建数据库和表

在db包下面新建实体类：省  市  县：

从Json数据中可以知道，省的实体类要有三个属性：id   省的名字  省的代码

​                                           市有四个属性：id ，市的名字和代码  ， 市所属省的id

​                                         县有四个属性 ：id  县的名字和天气id  县所属市的id

配置litepal.xml  让表和类一一映射。



## 2.遍历全国省市县数据

最初的数据是从服务器端获得的，可以创建一个工具类用来与服务器交互。

```java
public class HttpUtil {
    public static void sendOkHttpRequest(String address,okhttp3.Callback callback){
        OkHttpClient client = new OkHttpClient();
        Request request = new Request.Builder().url(address).build();
        client.newCall(request).enqueue(callback);
    }
}
```

发起一条HTTP请求只需要调用sendOkHttpRequest() 方法 ，填入地址，注册一个回调来处理服务器响应就可以。