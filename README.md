# Eliza-Polkadot-Assethub-Agent

## Configure Your Environment

### Create the `.env` file
```
touch .env
```
Then set the variables below in the `.env` file:

```
OPENROUTER_API_KEY=
OPENAI_API_KEY=
PGLITE_DATA_DIR=./.eliza/.elizadb
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

## License

This project is licensed under the Apache License 2.0. See the `LICENSE` file for details.
