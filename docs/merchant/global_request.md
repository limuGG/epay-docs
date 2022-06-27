---
sidebar_position: 3
---

# 通用请求

## method

`POST`

## header

```json
{
  "Content-Type": "application/json",
  "Accept": "application/json",
  "AppKey": "`AppKey`",
  "Sign": "`Sign`"
}
```

:::tip `Sign` 生成方法

Sign: 字符串拼接,AppKey+&+AppSecret (注意用'&'连接),将拼接后的结果进行 md5 加密

Sign=md5(AppKey+&+AppSecret)

详情请参考 [`md5编码工具`](./sign-tool#md5编码)

:::

## body

```json
{
  "raw_hex": "`raw_hex`",
  "signature": "`signature`"
}
```

:::info 释义

`raw_hex`: 原始 json 数据的十六进制表示

详情请参考 [`hex编码工具`](./sign-tool#hex编码)

hex(`json data string`)

`signature`: 签名结果

详情请参考 [`签名工具`](./sign-tool#签名)

:::

## 错误返回

```json
{
  "code": 1001,
  "message": "some description"
}
```

HttpStatusCode: `400`

:::note 错误码参考

| 错误码 | 错误描述           |
| :----- | :----------------- |
| 2001   | `AppKey不能为空`   |
| 2002   | `AppKey信息不存在` |
| 2003   | 商户公钥未配置     |
| 2004   | 商户账户信息不存在 |
| 2005   | 请求头签名错误     |
| 2006   | 签名错误           |
| 1001   | 参数错误           |
| 1006   | 余额不足           |
| 500    | 内部系统错误       |
| 1002   | 内部逻辑错误       |

:::
