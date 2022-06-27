---
sidebar_position: 3
---

# 付款结果回调通知

## 使用说明

- 需要在商户后台上传通知地址
- 在支付完成后，`epay-api` 会调用该地址，并传递支付结果参数
- 商户需要在该地址中处理支付结果
- 接收到结果后,需要进行验签,确保数据的合法性
- 订单处理结束后,需要返回一个 `HttpStatusCode = 200 OK` 的响应,返回结果为 `success` ,否则 `epay-api` 将重复调用该地址

:::tip 通知轮询

- 如果回调接口返回错误，`epay-api` 会在 `30秒` 后重试，直到成功为止
- 如果付款时间超过 `1小时`，`epay-api` 将会终止轮询

:::

## 回调验签

- 回调验签是 EPay 为商户提供的一种验证方式,用于验证商户接收到的支付结果是否合法
- 回调验签是通过商户账户地址和支付结果签名结果来验证的
- 使用 [`签名校验工具`](../sign-tool#验证签名) 验证数据的合法性

## 通知请求方式

- method: `POST`
- header: `Content-Type: application/json`
- body:

```json
{ "raw_hex": "原始数据hex序列化后的字符串", "signature": "签名结果" }
```

## 原始数据

将通知结果中的`raw_hex`进行 [`hex解码`](../sign-tool#hex解码)，获取原始数据

详情请参考 [`hex解码工具`](../sign-tool#hex解码)

### 原始数据结构

```json
{
  "trade_no": "2014072300007148",
  "out_trade_no": "2014072300007148",
  "amount": 888.88,
  "buyer_address": "TA5tWaMwtRRgAdkw3yRYbgs5HZWHGxkSKr",
  "pay_time": "2014-07-23 15:00:00",
  "scene": {}
}
```

### 原始数据结构 **释义:**

| 参数          | 类型   | 是否必填 | 描述           |
| :------------ | :----- | :------- | :------------- |
| trade_no      | String | ✅yes    | 内部交易流水号 |
| out_trade_no  | String | ✅yes    | 商户订单号     |
| amount        | Number | ✅yes    | 交易金额       |
| buyer_address | String | ✅yes    | 买家账户地址   |
| pay_time      | String | ✅yes    | 付款时间       |
| scene         | Object | ❓ no    | 附加数据       |
