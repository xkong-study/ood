我可以通过修改lc的cookie进行会员登陆，但是我有的时候修改cookie了就要重新登陆这是怎么回事。   

未授权的修改： 如果Cookie被未授权的方式修改，例如被第三方攻击者篡改，服务器可能无法验证用户的身份，因此要求用户重新登录。

怎么验证在传输过程中没有被篡改

在传输过程中验证消息是否被篡改通常涉及使用消息认证码（MAC）或数字签名。HMAC（Hash-based Message Authentication Code）是一种常见的MAC算法，而数字签名通常使用非对称加密算法。

以下是使用HMAC的简单示例：

发送方（生成和发送消息）：

```code
const crypto = require('crypto');

// 生成密钥
const secretKey = 'mySecretKey';

// 待发送的消息
const message = 'Hello, world!';

// 生成HMAC
const hmac = crypto.createHmac('sha256', secretKey);
hmac.update(message);
const hash = hmac.digest('hex');

// 发送消息和HMAC
const payload = {
    message,
    hash
};

```
// 发送 payload 到接收方
接收方（验证消息）：

```code
const crypto = require('crypto');

// 接收到的 payload
const receivedPayload = /* 从发送方获取的 payload */;

// 从 payload 中提取消息和HMAC
const receivedMessage = receivedPayload.message;
const receivedHash = receivedPayload.hash;

// 在接收方使用相同的密钥生成HMAC
const secretKey = 'mySecretKey';
const hmac = crypto.createHmac('sha256', secretKey);
hmac.update(receivedMessage);
const computedHash = hmac.digest('hex');

// 验证接收到的HMAC和计算的HMAC是否相同
if (computedHash === receivedHash) {
    console.log('消息未被篡改！');
} else {
    console.log('警告：消息可能已被篡改！');
}
```

这个简单的示例中，发送方生成消息和对应的HMAC，并将它们一起发送给接收方。接收方接收到消息和HMAC后，使用相同的密钥和相同的HMAC算法重新计算消息的HMAC，并将计算的HMAC与接收到的HMAC进行比较。如果两者匹配，那么消息在传输过程中就没有被篡改。

需要注意的是，密钥的安全性至关重要，因为HMAC是基于密钥的。密钥的安全性取决于如何生成、存储和传输密钥。此外，对于更高级的安全需求，可能需要考虑使用数字签名和公钥基础设施（PKI）等更复杂的机制。



