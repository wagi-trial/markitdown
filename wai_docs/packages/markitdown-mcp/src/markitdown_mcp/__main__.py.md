# packages/markitdown-mcp/src/markitdown_mcp/__main__.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown-mcp/src/markitdown_mcp/__main__.py",
  "file_hash": "2b33917f57322244252f318de6afa30b8f0903eac4ce9cc3f892788f16b70e27",
  "last_updated": "2025-12-23T15:44:24.120857+00:00",
  "functions": {
    "convert_to_markdown": {
      "hash": "3460dfd33ac1fa9acf6cb746b86123b719e614c5d7432a61e2b911717316df1d",
      "lines": "21-25",
      "last_updated": "2025-12-23T15:44:12.330901+00:00"
    },
    "check_plugins_enabled": {
      "hash": "7b60be0fcb1e4d3802f28b905c2399fba99da24f3f65f86365bdb5e53f7e128b",
      "lines": "26-33",
      "last_updated": "2025-12-23T15:44:15.010473+00:00"
    },
    "create_starlette_app": {
      "hash": "e85e4b4618322079619d26b1fdab49d32c465f697648d81cecb4a7b0bb3e728e",
      "lines": "34-81",
      "last_updated": "2025-12-23T15:44:19.322141+00:00"
    },
    "main": {
      "hash": "473aa1dd459c94a49c75c15441d36ce8af757901ba514407b85431cb7b232e74",
      "lines": "82-125",
      "last_updated": "2025-12-23T15:44:24.120785+00:00"
    }
  }
}
```

</details>



The Python file `__main__.py` in the `markitdown_mcp` package implements a server for converting resources to Markdown format using the MarkItDown library. It initializes a FastMCP server and defines an asynchronous tool for converting URIs to Markdown. The server can operate in two modes: using Streamable HTTP with Server-Sent Events (SSE) or standard input/output (STDIO). The main entry point of the file is the `main` function, which parses command-line arguments to configure server behavior and starts the appropriate server based on the provided options.

The main functions in this file include `convert_to_markdown`, which takes a URI as input and returns its Markdown representation, utilizing the `MarkItDown` class. The `check_plugins_enabled` function checks the environment variable `MARKITDOWN_ENABLE_PLUGINS` to determine if plugins are enabled. The `create_starlette_app` function constructs a Starlette application that handles SSE and Streamable HTTP requests, setting up appropriate routes and a lifespan context manager for session management. The file also imports several modules, including `contextlib`, `sys`, `os`, `uvicorn`, and components from the `starlette` framework, as well as the `mcp` library for server functionality.

The code manipulates various data structures and types, including the `Starlette` application instance, `Request`, `Scope`, and `Send` types from the `starlette` library. It also defines an asynchronous context manager for managing the lifespan of the application, ensuring proper resource management during server operation. The command-line argument parsing is handled using the `argparse` module, allowing for flexible configuration of server parameters such as host and port.

## Functions and Classes

## `convert_to_markdown`

**Location:** [`packages/markitdown-mcp/src/markitdown_mcp/__main__.py:21`](/packages/markitdown-mcp/src/markitdown_mcp/__main__.py#L21-L25)

# Function Documentation: `convert_to_markdown`

## Description
The `convert_to_markdown` function converts a resource specified by a URI into Markdown format. It supports URIs that begin with `http:`, `https:`, `file:`, or `data:`. The function utilizes the `MarkItDown` class to perform the conversion, enabling plugins based on the result of the `check_plugins_enabled()` function.

## Parameters
- `uri` (str): 
  - A string representing the URI of the resource to be converted.
  - Constraints: The URI must be a valid string that begins with one of the following prefixes: `http:`, `https:`, `file:`, or `data:`.

## Return Value
- Returns a string that contains the Markdown representation of the resource specified by the `uri`.

## Dependencies
- The function relies on the following external components:
  - `MarkItDown`: A class that provides functionality to convert URIs to Markdown.
  - `check_plugins_enabled()`: A function that returns a boolean indicating whether plugins are enabled for the `MarkItDown` conversion process.

## Usage Example
```python
markdown_content = await convert_to_markdown("https://example.com/resource")
```

---
## `check_plugins_enabled`

**Location:** [`packages/markitdown-mcp/src/markitdown_mcp/__main__.py:26`](/packages/markitdown-mcp/src/markitdown_mcp/__main__.py#L26-L33)

# Function Documentation: check_plugins_enabled

## Description
The `check_plugins_enabled` function checks the environment variable `MARKITDOWN_ENABLE_PLUGINS` to determine if plugins are enabled. It returns `True` if the value of the environment variable, after being stripped of whitespace and converted to lowercase, matches any of the following strings: `"true"`, `"1"`, or `"yes"`. Otherwise, it returns `False`.

## Parameters
This function does not take any parameters.

- **Type**: None
- **Constraints**: None
- **Usage**: The function does not utilize any input parameters.

## Return Value
- **Type**: `bool`
- **Content**: The function returns `True` if the environment variable `MARKITDOWN_ENABLE_PLUGINS` is set to a value that, when stripped of whitespace and converted to lowercase, is either `"true"`, `"1"`, or `"yes"`. It returns `False` for any other value or if the environment variable is not set.

## Dependencies
The function explicitly depends on the following external module:
- `os`: This module is used to access the environment variable.

## Usage Example
To invoke the function, simply call it without any arguments:

```python
enabled = check_plugins_enabled()
print(enabled)  # This will print True or False based on the environment variable.
```

---
## `create_starlette_app`

**Location:** [`packages/markitdown-mcp/src/markitdown_mcp/__main__.py:34`](/packages/markitdown-mcp/src/markitdown_mcp/__main__.py#L34-L81)

# Documentation for `create_starlette_app`

## Function Overview
The `create_starlette_app` function creates and configures a Starlette application. It sets up server-sent events (SSE) and a session manager for handling HTTP requests.

## Parameters

### `mcp_server`
- **Type**: `Server`
- **Description**: An instance of the `Server` class that is used to handle incoming streams and manage application logic.

### `debug`
- **Type**: `bool`
- **Default**: `False`
- **Description**: A flag that enables or disables debug mode for the Starlette application. When set to `True`, the application runs in debug mode.

## Return Value
- **Type**: `Starlette`
- **Description**: Returns an instance of the `Starlette` application configured with:
  - A route for handling SSE at `/sse` using the `handle_sse` function.
  - A mounted application for handling streamable HTTP requests at `/mcp` using the `handle_streamable_http` function.
  - A mounted application for handling messages at `/messages/` using the `sse.handle_post_message` method.
  - A lifespan context manager for managing the session lifecycle.

## Dependencies
The function relies on the following external modules and classes:
- `Starlette`: The main framework used to create the web application.
- `SseServerTransport`: A class used to manage server-sent events.
- `StreamableHTTPSessionManager`: A class that manages HTTP sessions and requests.
- `Request`, `Scope`, `Receive`, `Send`: Types used for handling incoming requests and responses.
- `contextlib.asynccontextmanager`: A utility for creating asynchronous context managers.
- `AsyncIterator`: Used in the lifespan context manager to yield control during the application lifecycle.

## Usage Example
```python
from your_module import create_starlette_app
from your_server_module import Server

