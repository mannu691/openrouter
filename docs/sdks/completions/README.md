# Completions
(*completions*)

## Overview

### Available Operations

* [generate](#generate) - Create a completion

## generate

Creates a completion for the provided prompt and parameters. Supports both streaming and non-streaming modes.

### Example Usage

<!-- UsageSnippet language="python" operationID="createCompletions" method="post" path="/completions" -->
```python
from openrouter import OpenRouter
import os


with OpenRouter(
    api_key=os.getenv("OPENROUTER_API_KEY", ""),
) as open_router:

    res = open_router.completions.generate(prompt=[], stream=False)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                       | Type                                                                                                                            | Required                                                                                                                        | Description                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `prompt`                                                                                                                        | [models.Prompt](../../models/prompt.md)                                                                                         | :heavy_check_mark:                                                                                                              | N/A                                                                                                                             |
| `model`                                                                                                                         | *Optional[str]*                                                                                                                 | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `models`                                                                                                                        | List[*str*]                                                                                                                     | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `best_of`                                                                                                                       | *OptionalNullable[int]*                                                                                                         | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `echo`                                                                                                                          | *OptionalNullable[bool]*                                                                                                        | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `frequency_penalty`                                                                                                             | *OptionalNullable[float]*                                                                                                       | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `logit_bias`                                                                                                                    | Dict[str, *float*]                                                                                                              | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `logprobs`                                                                                                                      | *OptionalNullable[int]*                                                                                                         | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `max_tokens`                                                                                                                    | *OptionalNullable[int]*                                                                                                         | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `n`                                                                                                                             | *OptionalNullable[int]*                                                                                                         | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `presence_penalty`                                                                                                              | *OptionalNullable[float]*                                                                                                       | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `seed`                                                                                                                          | *OptionalNullable[int]*                                                                                                         | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `stop`                                                                                                                          | [OptionalNullable[models.CompletionCreateParamsStop]](../../models/completioncreateparamsstop.md)                               | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `stream`                                                                                                                        | *Optional[bool]*                                                                                                                | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `stream_options`                                                                                                                | [OptionalNullable[models.StreamOptions]](../../models/streamoptions.md)                                                         | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `suffix`                                                                                                                        | *OptionalNullable[str]*                                                                                                         | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `temperature`                                                                                                                   | *OptionalNullable[float]*                                                                                                       | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `top_p`                                                                                                                         | *OptionalNullable[float]*                                                                                                       | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `user`                                                                                                                          | *Optional[str]*                                                                                                                 | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `metadata`                                                                                                                      | Dict[str, *str*]                                                                                                                | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `response_format`                                                                                                               | [OptionalNullable[models.CompletionCreateParamsResponseFormatUnion]](../../models/completioncreateparamsresponseformatunion.md) | :heavy_minus_sign:                                                                                                              | N/A                                                                                                                             |
| `retries`                                                                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                | :heavy_minus_sign:                                                                                                              | Configuration to override the default retry behavior of the client.                                                             |

### Response

**[models.CompletionResponse](../../models/completionresponse.md)**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| errors.ChatError              | 400, 401, 429                 | application/json              |
| errors.ChatError              | 500                           | application/json              |
| errors.OpenRouterDefaultError | 4XX, 5XX                      | \*/\*                         |