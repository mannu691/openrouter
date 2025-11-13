# openrouter

Developer-friendly & type-safe Python SDK specifically catered to leverage *openrouter* API.

<div align="left" style="margin-bottom: 0;">
    <a href="https://www.speakeasy.com/?utm_source=openrouter&utm_campaign=python" class="badge-link">
        <span class="badge-container">
            <span class="badge-icon-section">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 30 30" fill="none" style="vertical-align: middle;"><title>Speakeasy Logo</title><path fill="currentColor" d="m20.639 27.548-19.17-2.724L0 26.1l20.639 2.931 8.456-7.336-1.468-.208-6.988 6.062Z"></path><path fill="currentColor" d="m20.639 23.1 8.456-7.336-1.468-.207-6.988 6.06-6.84-.972-9.394-1.333-2.936-.417L0 20.169l2.937.416L0 23.132l20.639 2.931 8.456-7.334-1.468-.208-6.986 6.062-9.78-1.39 1.468-1.273 8.31 1.18Z"></path><path fill="currentColor" d="m20.639 18.65-19.17-2.724L0 17.201l20.639 2.931 8.456-7.334-1.468-.208-6.988 6.06Z"></path><path fill="currentColor" d="M27.627 6.658 24.69 9.205 20.64 12.72l-7.923-1.126L1.469 9.996 0 11.271l11.246 1.596-1.467 1.275-8.311-1.181L0 14.235l20.639 2.932 8.456-7.334-2.937-.418 2.937-2.549-1.468-.208Z"></path><path fill="currentColor" d="M29.095 3.902 8.456.971 0 8.305l20.639 2.934 8.456-7.337Z"></path></svg>
            </span>
            <span class="badge-text badge-text-section">BUILT BY SPEAKEASY</span>
        </span>
    </a>
    <a href="https://opensource.org/licenses/MIT" class="badge-link">
        <span class="badge-container blue">
            <span class="badge-text badge-text-section">LICENSE // MIT</span>
        </span>
    </a>
</div>


