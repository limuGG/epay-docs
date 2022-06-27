---
id: ready
sidebar_position: 2
---

# 接入准备

## 准备接入信息

- 获取 `AppKey` 和 `AppSecret`
- 获取账户地址`address`，用于回调验签
- 通过 [`签名工具`](./sign-tool#生成秘钥对) 生成 `private_key` 和 `public_key`
- 保存 `private_key` 用于签名操作
- 上传 `public_key` 到商户中心用于请求验签
- 上传回调地址到商户中心，客户付款后通知到该地址

:::danger 提示

`private_key` 非常重要，请妥善保存

如果没有上传 `public_key` ，服务将不可用

:::

## 安装签名工具

1. 安装 `docker` [`docker文档`](https://docs.docker.com/get-docker/)
2. 获取 `epay-sign-tool-v1.tar`
3. 导入 `epay-sign-tool-v1.tar`

   ```shell
    docker load -i epay-sign-tool-v1.tar
   ```

4. 启动`epay-sign-tool-v1`

   ```shell
   docker run -d --restart="always" --name='epay-sign-tool' -p="81:8080" epay-sign-tool:v1
   ```

   可以通过[`http://localhost:81`](http://localhost:81)查看 `epay-sign-tool` 服务的状态

:::note 修改端口号

如果需要使用其他端口号,可以修改`-p`参数:如 `-p="9080:8080"`(使用端口号`9080`)

:::
