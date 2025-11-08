# Eliza-Polkadot-Assethub-Agent

## Configure Your Environment

### Create the `.env` file


```
git clone https://github.com/ChainSupport/eliza.git
cd eliza
cp .env.example.env ./env
```
Then set the variables below in the `.env` file:

```
OPENROUTER_API_KEY=
OPENAI_API_KEY=
ASSET_HUB_PRIVATE_KEY=

```

Run the command below to load the variables into the current shell session:

```
export $(grep -v '^#' .env | xargs)
```

### Run the agent (choose one option)

#### 1. Run locally
```
elizaos start
```

#### 2. Run with Docker
```
docker-compose up --build
```

### Interact with the Polkadot Asset Hub Agent

Visit [http://localhost:3000/](http://localhost:3000/)

Then create a new chat and ask questions:

![new chat](./docs/images/new-chat.jpg)

#### Ask Question For Example

1. Agent abilities
![abilities](./docs/images/first-question.jpg)

2. My wallet Info
![address](./docs/images/my-address.jpg)

3. Transfer with encrpyto Memo

![trasnfer](./docs/images/transfer.jpg)

> see transfer detail [https://assethub-polkadot.subscan.io/extrinsic/0x5ec0784fe5475f7d4a4cd70a4acce0f498376728a770cf534e349db83127e197](https://assethub-polkadot.subscan.io/extrinsic/0x5ec0784fe5475f7d4a4cd70a4acce0f498376728a770cf534e349db83127e197)
## License

This project is licensed under the Apache License 2.0. See the `LICENSE` file for details.
