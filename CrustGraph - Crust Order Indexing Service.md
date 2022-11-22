---
tags: [decoo]
title: CrustGraph - Crust Order Indexing Service
created: '2022-11-22T05:00:53.071Z'
modified: '2022-11-22T05:01:08.910Z'
---

CrustGraph - Crust Order Indexing Service


# 目的

构建一个通用的 L2 层的 Crust Order 索引服务，完善 Crust 生态。

## MVP

- 支持常规的 CID -> Order 查询

- 针对 Folder 下单场景，支持通过 Sub-Folder & File 的 CID，查询对应的 Order


## 扩展功能

- 针对没有设置 memo 字段的订单 (见下述 Proposal)，尝试自动检测 CID 是否为 Folder 

- 支持更多维度的聚合查询，比如：
  - 通过 Order ID (tx hash) 查询
  
  - 通过订单状态、下单帐号、下单日期、到期时间、是否有 Renew Pool 等信息过滤查询

- 支持 GraphQL

- Open Service，支持生成 API Key 给第三方使用


# Proposal

## api.tx.market.placeStorageOrder

用户在调用 `api.tx.market.placeStorageOrder` 下单时，如果下单的 CID 是一个 Folder 并且希望 Sub Folders & Files 被 IPFS Scan 索引到，则在 `memo` 字段附上对应的信息，例如：

```json
{
    withRefs: true,
    origins: [
        "/ip4/203.0.113.142/tcp/4001/p2p/QmSourcePeerId",
        "/ip4/203.0.113.114/udp/4001/quic/p2p/QmSourcePeerId"
    ]
}
```

其中：

- `withRefs`：是否有 Refs 或者 Links。如果为 True，表示下单的 CID 代表一个 Folder，可以通过 Http API [/api/v0/refs](https://docs.ipfs.tech/reference/kubo/rpc/#api-v0-refs) 来获取所有 Sub Folders & Files 的 CID 列表

- `origins`：`Optional`，仅在 `withRefs: true` 时有意义。代表从哪些 IPFS Node 可以找到下单的 CID 代表的 Folder。格式为 [multiaddr](https://docs.ipfs.io/concepts/glossary/#multiaddr)，字段命名参考了 IPFS Pinning Service API Spec 里的 [Pin.origins](https://ipfs.github.io/pinning-services-api-spec/#section/Provider-hints/Pin.origins)


## Crust Order Indexing Service

### 主体逻辑

- 监测 Crust Mainnet 所有 Order，建立数据库索引

- 如果 `memo.withRefs` 为 true，则:

  - 调用本地 IPFS Node 的 `/api/v0/swarm/connect` API，与 `memo.origins` 里的 IPFS Nodes 建立连接
  
  - 调用本地 IFPS Node 的 `/api/v0/refs` API，获取文件夹的子目录和文件 CID 列表，索引进数据库
  
### Notes

- 一个文件或者文件夹，可能会被包含在多个 Folder Order，所以 CID -> Order 的查询，返回值是一个 Order 列表

- Order 之间没有先后顺序，可以使用 `thread pool` 来并发索引


# 开发任务 (MVP)

- **Curst Order Indexing Service**

- **Crust Pinning Service**，打包下单时填充 `memo` 字段

- **IPFS Scan**，调用新的 **Curst Order Indexing Service** API，支持查询打包下单场景

- (Optional) **Crust Wiki Updates**