<br /><br />
> [!IMPORTANT]
> This SDK is not yet ready for production use. To complete setup please follow the steps outlined in your [workspace](https://app.speakeasy.com/org/openrouter/sdk). Delete this section before > publishing to a package manager.

<!-- Start Summary [summary] -->
## Summary

OpenRouter API: OpenAI-compatible Chat Completions and Completions API with additional OpenRouter features

For more information about the API: [OpenRouter Documentation](https://openrouter.ai/docs)
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [openrouter](#openrouter)
  * [SDK Installation](#sdk-installation)
  * [IDE Support](#ide-support)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Server-sent event streaming](#server-sent-event-streaming)
  * [Retries](#retries)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
  * [Custom HTTP Client](#custom-http-client)
  * [Resource Management](#resource-management)
  * [Debugging](#debugging)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

> [!TIP]
> To finish publishing your SDK to PyPI you must [run your first generation action](https://www.speakeasy.com/docs/github-setup#step-by-step-guide).


> [!NOTE]
> **Python version upgrade policy**
>
> Once a Python version reaches its [official end of life date](https://devguide.python.org/versions/), a 3-month grace period is provided for users to upgrade. Following this grace period, the minimum python version supported in the SDK will be updated.

The SDK can be installed with *uv*, *pip*, or *poetry* package managers.

### uv

*uv* is a fast Python package installer and resolver, designed as a drop-in replacement for pip and pip-tools. It's recommended for its speed and modern Python tooling capabilities.

```bash
uv add git+<UNSET>.git
```

### PIP

*PIP* is the default package installer for Python, enabling easy installation and management of packages from PyPI via the command line.

```bash
pip install git+<UNSET>.git
```

### Poetry

*Poetry* is a modern tool that simplifies dependency management and package publishing by using a single `pyproject.toml` file to handle project metadata and dependencies.

```bash
poetry add git+<UNSET>.git
```

### Shell and script usage with `uv`

You can use this SDK in a Python shell with [uv](https://docs.astral.sh/uv/) and the `uvx` command that comes with it like so:

```shell
uvx --from openrouter python
```

It's also possible to write a standalone Python script without needing to set up a whole project like so:

```python
#!/usr/bin/env -S uv run --script
# /// script
# requires-python = ">=3.9"
# dependencies = [
#     "openrouter",
# ]
# ///

from openrouter import OpenRouter

sdk = OpenRouter(
  # SDK arguments
)

# Rest of script here...
```

Once that is saved to a file, you can run it with `uv run script.py` where
`script.py` can be replaced with the actual file name.
<!-- End SDK Installation [installation] -->

<!-- Start IDE Support [idesupport] -->
## IDE Support

### PyCharm

Generally, the SDK will work well with most IDEs out of the box. However, when using PyCharm, you can enjoy much better integration with Pydantic by installing an additional plugin.

- [PyCharm Pydantic Plugin](https://docs.pydantic.dev/latest/integrations/pycharm/)
<!-- End IDE Support [idesupport] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

```python
# Synchronous Example
from openrouter import OpenRouter
import os


with OpenRouter(
    api_key=os.getenv("OPENROUTER_API_KEY", ""),
) as open_router:

    res = open_router.beta.responses.send(input=[
        {
            "type": "message",
            "role": "user",
            "content": "Hello, how are you?",
        },
    ], metadata={
        "user_id": "123",
        "session_id": "abc-def-ghi",
    }, tools=[
        {
            "type": "function",
            "name": "get_current_weather",
            "description": "Get the current weather in a given location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                    },
                },
            },
        },
    ], model="anthropic/claude-4.5-sonnet-20250929", text={
        "format_": {
            "type": "text",
        },
        "verbosity": "medium",
    }, reasoning={
        "summary": "auto",
        "enabled": True,
    }, temperature=0.7, top_p=0.9, prompt={
        "id": "<id>",
        "variables": {
            "key": {
                "type": "input_text",
                "text": "Hello, how can I help you?",
            },
        },
    }, service_tier="auto", truncation="auto", stream=False, provider={
        "data_collection": "deny",
        "zdr": True,
        "enforce_distillable_text": True,
        "order": [
            "OpenAI",
        ],
        "only": [
            "OpenAI",
        ],
        "ignore": [
            "OpenAI",
        ],
        "quantizations": None,
        "sort": "price",
    })

    with res as event_stream:
        for event in event_stream:
            # handle event
            print(event, flush=True)
```

</br>

The same SDK client can also be used to make asynchronous requests by importing asyncio.

```python
# Asynchronous Example
import asyncio
from openrouter import OpenRouter
import os

async def main():

    async with OpenRouter(
        api_key=os.getenv("OPENROUTER_API_KEY", ""),
    ) as open_router:

        res = await open_router.beta.responses.send_async(input=[
            {
                "type": "message",
                "role": "user",
                "content": "Hello, how are you?",
            },
        ], metadata={
            "user_id": "123",
            "session_id": "abc-def-ghi",
        }, tools=[
            {
                "type": "function",
                "name": "get_current_weather",
                "description": "Get the current weather in a given location",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "location": {
                            "type": "string",
                        },
                    },
                },
            },
        ], model="anthropic/claude-4.5-sonnet-20250929", text={
            "format_": {
                "type": "text",
            },
            "verbosity": "medium",
        }, reasoning={
            "summary": "auto",
            "enabled": True,
        }, temperature=0.7, top_p=0.9, prompt={
            "id": "<id>",
            "variables": {
                "key": {
                    "type": "input_text",
                    "text": "Hello, how can I help you?",
                },
            },
        }, service_tier="auto", truncation="auto", stream=False, provider={
            "data_collection": "deny",
            "zdr": True,
            "enforce_distillable_text": True,
            "order": [
                "OpenAI",
            ],
            "only": [
                "OpenAI",
            ],
            "ignore": [
                "OpenAI",
            ],
            "quantizations": None,
            "sort": "price",
        })

        async with res as event_stream:
            async for event in event_stream:
                # handle event
                print(event, flush=True)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name      | Type | Scheme      | Environment Variable |
| --------- | ---- | ----------- | -------------------- |
| `api_key` | http | HTTP Bearer | `OPENROUTER_API_KEY` |

To authenticate with the API the `api_key` parameter must be set when initializing the SDK client instance. For example:
```python
from openrouter import OpenRouter
import os


with OpenRouter(
    api_key=os.getenv("OPENROUTER_API_KEY", ""),
) as open_router:

    res = open_router.beta.responses.send(input=[
        {
            "type": "message",
            "role": "user",
            "content": "Hello, how are you?",
        },
    ], metadata={
        "user_id": "123",
        "session_id": "abc-def-ghi",
    }, tools=[
        {
            "type": "function",
            "name": "get_current_weather",
            "description": "Get the current weather in a given location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                    },
                },
            },
        },
    ], model="anthropic/claude-4.5-sonnet-20250929", text={
        "format_": {
            "type": "text",
        },
        "verbosity": "medium",
    }, reasoning={
        "summary": "auto",
        "enabled": True,
    }, temperature=0.7, top_p=0.9, prompt={
        "id": "<id>",
        "variables": {
            "key": {
                "type": "input_text",
                "text": "Hello, how can I help you?",
            },
        },
    }, service_tier="auto", truncation="auto", stream=False, provider={
        "data_collection": "deny",
        "zdr": True,
        "enforce_distillable_text": True,
        "order": [
            "OpenAI",
        ],
        "only": [
            "OpenAI",
        ],
        "ignore": [
            "OpenAI",
        ],
        "quantizations": None,
        "sort": "price",
    })

    with res as event_stream:
        for event in event_stream:
            # handle event
            print(event, flush=True)

```

### Per-Operation Security Schemes

Some operations in this SDK require the security scheme to be specified at the request level. For example:
```python
from openrouter import OpenRouter, models
import os


with OpenRouter() as open_router:

    res = open_router.credits.create_coinbase_charge(security=models.CreateCoinbaseChargeSecurity(
        bearer=os.getenv("OPENROUTER_BEARER", ""),
    ), amount=100, sender="0x1234567890123456789012345678901234567890", chain_id=1)

    # Handle response
    print(res)

```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [analytics](docs/sdks/analytics/README.md)

* [get_user_activity](docs/sdks/analytics/README.md#get_user_activity) - Get user activity grouped by endpoint

### [api_keys](docs/sdks/apikeys/README.md)

* [list](docs/sdks/apikeys/README.md#list) - List API keys
* [create](docs/sdks/apikeys/README.md#create) - Create a new API key
* [update](docs/sdks/apikeys/README.md#update) - Update an API key
* [delete](docs/sdks/apikeys/README.md#delete) - Delete an API key
* [get](docs/sdks/apikeys/README.md#get) - Get a single API key
* [get_current_key_metadata](docs/sdks/apikeys/README.md#get_current_key_metadata) - Get current API key

#### [beta.responses](docs/sdks/responses/README.md)

* [send](docs/sdks/responses/README.md#send) - Create a response

### [chat](docs/sdks/chat/README.md)

* [send](docs/sdks/chat/README.md#send) - Create a chat completion

### [completions](docs/sdks/completions/README.md)

* [generate](docs/sdks/completions/README.md#generate) - Create a completion

### [credits](docs/sdks/credits/README.md)

* [get_credits](docs/sdks/credits/README.md#get_credits) - Get remaining credits
* [create_coinbase_charge](docs/sdks/credits/README.md#create_coinbase_charge) - Create a Coinbase charge for crypto payment

### [embeddings](docs/sdks/embeddings/README.md)

* [generate](docs/sdks/embeddings/README.md#generate) - Submit an embedding request
* [list_models](docs/sdks/embeddings/README.md#list_models) - List all embeddings models

### [endpoints](docs/sdks/endpoints/README.md)

* [list](docs/sdks/endpoints/README.md#list) - List all endpoints for a model
* [list_zdr_endpoints](docs/sdks/endpoints/README.md#list_zdr_endpoints) - Preview the impact of ZDR on the available endpoints

### [generations](docs/sdks/generations/README.md)

* [get_generation](docs/sdks/generations/README.md#get_generation) - Get request & usage metadata for a generation

### [models](docs/sdks/models/README.md)

* [count](docs/sdks/models/README.md#count) - Get total count of available models
* [list](docs/sdks/models/README.md#list) - List all models and their properties
* [list_for_user](docs/sdks/models/README.md#list_for_user) - List models filtered by user provider preferences

### [o_auth](docs/sdks/oauth/README.md)

* [exchange_auth_code_for_api_key](docs/sdks/oauth/README.md#exchange_auth_code_for_api_key) - Exchange authorization code for API key
* [create_auth_code](docs/sdks/oauth/README.md#create_auth_code) - Create authorization code

### [parameters](docs/sdks/parameters/README.md)

* [get_parameters](docs/sdks/parameters/README.md#get_parameters) - Get a model's supported parameters and data about which are most popular

### [providers](docs/sdks/providers/README.md)

* [list](docs/sdks/providers/README.md#list) - List all providers

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Server-sent event streaming [eventstream] -->
## Server-sent event streaming

[Server-sent events][mdn-sse] are used to stream content from certain
operations. These operations will expose the stream as [Generator][generator] that
can be consumed using a simple `for` loop. The loop will
terminate when the server no longer has any events to send and closes the
underlying connection.  

The stream is also a [Context Manager][context-manager] and can be used with the `with` statement and will close the
underlying connection when the context is exited.

```python
from openrouter import OpenRouter
import os


with OpenRouter(
    api_key=os.getenv("OPENROUTER_API_KEY", ""),
) as open_router:

    res = open_router.beta.responses.send(input=[
        {
            "type": "message",
            "role": "user",
            "content": "Hello, how are you?",
        },
    ], metadata={
        "user_id": "123",
        "session_id": "abc-def-ghi",
    }, tools=[
        {
            "type": "function",
            "name": "get_current_weather",
            "description": "Get the current weather in a given location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                    },
                },
            },
        },
    ], model="anthropic/claude-4.5-sonnet-20250929", text={
        "format_": {
            "type": "text",
        },
        "verbosity": "medium",
    }, reasoning={
        "summary": "auto",
        "enabled": True,
    }, temperature=0.7, top_p=0.9, prompt={
        "id": "<id>",
        "variables": {
            "key": {
                "type": "input_text",
                "text": "Hello, how can I help you?",
            },
        },
    }, service_tier="auto", truncation="auto", stream=False, provider={
        "data_collection": "deny",
        "zdr": True,
        "enforce_distillable_text": True,
        "order": [
            "OpenAI",
        ],
        "only": [
            "OpenAI",
        ],
        "ignore": [
            "OpenAI",
        ],
        "quantizations": None,
        "sort": "price",
    })

    with res as event_stream:
        for event in event_stream:
            # handle event
            print(event, flush=True)

```

[mdn-sse]: https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events
[generator]: https://book.pythontips.com/en/latest/generators.html
[context-manager]: https://book.pythontips.com/en/latest/context_managers.html
<!-- End Server-sent event streaming [eventstream] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply provide a `RetryConfig` object to the call:
```python
from openrouter import OpenRouter
from openrouter.utils import BackoffStrategy, RetryConfig
import os


with OpenRouter(
    api_key=os.getenv("OPENROUTER_API_KEY", ""),
) as open_router:

    res = open_router.beta.responses.send(input=[
        {
            "type": "message",
            "role": "user",
            "content": "Hello, how are you?",
        },
    ], metadata={
        "user_id": "123",
        "session_id": "abc-def-ghi",
    }, tools=[
        {
            "type": "function",
            "name": "get_current_weather",
            "description": "Get the current weather in a given location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                    },
                },
            },
        },
    ], model="anthropic/claude-4.5-sonnet-20250929", text={
        "format_": {
            "type": "text",
        },
        "verbosity": "medium",
    }, reasoning={
        "summary": "auto",
        "enabled": True,
    }, temperature=0.7, top_p=0.9, prompt={
        "id": "<id>",
        "variables": {
            "key": {
                "type": "input_text",
                "text": "Hello, how can I help you?",
            },
        },
    }, service_tier="auto", truncation="auto", stream=False, provider={
        "data_collection": "deny",
        "zdr": True,
        "enforce_distillable_text": True,
        "order": [
            "OpenAI",
        ],
        "only": [
            "OpenAI",
        ],
        "ignore": [
            "OpenAI",
        ],
        "quantizations": None,
        "sort": "price",
    },
        RetryConfig("backoff", BackoffStrategy(1, 50, 1.1, 100), False))

    with res as event_stream:
        for event in event_stream:
            # handle event
            print(event, flush=True)

```

If you'd like to override the default retry strategy for all operations that support retries, you can use the `retry_config` optional parameter when initializing the SDK:
```python
from openrouter import OpenRouter
from openrouter.utils import BackoffStrategy, RetryConfig
import os


with OpenRouter(
    retry_config=RetryConfig("backoff", BackoffStrategy(1, 50, 1.1, 100), False),
    api_key=os.getenv("OPENROUTER_API_KEY", ""),
) as open_router:

    res = open_router.beta.responses.send(input=[
        {
            "type": "message",
            "role": "user",
            "content": "Hello, how are you?",
        },
    ], metadata={
        "user_id": "123",
        "session_id": "abc-def-ghi",
    }, tools=[
        {
            "type": "function",
            "name": "get_current_weather",
            "description": "Get the current weather in a given location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                    },
                },
            },
        },
    ], model="anthropic/claude-4.5-sonnet-20250929", text={
        "format_": {
            "type": "text",
        },
        "verbosity": "medium",
    }, reasoning={
        "summary": "auto",
        "enabled": True,
    }, temperature=0.7, top_p=0.9, prompt={
        "id": "<id>",
        "variables": {
            "key": {
                "type": "input_text",
                "text": "Hello, how can I help you?",
            },
        },
    }, service_tier="auto", truncation="auto", stream=False, provider={
        "data_collection": "deny",
        "zdr": True,
        "enforce_distillable_text": True,
        "order": [
            "OpenAI",
        ],
        "only": [
            "OpenAI",
        ],
        "ignore": [
            "OpenAI",
        ],
        "quantizations": None,
        "sort": "price",
    })

    with res as event_stream:
        for event in event_stream:
            # handle event
            print(event, flush=True)

```
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

[`OpenRouterError`](./src/openrouter/errors/openroutererror.py) is the base class for all HTTP error responses. It has the following properties:

| Property           | Type             | Description                                                                             |
| ------------------ | ---------------- | --------------------------------------------------------------------------------------- |
| `err.message`      | `str`            | Error message                                                                           |
| `err.status_code`  | `int`            | HTTP response status code eg `404`                                                      |
| `err.headers`      | `httpx.Headers`  | HTTP response headers                                                                   |
| `err.body`         | `str`            | HTTP body. Can be empty string if no body is returned.                                  |
| `err.raw_response` | `httpx.Response` | Raw HTTP response                                                                       |
| `err.data`         |                  | Optional. Some errors may contain structured data. [See Error Classes](#error-classes). |

### Example
```python
from openrouter import OpenRouter, errors
import os


with OpenRouter(
    api_key=os.getenv("OPENROUTER_API_KEY", ""),
) as open_router:
    res = None
    try:

        res = open_router.beta.responses.send(input=[
            {
                "type": "message",
                "role": "user",
                "content": "Hello, how are you?",
            },
        ], metadata={
            "user_id": "123",
            "session_id": "abc-def-ghi",
        }, tools=[
            {
                "type": "function",
                "name": "get_current_weather",
                "description": "Get the current weather in a given location",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "location": {
                            "type": "string",
                        },
                    },
                },
            },
        ], model="anthropic/claude-4.5-sonnet-20250929", text={
            "format_": {
                "type": "text",
            },
            "verbosity": "medium",
        }, reasoning={
            "summary": "auto",
            "enabled": True,
        }, temperature=0.7, top_p=0.9, prompt={
            "id": "<id>",
            "variables": {
                "key": {
                    "type": "input_text",
                    "text": "Hello, how can I help you?",
                },
            },
        }, service_tier="auto", truncation="auto", stream=False, provider={
            "data_collection": "deny",
            "zdr": True,
            "enforce_distillable_text": True,
            "order": [
                "OpenAI",
            ],
            "only": [
                "OpenAI",
            ],
            "ignore": [
                "OpenAI",
            ],
            "quantizations": None,
            "sort": "price",
        })

        with res as event_stream:
            for event in event_stream:
                # handle event
                print(event, flush=True)


    except errors.OpenRouterError as e:
        # The base class for HTTP error responses
        print(e.message)
        print(e.status_code)
        print(e.body)
        print(e.headers)
        print(e.raw_response)

        # Depending on the method different errors may be thrown
        if isinstance(e, errors.BadRequestResponseError):
            print(e.data.error)  # models.BadRequestResponseErrorData
            print(e.data.user_id)  # OptionalNullable[str]
```

### Error Classes
**Primary errors:**
* [`OpenRouterError`](./src/openrouter/errors/openroutererror.py): The base class for HTTP error responses.
  * [`InternalServerResponseError`](./src/openrouter/errors/internalserverresponseerror.py): Internal Server Error - Unexpected server error. Status code `500`. *

<details><summary>Less common errors (19)</summary>

<br />

**Network errors:**
* [`httpx.RequestError`](https://www.python-httpx.org/exceptions/#httpx.RequestError): Base class for request errors.
    * [`httpx.ConnectError`](https://www.python-httpx.org/exceptions/#httpx.ConnectError): HTTP client was unable to make a request to a server.
    * [`httpx.TimeoutException`](https://www.python-httpx.org/exceptions/#httpx.TimeoutException): HTTP request timed out.


**Inherit from [`OpenRouterError`](./src/openrouter/errors/openroutererror.py)**:
* [`UnauthorizedResponseError`](./src/openrouter/errors/unauthorizedresponseerror.py): Unauthorized - Authentication required or invalid credentials. Status code `401`. Applicable to 15 of 24 methods.*
* [`BadRequestResponseError`](./src/openrouter/errors/badrequestresponseerror.py): Bad Request - Invalid request parameters or malformed input. Status code `400`. Applicable to 10 of 24 methods.*
* [`TooManyRequestsResponseError`](./src/openrouter/errors/toomanyrequestsresponseerror.py): Too Many Requests - Rate limit exceeded. Status code `429`. Applicable to 9 of 24 methods.*
* [`NotFoundResponseError`](./src/openrouter/errors/notfoundresponseerror.py): Not Found - Resource does not exist. Status code `404`. Applicable to 8 of 24 methods.*
* [`PaymentRequiredResponseError`](./src/openrouter/errors/paymentrequiredresponseerror.py): Payment Required - Insufficient credits or quota to complete request. Status code `402`. Applicable to 3 of 24 methods.*
* [`ForbiddenResponseError`](./src/openrouter/errors/forbiddenresponseerror.py): Forbidden - Authentication successful but insufficient permissions. Status code `403`. Applicable to 3 of 24 methods.*
* [`BadGatewayResponseError`](./src/openrouter/errors/badgatewayresponseerror.py): Bad Gateway - Provider/upstream API failure. Status code `502`. Applicable to 3 of 24 methods.*
* [`EdgeNetworkTimeoutResponseError`](./src/openrouter/errors/edgenetworktimeoutresponseerror.py): Infrastructure Timeout - Provider request timed out at edge network. Status code `524`. Applicable to 3 of 24 methods.*
* [`ProviderOverloadedResponseError`](./src/openrouter/errors/provideroverloadedresponseerror.py): Provider Overloaded - Provider is temporarily overloaded. Status code `529`. Applicable to 3 of 24 methods.*
* [`ChatError`](./src/openrouter/errors/chaterror.py): Bad request - invalid parameters. Applicable to 2 of 24 methods.*
* [`ServiceUnavailableResponseError`](./src/openrouter/errors/serviceunavailableresponseerror.py): Service Unavailable - Service temporarily unavailable. Status code `503`. Applicable to 2 of 24 methods.*
* [`RequestTimeoutResponseError`](./src/openrouter/errors/requesttimeoutresponseerror.py): Request Timeout - Operation exceeded time limit. Status code `408`. Applicable to 1 of 24 methods.*
* [`PayloadTooLargeResponseError`](./src/openrouter/errors/payloadtoolargeresponseerror.py): Payload Too Large - Request payload exceeds size limits. Status code `413`. Applicable to 1 of 24 methods.*
* [`UnprocessableEntityResponseError`](./src/openrouter/errors/unprocessableentityresponseerror.py): Unprocessable Entity - Semantic validation failure. Status code `422`. Applicable to 1 of 24 methods.*
* [`ResponseValidationError`](./src/openrouter/errors/responsevalidationerror.py): Type mismatch between the response data and the expected Pydantic model. Provides access to the Pydantic validation error via the `cause` attribute.

</details>

\* Check [the method documentation](#available-resources-and-operations) to see if the error is applicable.
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Select Server by Name

You can override the default server globally by passing a server name to the `server: str` optional parameter when initializing the SDK client instance. The selected server will then be used as the default on the operations that use it. This table lists the names associated with the available servers:

| Name         | Server                         | Description       |
| ------------ | ------------------------------ | ----------------- |
| `production` | `https://openrouter.ai/api/v1` | Production server |

#### Example

```python
from openrouter import OpenRouter
import os


with OpenRouter(
    server="production",
    api_key=os.getenv("OPENROUTER_API_KEY", ""),
) as open_router:

    res = open_router.beta.responses.send(input=[
        {
            "type": "message",
            "role": "user",
            "content": "Hello, how are you?",
        },
    ], metadata={
        "user_id": "123",
        "session_id": "abc-def-ghi",
    }, tools=[
        {
            "type": "function",
            "name": "get_current_weather",
            "description": "Get the current weather in a given location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                    },
                },
            },
        },
    ], model="anthropic/claude-4.5-sonnet-20250929", text={
        "format_": {
            "type": "text",
        },
        "verbosity": "medium",
    }, reasoning={
        "summary": "auto",
        "enabled": True,
    }, temperature=0.7, top_p=0.9, prompt={
        "id": "<id>",
        "variables": {
            "key": {
                "type": "input_text",
                "text": "Hello, how can I help you?",
            },
        },
    }, service_tier="auto", truncation="auto", stream=False, provider={
        "data_collection": "deny",
        "zdr": True,
        "enforce_distillable_text": True,
        "order": [
            "OpenAI",
        ],
        "only": [
            "OpenAI",
        ],
        "ignore": [
            "OpenAI",
        ],
        "quantizations": None,
        "sort": "price",
    })

    with res as event_stream:
        for event in event_stream:
            # handle event
            print(event, flush=True)

```

### Override Server URL Per-Client

The default server can also be overridden globally by passing a URL to the `server_url: str` optional parameter when initializing the SDK client instance. For example:
```python
from openrouter import OpenRouter
import os


with OpenRouter(
    server_url="https://openrouter.ai/api/v1",
    api_key=os.getenv("OPENROUTER_API_KEY", ""),
) as open_router:

    res = open_router.beta.responses.send(input=[
        {
            "type": "message",
            "role": "user",
            "content": "Hello, how are you?",
        },
    ], metadata={
        "user_id": "123",
        "session_id": "abc-def-ghi",
    }, tools=[
        {
            "type": "function",
            "name": "get_current_weather",
            "description": "Get the current weather in a given location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                    },
                },
            },
        },
    ], model="anthropic/claude-4.5-sonnet-20250929", text={
        "format_": {
            "type": "text",
        },
        "verbosity": "medium",
    }, reasoning={
        "summary": "auto",
        "enabled": True,
    }, temperature=0.7, top_p=0.9, prompt={
        "id": "<id>",
        "variables": {
            "key": {
                "type": "input_text",
                "text": "Hello, how can I help you?",
            },
        },
    }, service_tier="auto", truncation="auto", stream=False, provider={
        "data_collection": "deny",
        "zdr": True,
        "enforce_distillable_text": True,
        "order": [
            "OpenAI",
        ],
        "only": [
            "OpenAI",
        ],
        "ignore": [
            "OpenAI",
        ],
        "quantizations": None,
        "sort": "price",
    })

    with res as event_stream:
        for event in event_stream:
            # handle event
            print(event, flush=True)

```
<!-- End Server Selection [server] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The Python SDK makes API calls using the [httpx](https://www.python-httpx.org/) HTTP library.  In order to provide a convenient way to configure timeouts, cookies, proxies, custom headers, and other low-level configuration, you can initialize the SDK client with your own HTTP client instance.
Depending on whether you are using the sync or async version of the SDK, you can pass an instance of `HttpClient` or `AsyncHttpClient` respectively, which are Protocol's ensuring that the client has the necessary methods to make API calls.
This allows you to wrap the client with your own custom logic, such as adding custom headers, logging, or error handling, or you can just pass an instance of `httpx.Client` or `httpx.AsyncClient` directly.

For example, you could specify a header for every request that this sdk makes as follows:
```python
from openrouter import OpenRouter
import httpx

http_client = httpx.Client(headers={"x-custom-header": "someValue"})
s = OpenRouter(client=http_client)
```

or you could wrap the client with your own custom logic:
```python
from openrouter import OpenRouter
from openrouter.httpclient import AsyncHttpClient
import httpx

class CustomClient(AsyncHttpClient):
    client: AsyncHttpClient

    def __init__(self, client: AsyncHttpClient):
        self.client = client

    async def send(
        self,
        request: httpx.Request,
        *,
        stream: bool = False,
        auth: Union[
            httpx._types.AuthTypes, httpx._client.UseClientDefault, None
        ] = httpx.USE_CLIENT_DEFAULT,
        follow_redirects: Union[
            bool, httpx._client.UseClientDefault
        ] = httpx.USE_CLIENT_DEFAULT,
    ) -> httpx.Response:
        request.headers["Client-Level-Header"] = "added by client"

        return await self.client.send(
            request, stream=stream, auth=auth, follow_redirects=follow_redirects
        )

    def build_request(
        self,
        method: str,
        url: httpx._types.URLTypes,
        *,
        content: Optional[httpx._types.RequestContent] = None,
        data: Optional[httpx._types.RequestData] = None,
        files: Optional[httpx._types.RequestFiles] = None,
        json: Optional[Any] = None,
        params: Optional[httpx._types.QueryParamTypes] = None,
        headers: Optional[httpx._types.HeaderTypes] = None,
        cookies: Optional[httpx._types.CookieTypes] = None,
        timeout: Union[
            httpx._types.TimeoutTypes, httpx._client.UseClientDefault
        ] = httpx.USE_CLIENT_DEFAULT,
        extensions: Optional[httpx._types.RequestExtensions] = None,
    ) -> httpx.Request:
        return self.client.build_request(
            method,
            url,
            content=content,
            data=data,
            files=files,
            json=json,
            params=params,
            headers=headers,
            cookies=cookies,
            timeout=timeout,
            extensions=extensions,
        )

s = OpenRouter(async_client=CustomClient(httpx.AsyncClient()))
```
<!-- End Custom HTTP Client [http-client] -->

<!-- Start Resource Management [resource-management] -->
## Resource Management

The `OpenRouter` class implements the context manager protocol and registers a finalizer function to close the underlying sync and async HTTPX clients it uses under the hood. This will close HTTP connections, release memory and free up other resources held by the SDK. In short-lived Python programs and notebooks that make a few SDK method calls, resource management may not be a concern. However, in longer-lived programs, it is beneficial to create a single SDK instance via a [context manager][context-manager] and reuse it across the application.

[context-manager]: https://docs.python.org/3/reference/datamodel.html#context-managers

```python
from openrouter import OpenRouter
import os
def main():

    with OpenRouter(
        api_key=os.getenv("OPENROUTER_API_KEY", ""),
    ) as open_router:
        # Rest of application here...


# Or when using async:
async def amain():

    async with OpenRouter(
        api_key=os.getenv("OPENROUTER_API_KEY", ""),
    ) as open_router:
        # Rest of application here...
```
<!-- End Resource Management [resource-management] -->

<!-- Start Debugging [debug] -->
## Debugging

You can setup your SDK to emit debug logs for SDK requests and responses.

You can pass your own logger class directly into your SDK.
```python
from openrouter import OpenRouter
import logging

logging.basicConfig(level=logging.DEBUG)
s = OpenRouter(debug_logger=logging.getLogger("openrouter"))
```

You can also enable a default debug logger by setting an environment variable `OPENROUTER_DEBUG` to true.
<!-- End Debugging [debug] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=openrouter&utm_campaign=python)

<style>
  :root {
    --badge-gray-bg: #f3f4f6;
    --badge-gray-border: #d1d5db;
    --badge-gray-text: #374151;
    --badge-blue-bg: #eff6ff;
    --badge-blue-border: #3b82f6;
    --badge-blue-text: #3b82f6;
  }

  @media (prefers-color-scheme: dark) {
    :root {
      --badge-gray-bg: #374151;
      --badge-gray-border: #4b5563;
      --badge-gray-text: #f3f4f6;
      --badge-blue-bg: #1e3a8a;
      --badge-blue-border: #3b82f6;
      --badge-blue-text: #93c5fd;
    }
  }
  
  h1 {
    border-bottom: none !important;
    margin-bottom: 4px;
    margin-top: 0;
    letter-spacing: 0.5px;
    font-weight: 600;
  }
  
  .badge-text {
    letter-spacing: 1px;
    font-weight: 300;
  }
  
  .badge-container {
    display: inline-flex;
    align-items: center;
    background: var(--badge-gray-bg);
    border: 1px solid var(--badge-gray-border);
    border-radius: 6px;
    overflow: hidden;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
    font-size: 11px;
    text-decoration: none;
    vertical-align: middle;
  }

  .badge-container.blue {
    background: var(--badge-blue-bg);
    border-color: var(--badge-blue-border);
  }

  .badge-icon-section {
    padding: 4px 8px;
    border-right: 1px solid var(--badge-gray-border);
    display: flex;
    align-items: center;
  }

  .badge-text-section {
    padding: 4px 10px;
    color: var(--badge-gray-text);
    font-weight: 400;
  }

  .badge-container.blue .badge-text-section {
    color: var(--badge-blue-text);
  }
  
  .badge-link {
    text-decoration: none;
    margin-left: 8px;
    display: inline-flex;
    vertical-align: middle;
  }

  .badge-link:hover {
    text-decoration: none;
  }
  
  .badge-link:first-child {
    margin-left: 0;
  }
  
  .badge-icon-section svg {
    color: var(--badge-gray-text);
  }

  .badge-container.blue .badge-icon-section svg {
    color: var(--badge-blue-text);
  }
</style> 