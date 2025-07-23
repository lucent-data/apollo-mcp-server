<div align="center">
<a href="https://www.apollographql.com/"><img src="https://raw.githubusercontent.com/apollographql/apollo-client-devtools/main/assets/apollo-wordmark.svg" height="100" alt="Apollo Client"></a>
</div>

# Apollo MCP Server

An [MCP](https://modelcontextprotocol.io/) Server to expose GraphQL operations as MCP tools.

See [the documentation](https://www.apollographql.com/docs/apollo-mcp-server/) for details.

## Modification Notice

This is a modified version of the Apollo MCP Server that enables **Authorization header pass-through**. This allows the MCP client to send a Bearer token which is automatically forwarded by the MCP server to the backend GraphQL service for authentication and authorization, enabling seamless integration with protected APIs that require user authentication.

## Installation & Usage

### Prerequisites

- [Rust](https://rustup.rs/) (latest stable version)

### Building the Server

1. Clone this repository:

   ```bash
   git clone <repository-url>
   cd apollo-mcp-server
   ```

2. Build the project:
   ```bash
   cargo build --release
   ```

### Running the Server

Run the server with your GraphQL schema and endpoint:

```bash
./target/release/apollo-mcp-server \
  --schema path/to/your/schema.graphql \
  --endpoint http://your-graphql-endpoint \
  --http-port 5000 \
  --introspection \
  --operations path/to/your/operations \
  --allow-mutations all \
  --log debug
```

#### Configuration Options

- `--schema`: Path to your GraphQL schema file (required, unless using Apollo registry)
- `--endpoint`: Base URL of your GraphQL endpoint (optional, defaults to `http://127.0.0.1:4000`)
- `--http-port`: Port for HTTP transport (optional, enables HTTP mode; defaults to `5000` if specified)
- `--introspection`: Enable GraphQL introspection (optional)
- `--operations`: Path to directory containing GraphQL operation files (optional, but either this or `--introspection` must be provided)
- `--allow-mutations`: Controls mutation permissions (`all`, `none`, or specific operations) (optional, defaults to `none`)
- `--log`: Log level (`debug`, `info`, `warn`, `error`) (optional, defaults to `info`)

_Note: This is a selection of the most commonly used configuration options. Run `./target/release/apollo-mcp-server --help` to see all available options._

**Transport Modes:**
Specifying either the SSE port or address (or both) will enable the SSE transport. Specifying either the HTTP port or address (or both) will enable the Streamable HTTP transport.

# Licensing

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for the full license text.
