## 1 . 什么是 OAuth
开放式授权协议

现在使用 OAuth 2.0 
```javascript
- 1 . 请求OAuth登录页
    Request Token URL 未授权的令牌请求服务地址
      第三方请求qq登录页面时 使用的带有 特定参数的URL

    client : appid
    redirect_uri : 回调地址

- 2 . 用户使用QQ号登录 并授权
当url跳转回 指定的回调地址后 会带一个 code

- 3 . 返回登录结果
    只有一个code 值 不能让第三方 使用QQ登录 需要第三方 再请求一个地址
    User Authorization URL 用户授权的令牌请求服务地址
    第三方QQ登录授权之后  需要请求一个 带有 特定参数的 URL
    注册时 我方获取的获取appid appkey 
    code(有效时间十分短,10s左右)

    请求 OAuth登录页 
    qq向回调地址 返回 code
    请求 OAuth登录页 
    QQ向第三方返回 AccessToken RefreshToken
```