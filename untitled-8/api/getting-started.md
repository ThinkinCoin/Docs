# Getting Started

## Fantom GraphQL API <a id="fantom-graphql-api"></a>

Purpose of the API server is to provide high performance [GraphQL](https://graphql.org/) API for Fantom powered blockchain network. Our aim is to offer access to both low level as well as aggregated blockchain data for remote clients. Client developers can concentrate on their app business logic, instead of dealing with complexity of data and entity relationship inside the Opera blockchain.

The API server is published on [fantom-api-graphql](https://github.com/Fantom-foundation/fantom-api-graphql) GitHub repository. Feel free to download and deploy your copy of the application. We are actively developing the project and adding new features so it's worth checking the recent development even if you already checked the repository before.

An example of implementation of a client using this API is our new Opera browser [Fantom Vision](https://vision.fantom.rocks/). It's source code is also publicly available in our GitHub projects collection. Please check [fantom-ui](https://github.com/Fantom-foundation/fantom-ui) GitHub repository for more information.

We also support standard Ethereum Web3 API. Use websocket provider with our public API address [wss://wsapi.fantom.network](wss://wsapi.fantom.network/) to interact with Fantom Opera blockchain using Web3 client library.

## Technology <a id="technology"></a>

We use several pieces of technology to make the API work. If your intention is to run your own copy of it, please check our setup and make sure you are familiar with using these technologies at least on rudimentary level before you continue.

First, you will need access to Opera Lachesis full node RPC interface. You can use properly configured remote one, but it would significantly affect performance and potentially also security of your deployment. Please consider security implications of opening Lachesis RPC to outside access. Especially if you enable "personal" commands on your node while keeping your account keys in the Lachesis key store. We recommend using local IPC channel for communication between a Lachesis node and the API server. The IPC interface is available by default. Please check the [Lachesis launch instructions](https://github.com/Fantom-foundation/lachesis_launch) as well as [Lachesis repository](https://github.com/Fantom-foundation/go-lachesis) for deployment and configuration details.

Some aggregated and relationship data are kept off-chain in a [mongoDB](https://www.mongodb.com/) database. Especially the kind of data not easily accessible through basic node RPC interface. For example references between account and it's transaction history, or transaction position in time. The database is initialized by the API server, populated with historical data and kept in sync with the full node by internal subscriptions. You don't have to deal with extra database management, but you need to prepare well configured and reliable database connection address to the API server.

Finally, the server itself is developed using [Go](https://golang.org/), excellent, fast and secure programming language. You will need to install and configure Go development environment to be able to build your copy of the API server. Please follow the [official installation instructions](https://golang.org/doc/install).

