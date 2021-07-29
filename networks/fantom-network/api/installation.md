# Installation

## What you need <a id="what-you-need"></a>

Please note that an official binary distribution is not available at the moment. To build your own Fantom GraphQL API, you need to have following:

* Working [MongoDB](https://docs.mongodb.com/manual/installation/) database installation.
* Go version 1.13 or later [configured and ready](https://golang.org/doc/install).
* Fantom foundation [Lachesis full node](https://github.com/Fantom-foundation/go-lachesis) up and running on desired network.

You do have another option. For initial testing and development, you can use our own test playground. The API server is deployed at `https://xapi2.fantom.network/api` for regular GraphQL queries and`https://xapi2.fantom.network/graphql` for Web Socket subscriptions. Feel free to connect and try your queries. Fine tune your application before committing to deploy your own instance.

## Building process <a id="building-process"></a>

Building your API server is a fairly straight forward process. First clone the repository to your local machine. Do not clone the project into $GOPATH, due to the [Go modules](https://blog.golang.org/using-go-modules). Instead, use any other location.

```text
$ git clone https://github.com/Fantom-foundation/fantom-api-graphql.git
```

Once you have the copy on your machine, build the executable:

```text
$ cd fantom-api-graphql$ go build -o ./build/apiserver ./cmd/apiserver
```

The API server executable will be created in the folder of the project. You can change the location by changing the output path in the Go building command above.

To run your copy of the API server, simply run:

## Configuration <a id="configuration"></a>

The API server already contains some most common configuration options as default values and you don't have to change them most of the time. The default values are:

* The network binding address is **localhost.**
* Default listening port is **16761**.
* Default Lachesis IPC interface is **~/.lachesis/data/lachesis.ipc**.
* MongoDB connection address is **mongodb://localhost:27017**.
* Default logging level is **INFO**.

If you want to change one of the default values, you need to create a configuration file. The API server can read configuration options from several configuration formats, namely JSON, TOML, YAML, HCL, envfile and Java properties config files. Please choose the one you are most familiar with. The name of the configuration file is expected to be "apiserver" with extension which corresponds with the file format of your choosing.

Example YAML file looks like this:

```text
server:    bind: 127.0.0.1:16761    lachesis:    url: /var/opera/data/lachesis.ipclog:    level: Debugmongo:    url: mongodb://127.0.0.1:27017cors:    origins: *
```

You can keep the config file on with the API server executable, or you can save it on the home folder under the **.fantomapi** sub-folder. On MacOS the expected path is **Library/FantomApi**.