# Create an instance of the Server
mcp_server_instance = Server()

# Create the Starlette application
app = create_starlette_app(mcp_server_instance, debug=True)
```

---
## `main`

**Location:** [`packages/markitdown-mcp/src/markitdown_mcp/__main__.py:82`](/packages/markitdown-mcp/src/markitdown_mcp/__main__.py#L82-L125)

# Function Documentation: main

## Description
The `main` function initializes and runs a MarkItDown MCP server. It utilizes command-line arguments to configure the server's behavior, including the transport method, host, and port. The function either runs the server using Streamable HTTP or SSE transport or falls back to a standard input/output method.

## Parameters
The `main` function does not take any parameters.

## Command-Line Arguments
The function accepts the following command-line arguments:

- `--http` (action: `store_true`): 
  - Type: Boolean
  - Default: `False`
  - Description: Enables the server to run with Streamable HTTP and SSE transport.

- `--sse` (action: `store_true`): 
  - Type: Boolean
  - Default: `False`
  - Description: Deprecated alias for `--http`.

- `--host`: 
  - Type: String
  - Default: `None`
  - Description: Specifies the host to bind to. Defaults to `127.0.0.1` if not provided.

- `--port`: 
  - Type: Integer
  - Default: `None`
  - Description: Specifies the port to listen on. Defaults to `3001` if not provided.

## Return Value
The `main` function does not return a value. It either starts the server or exits the program with an error message.

## Dependencies
The function explicitly imports and depends on the following external modules:
- `argparse`: Used for parsing command-line arguments.
- `uvicorn`: Used to run the server when Streamable HTTP or SSE transport is enabled.
- `mcp`: A module that provides the `_mcp_server` and `run` functions.
- `create_starlette_app`: A function that creates a Starlette application using the MCP server.

## Usage Example
To run the server with default settings:
```
python script.py
```

To run the server with Streamable HTTP on a specific host and port:
```
python script.py --http --host 0.0.0.0 --port 8080
```

To run the server with the deprecated SSE option:
```
python script.py --sse
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
