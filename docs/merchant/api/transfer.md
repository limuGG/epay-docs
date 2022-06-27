---
sidebar_position: 2
---

# 转账付款

## 请求参数原始数据

```json
{
  "to_address": "TB1Eab9287cFe0DaE94eA4BdB2FcaFD47609E8385",
  "amount": 888
}
```

### 原始数据 **释义:**

| 参数       | 类型   | 必填? | 描述           |
| :--------- | :----- | :---: | -------------- |
| to_address | String | ✅yes | 转账的目标地址 |
| amount     | Number | ✅yes | 转账金额       |

## 响应参数

```json
{
  "code": 200
}
```

### 响应参数 **释义:**

| 参数 | 类型   | 描述   |
| :--- | :----- | :----- |
| code | Number | 状态码 |
