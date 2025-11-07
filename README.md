# Eliza-Polkadot-Assethub-Agent

## Configure Your Environment

### Create the `.env` file
```
touch .env
```
Then set the variables below:

```
OPENROUTER_API_KEY=
OPENAI_API_KEY=
PGLITE_DATA_DIR=./.eliza/.elizadb
ASSET_HUB_PRIVATE_KEY=0x139ace2d79edcd1af5f5449e784e48b147bdc0f22598fbb0fe3c3f0e02a5c455

```

Run the command below to load the variables into the current shell session:

```
export $(grep -v '^#' .env | xargs)
```

### Run the agent (choose one option)

### 1. Run locally
```
elizaos start
```

### 2. Run with Docker
```
docker-compose up --build
```

## License

This project is licensed under the Apache License 2.0. See the `LICENSE` file for details.
