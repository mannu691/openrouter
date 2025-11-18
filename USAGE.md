<!-- Start SDK Example Usage [usage] -->
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
        "data_collection": "allow",
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
            "data_collection": "allow",
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