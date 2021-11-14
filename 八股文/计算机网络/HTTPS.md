- [常见问题](#常见问题)
  - [常见的 Web 方式有哪些？](#常见的-web-方式有哪些)
  - [HTTP 与 HTTPS 的区别？](#http-与-https-的区别)
- [公司](#公司)


</br></br>


# 常见问题
## 常见的 Web 方式有哪些？
答：
1. 主动攻击：直接对服务器上对资源进行攻击，比较有代表性的是 `SQL 注入攻击` 和 `OS 命令注入攻击`。
    - SQL Injection 
        ```
        TxtUserID = getRequestString("UserID");
        txtSQL = "SELECT * FROM user WHERE user_id = " + txtUserId;
        ``` 
        ```
        > UserID: 105 OR 1 = 1
        SELECT * FROM user WHERE user_id = 105 OR 1 = 1;
        ```
2. 被动攻击：攻击者不直接对目标 Web 应用发起攻击，而是诱使用户触发已经设置好的陷阱，获取用户的资源和权限，比较有代表性的是跨站脚本攻击（XSS）和跨站点请求伪造。


## HTTP 与 HTTPS 的区别？
- HTTP + 通信加密 + 证书认证 + 完整性保护 = HTTPS
- HTTP主要有这些不足：
    1. 通信使用明文 -> 窃听
    2. 不验证通信方的身份 -> 伪装
    3. 无法验证报文的完整性 -> 篡改


</br></br>


# 公司