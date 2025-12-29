### Environment Requirements

#### Local (if you run the agent on your machine)
1. [node](https://nodejs.org/en/download) version v23.3.0 (or version >= v23.3.0)
2. [bun](https://bun.com/docs/installation) latest release

#### Docker (if you run the agent in Docker)
No additional requirements

### Run the Agent (choose one option)
```
git clone https://github.com/ChainSupport/eliza.git
cd eliza
```
#### 1. Run locally

Create the `.env` file
```
cp .env.example.env .env
```
Then set the variables below in `.env`:

```
OPENROUTER_API_KEY=
OPENAI_API_KEY=
ASSET_HUB_PRIVATE_KEY=
```
Install the ElizaOS CLI globally:
```
bun install -g @elizaos/cli
```

Start the agent:
```
elizaos start
```

#### 2. Run with Docker
Set the variables below in `docker-compose.yaml`:

```
OPENROUTER_API_KEY=
OPENAI_API_KEY=
ASSET_HUB_PRIVATE_KEY=
```

```
docker-compose up --build
```

### 手动测试

#### 1. GET_MY_WALLET_INFO (get-my-wallet-info.ts)
  input:
  ```
  Get my wallet info
  ```
  output:
  ```
  My wallet address: 13GKHvBFjWuVjezV8cG6DMoK2FftY4awXXqKdunApnJGbvwd
  Native DOT balance: 0.1669384548
  Account URL: https://assethub-polkadot.subscan.io/account/13GKHvBFjWuVjezV8cG6DMoK2FftY4awXXqKdunApnJGbvwd
  ```
  ![My Wallet Info on eliza](./v1-images/my-wallet-info-eliza.png)
  在这里， 我们会获得我们的钱包地址以及链上余额， 测试通过.

#### 2. USER_ASSETS_BALANCE （address-assets-balance.ts）
##### 1. 查询DOT
  input:
  ``` 
  Get my wallet's native DOT balance
  ```
  output:
  ```
  My Native DOT balance on the Polkadot AssetHub is 0.1669384548
  Account URL: https://assethub-polkadot.subscan.io/account/13GKHvBFjWuVjezV8cG6DMoK2FftY4awXXqKdunApnJGbvwd
  ```
  ![My Native DOT Balance on eliza](./v1-images/my-dot-balance-eliza.png)
  ![My Native DOT Balance on subscan](./v1-images/my-dot-balance-subscan.png)
  在这里， 我们看到在eliza agent中显示的Native DOT余额与subscan相同，测试通过。
##### 2. 查询多资产 （DOTA）
  input:
  ```
  show my DOTA asset balance
  ```
  output:
  ```
  My Asset 18 balance on the Polkadot AssetHub is 5.3898
  Account URL: https://assethub-polkadot.subscan.io/account/13GKHvBFjWuVjezV8cG6DMoK2FftY4awXXqKdunApnJGbvwd
  ```
  ![My DOTA Balance on eliza](./v1-images/my-dota-balance-eliza.png)
  ![My DOTA Balance on ubscan](./v1-images/my-dota-balance-subscan.png)
  在这里， 我们看到在eliza agent中显示的DOTA余额与subscan相同，测试通过。

##### 3. 查询一个非法地址的余额 （地址格式错误）
input:
```
Get ddDBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit native DOT balance
```
output:
```
Invalid address or assetId: ddDBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit, null
```
查询失败， 符合预期。 测试通过。

#### 3. TRANSFER_ASSETS (assets-transfer.ts)

##### 1. 转账DOT
  input:
  ```
  Transfer 0.01 DOT to address 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit
  ```
  output:
  ```
  Transfer Native DOT to 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit successfully.
  Tx's id: 0x43c3da59fdc72082a42452459de1e8c37b93e1f968dbaf4d33631ec339794d82
  Extrinsic URL: https://assethub-polkadot.subscan.io/extrinsic/0x43c3da59fdc72082a42452459de1e8c37b93e1f968dbaf4d33631ec339794d82
  ```
  ![transfer dot on eliza](./v1-images/transfer-dot-eliza.png)
  点击 `Extrinsic URL`, 在subscan中看到交易
  ![transfer dot on subscan](./v1-images/transfer-dot-subscan.png)
  我们看到这笔交易已经上链， 并且在subscan中， 测试成功。

##### 2.  转账多资产
  input:
  ```
  ransfer 1 DOTA to address 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit
  ```
  output:
  ```
  Transfer Asset 18 to 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit successfully.
  Tx's id: 0xdbef006350ab62d2bca01692a312bfba5bbbb10193c821ac6f6d36a7f9562edc
  Extrinsic URL: https://assethub-polkadot.subscan.io/extrinsic/0xdbef006350ab62d2bca01692a312bfba5bbbb10193c821ac6f6d36a7f9562edc
  ```
  ![transfer dota on eliza](./v1-images/transfer-dota-eliza.png)
  ![transfer dota on subscan](./v1-images/transfer-dota-subscan.png)
  这笔交易成功， 并且在subscan中可以查询得到， 测试成功

#### 4. SEND_MESSAGE_WITH_NO_TRANSFER (send-message.ts)
input:
```
Send the message "Hello, nice to meet you!" to address 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit
```
output:
```
Send message 'Hello, nice to meet you!' to 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit successfully.
Tx's id: 0xfe578930c93064349ea1481da666483b81cc86aab59ac67011e63841c67bf3fa
Extrinsic URL: https://assethub-polkadot.subscan.io/extrinsic/0xfe578930c93064349ea1481da666483b81cc86aab59ac67011e63841c67bf3fa

```
![Send Message on eliza](./v1-images/send-message-eliza.png)
![Send Message on subscan](./v1-images/send-message-subscan.png)
我们看到消息已经发送到链上， 并且已经进行加密， 包含在e字段当中。测试成功

#### 5. GET_TRANSFER_DETAIL_BY_HASH (get_transfer_detail_by_hash.ts)

##### 1. 合法交易
在这里， 我们获取上一步那笔交易的详细信息。

input:
```
Show transaction 0xfe578930c93064349ea1481da666483b81cc86aab59ac67011e63841c67bf3fa details
```
output:
```
Get transfer detail by hash on the POLKADOT AssetHub successfully.
Detail:
Sender: 13GKHvBFjWuVjezV8cG6DMoK2FftY4awXXqKdunApnJGbvwd
Recipient: 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit
Token: DOT
Amount: 0
Fee: 0.0027061864 DOT
Memo: Hello, nice to meet you!
Time: 12/29/2025, 6:26:36 PM
TxId: 0xfe578930c93064349ea1481da666483b81cc86aab59ac67011e63841c67bf3fa
Extrinsic URL: https://assethub-polkadot.subscan.io/extrinsic/11003435-2
```
![Transaction Detail on eliza](./v1-images/transaction-details-eliza.png)
在这里， 我们已经查询到步骤4中的那笔加密交易， 并且解密加密消息。测试成功。

##### 2. 非法交易 （链上不存在）
在这里， 我们试着查询一笔链上不存在的交易。
input:
```
Get transaction 0xdbef006350ab62d2bca01692a312bfba5bbbb10193c821ac6f6d36a7f9562edd detail
```
output:
```
Failed to get transfer detail by hash on the POLKADOT AssetHub. error: TypeError: null is not an object (evaluating '(await (await fetch(url, options)).json()).data.extrinsic_index')
```
错误交易抛出错误， 符合预期。 测试通过

#### 6. MY_WALLET_HISTORY (my-wallet-history.ts)

input:
```
Get my wallet history
```
output:
```
Get my wallet history on the Polkadot AssetHub successfully.
History:

Type: Send
Sender: 13GKHvBFjWuVjezV8cG6DMoK2FftY4awXXqKdunApnJGbvwd
Recipient: 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit
Token: DOT
Amount: 0
Memo: Hello, nice to meet you!
Time: 12/29/2025, 6:26:36 PM
TxId: 0xfe578930c93064349ea1481da666483b81cc86aab59ac67011e63841c67bf3fa
Extrinsic URL: https://assethub-polkadot.subscan.io/extrinsic/11003435-2
Type: Send
Sender: 13GKHvBFjWuVjezV8cG6DMoK2FftY4awXXqKdunApnJGbvwd
Recipient: 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit
Token: DOTA
Amount: 1
Memo:

Time: 12/29/2025, 6:03:18 PM
TxId: 0xdbef006350ab62d2bca01692a312bfba5bbbb10193c821ac6f6d36a7f9562edc
Extrinsic URL: https://assethub-polkadot.subscan.io/extrinsic/11003206-2
Type: Send
Sender: 13GKHvBFjWuVjezV8cG6DMoK2FftY4awXXqKdunApnJGbvwd
Recipient: 15DBKxnn69eo4pYZQbD8geFXFQDC2qC51qhvBEKgEYviahit
Token: DOT
Amount: 0.01
Memo:

Time: 12/29/2025, 5:58:06 PM
TxId: 0x43c3da59fdc72082a42452459de1e8c37b93e1f968dbaf4d33631ec339794d82
Extrinsic URL: https://assethub-polkadot.subscan.io/extrinsic/11003155-2
```image.png
![my wallet history](./v1-images/my-wallet-history.png)

在这里， 我们看到了我们在上面发送的所有交易， 并且memo被解密。 测试成功

<!-- #### 7. 证明to地址可以解密消息(直接使用 MY_WALLET_HISTORY) -->
