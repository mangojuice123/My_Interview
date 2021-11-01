- [常见问题](#常见问题)
  - [HTTP 中 GET/POST 的区别？](#http-中-getpost-的区别)
  - [浏览器中 GET/POST 的区别？](#浏览器中-getpost-的区别)
  - [公司](#公司)

</br></br>

# 常见问题
## HTTP 中 GET/POST 的区别？
答：
- 本质上没有什么区别，可以自由地去利用格式。但是太自由带来了另一种麻烦，即开发工作时形式的不统一导致的低效。因此，有了一系列的接口规范和风格，其中比较出名的是 [`REST`](https://www.zhihu.com/question/28570307/answer/163638731)。
- REST 中：
  - GET + URL = 获取资源
  - POST + URL + body = 创建一个资源（与浏览器中的 POST 不同）

## 浏览器中 GET/POST 的区别？
答：
- GET：读取一个资源，是幂等的，可以对请求的数据进行缓存。
    - 浏览器直接发出的 GET 只能由一个 URL 触发，因此 GET 在 URL 之外带一些参数就只能依靠 URL 上附带 queryString（但是 HTTP 协议本身没有这样的限制）
- POST：提交一个表单，发出一个 POST 请求让服务器做一件事，这件事往往是不幂等的，因此不能缓存。
    - 表单提交时，表单中的数据被浏览器编码到 HTTP 请求到 body 里。
- 浏览器场景下：
  - GET 请求没有 body，只有 URL，请求数据放在 URL 的 queryString 中；
  - POST 请求的数据在 body 中。

## 公司
- 2021-9 美团