---
tags: [projects]
title: footage contracts comments
created: '2022-11-24T03:57:37.526Z'
modified: '2022-11-24T04:41:17.582Z'
---

footage contracts comments

# Overall comments

- migrations 部署脚本尚未完成

- test case 建议多补充些。一般 test case 需要覆盖所有能想到的正常和非正常场景

- 缺少 etherscan verification，可以研究下 truffle-plugin-verify 这个插件如何使用

- 通用的 ERC20 / ERC721 合约，可以使用 https://docs.openzeppelin.com/contracts/4.x/wizard 辅助生成

- 合约尽量支持可升级，升级一般使用 UUPS 模式，参考 https://docs.openzeppelin.com/contracts/4.x/api/proxy#UUPSUpgradeable

- .env 文件不要提交，可能会泄漏部署合约的私钥。通常将 .env 放在 .gitignore 里忽略掉，而提交一个 .env-sample 文件

- 合约的 `_owner` 地址不要显示地传入 contructor，在合约里可以直接通过 `msg.sender` 获取，这样也更安全。如果需要 transfer ownership，通常在合约里额外添加一个方法，这样 ownership 可以多次转移。

- Access Control 可以细化一些，多定义几个 Role。

- 合约帐户的 ETH Balance，应该是公开的，可以直接查，不需要单独提供 `balance()` 查询方法

- ETH 转帐，如果要支持转给合约地址的话，通常用 `call` 函数: 
  ```sol
  (bool success, ) = to.call{ value: value }("");
  ```






