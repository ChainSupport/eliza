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

#### 2. USER_ASSETS_BALANCE （address-assets-balance.ts）
* 查询DOT
  input
  ``` 
  Get my wallet's native DOT balance
  ```

* 查询多资产
* subscan 显示真实余额



#### 3. TRANSFER_ASSETS (assets-transfer.ts)

* 转账DOT
* 转账多资产
* subscan显示转账记录
#### 4. SEND_MESSAGE_WITH_NO_TRANSFER (send-message.ts)
* 发送消息
* 在subscan查看消息 （说明已经发送并且加密）

#### 5. MY_WALLET_HISTORY (my-wallet-history.ts)

* 看到3和4所有记录， 并且均解密

#### 6. GET_TRANSFER_DETAIL_BY_HASH (get_transfer_detail_by_hash.ts)
* 看到转账记录， 并且解密

#### 7. 证明to地址可以解密消息(直接使用 MY_WALLET_HISTORY)
