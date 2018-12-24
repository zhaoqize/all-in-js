## 一、Rewrite前端域名不变

rewrite flag 命令
- last相当于Apache里的[L]标记，表示完成rewrite
- break终止匹配, 不再匹配后面的规则
- redirect返回302临时重定向 地址栏会显示跳转后的地址
- permanent返回301永久重定向 地址栏会显示跳转后的地址

## 二、地址重写与地址转发

### 1、地址重写

地址重写是实际上是为了实现址标准化

### 2、地址转发

一个域名指向另一个已有站点的过程，地址栏的地址保持不变

## 三、rewrite 使用场景

- 调整用户浏览的URL，看起来更规范，合乎开发及产品人员的需求。
- 为了让搜索引擎搜录网站内容及用户体验更好，企业会将动态URL地址伪装成静态地址提供服务。
- 网址换新域名后，让旧的访问跳转到新的域名上。例如，访问京东的360buy.com会跳转到jd.com
- 根据特殊变量、目录、客户端的信息进行URL调整等

## 四、参考&拓展
- [Nginx Rewrite](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#rewrite)