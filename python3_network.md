# requests
## get
## post

## Response
* r.status_code #响应状态码
* r.raw #返回原始响应体，也就是 urllib 的 response 对象，使用 r.raw.read() 读取
* r.content #字节方式的响应体，会自动为你解码 gzip 和 deflate 压缩
* r.text #字符串方式的响应体，会自动根据响应头部的字符编码进行解码
* r.headers #以字典对象存储服务器响应头，但是这个字典比较特殊，字典键不区分大小写，若键不存在则返回None
* r.json() #Requests中内置的JSON解码器
* r.raise_for_status() #失败请求(非200响应)抛出异常