---
sidebar_position: 5
---

# 签名工具

```shell
export baseURL="http://localhost:81"
```

## 生成秘钥对

```shell
curl -L -X POST "$baseURL/generateKey"
```

:::tip 说明

- response: 返回秘钥对; `private_key` 需要在本地妥善保存,非常重要

```json
{
  "private_key": "08431277AEF959466EBD02D9B080B3143E741783BD3F2917671783E2C187A2B5",
  "public_key": "04756D3D75B0E6AAB00AC740B98E6F12978CE184BDEA2AF367F110A43C59D758B7817A633BCFF64D4169972EA8A7D00B443A276B127F069C75F4FF988EA806363A",
  "hex": "4187C6FE527DEF95335E8AABBBC0D28737DD5F0C69",
  "base58": "TNM8cGDThJzBy7hrfmc7trCYuzz4BExb9Y"
}
```

:::

## 签名

```shell
curl -L -X POST "$baseURL/sign" \
--header 'Content-Type: application/json' \
--data-raw '{
    "private_key": "27C47FD92C5CA07711C6209C79BFAE4110E6C4224E5757D693E0F39926212C34",
    "data": "7b22616d6f756e74223a3130302c226f75745f74726164655f6e6f223a22303032222c2272657475726e5f706e67223a66616c73657d"
}'
```

:::tip 说明

- private_key: 私钥
- data: 待签名数据
- response: 返回签名结果

```json
{
  "signature": "63b9669947526cf24c5fc527c8790509d79c11a604a67b7958b6b90914a6ba2c485b3ddf89fe2688c87f1a4c0fdd443428b3ad14304e843f830d86456c08164c00"
}
```

:::

## 验证签名

```shell
curl -L -X POST "$baseURL/verify" \
--header 'Content-Type: application/json' \
--data-raw '{
    "address": "THXrnwp8aQqgidY1ApRSXFnKGS6abL7wLY",
    "signature": "91ecccd21d022faccfb6766b5edcb1686c279196023987b0dabe11a86b0ee0e6206dfa09950714769e1330ed1f810b43ec8508b0c2b562d76e473cc9e956e9c300",
    "data": "7b22616d6f756e74223a3130302c226f75745f74726164655f6e6f223a22303031222c2272657475726e5f706e67223a66616c73652c227363656e65223a7b2273746174223a317d7d"
}'
```

:::caution 说明

- address: 商户本身的账户地址
- signature: 签名由 `api服务器` 发送
- data: `hex数据`

- response: 签名是否通过验证

```json
{
  "valid": true
}
```

:::

## `hex编码`

```shell
curl -L -X POST "$baseURL/hexEncode" \
--header 'Content-Type: application/json' \
--data-raw '{
    "amount": 100,
    "out_trade_no": "002",
    "return_png": false
}'
```

:::tip 说明

- response: 返回编码结果

```json
{
  "data": "7b22616d6f756e74223a3130302c226f75745f74726164655f6e6f223a22303032222c2272657475726e5f706e67223a66616c73657d"
}
```

:::

## `hex解码`

```shell
curl -L -X POST "$baseURL/hexDecode" \
--header 'Content-Type: application/json' \
--data-raw '"7b22616d6f756e74223a3130302c226f75745f74726164655f6e6f223a22303031222c2272657475726e5f706e67223a66616c73652c227363656e65223a7b2273746174223a317d7d"'
```

:::caution 注意

- 请求中的数据格式是 `字符串`

:::

:::tip 说明

- response: `data` 返回解码结果

```json
{
  "data": {
    "amount": 100,
    "out_trade_no": "001",
    "return_png": false,
    "scene": { "stat": 1 }
  }
}
```

:::

## `md5编码`

```shell
curl -L -X POST "$baseURL/md5" \
--header 'Content-Type: application/json' \
--data-raw '"10D62FF476F5C7E2&j7oY8WHxGPxYg1XZA31Qbq7GhQanzdht"'
```

:::caution 注意

- 请求中的数据格式是 `字符串`

:::

:::tip 说明

- response: 返回编码结果

```json
{ "data": "ea1f5771dec7386f9071b71ff97f0862" }
```

:::
