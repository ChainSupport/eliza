
## Configure Your Environment

### Environment Requirements

#### Local (if you run the agent on your machine)
1. [node](https://nodejs.org/en/download) version v23.3.0 (or version >= v23.3.0)
2. [bun](https://bun.com/docs/installation) latest release

#### Docker (if you run the agent in Docker)
No additional requirements

### Create the `.env` file

```
git clone https://github.com/ChainSupport/eliza.git
cd eliza
cp .env.example.env .env
```

Then set the variables below in `.env`:

```
OPENROUTER_API_KEY=
OPENAI_API_KEY=
ASSET_HUB_PRIVATE_KEY=
```

Run the command below to load the variables into your current shell session:

```
export $(grep -v '^#' .env | xargs)
```

### Run the Agent (choose one option)

#### 1. Run locally

Install the ElizaOS CLI globally:
```
bun install -g @elizaos/cli
```

Start the agent:
```
elizaos start
```

#### 2. Run with Docker
```
docker-compose up --build
```

### Interact with the Polkadot Asset Hub Agent

Visit [http://localhost:3000/](http://localhost:3000/)

Create a new chat and start asking questions:

![new chat](./images/new-chat.jpg)

### Testing
