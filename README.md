

修改记录：



* 1389行修改：
添加：getOriginalUri()；解决getUri()，无法拿到域和端口问题

* 1366 + 2111行修改：
获取：socket 的址址，作为：remoteAddr（否则没有远程连接地址）

* 1491行修改：
添加_paramsList，实现参数寄存功能（流只能读一次，后面就没了）

* 2807行修改：
将编译改为：UTF-8；解决中文参数乱码问题

* 1748行修改：（优先使用传进来的contentType，解决内部404之类的调用无法显示为html的问题 ）

```java
public void sendHeaders(int status, long length, long lastModified, String etag, String contentType, long[] range) throws IOException {
    String ct = headers.get("Content-Type");
    if (ct == null) {
        ct = contentType != null ? contentType : "application/octet-stream";
        headers.add("Content-Type", ct);
    } else {
        if (contentType != null) { //noear,20181220
            ct = contentType;
        }

        headers.replace("Content-Type", ct);
    }
}
```