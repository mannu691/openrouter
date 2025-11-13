# Parameters
(*parameters*)

## Overview

Parameters endpoints

### Available Operations

* [get_parameters](#get_parameters) - Get a model's supported parameters and data about which are most popular

## get_parameters

Get a model's supported parameters and data about which are most popular

### Example Usage

<!-- UsageSnippet language="python" operationID="getParameters" method="get" path="/parameters/{author}/{slug}" -->
```python
from openrouter import OpenRouter, models
import os


with OpenRouter() as open_router:

    res = open_router.parameters.get_parameters(security=models.GetParametersSecurity(
        bearer=os.getenv("OPENROUTER_BEARER", ""),
    ), author="<value>", slug="<value>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                       | Type                                                                            | Required                                                                        | Description                                                                     |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `security`                                                                      | [models.GetParametersSecurity](../../models/getparameterssecurity.md)           | :heavy_check_mark:                                                              | N/A                                                                             |
| `author`                                                                        | *str*                                                                           | :heavy_check_mark:                                                              | N/A                                                                             |
| `slug`                                                                          | *str*                                                                           | :heavy_check_mark:                                                              | N/A                                                                             |
| `provider`                                                                      | [Optional[models.GetParametersProvider]](../../models/getparametersprovider.md) | :heavy_minus_sign:                                                              | N/A                                                                             |
| `retries`                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                | :heavy_minus_sign:                                                              | Configuration to override the default retry behavior of the client.             |

### Response

**[models.GetParametersResponse](../../models/getparametersresponse.md)**

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| errors.UnauthorizedResponseError   | 401                                | application/json                   |
| errors.NotFoundResponseError       | 404                                | application/json                   |
| errors.InternalServerResponseError | 500                                | application/json                   |
| errors.OpenRouterDefaultError      | 4XX, 5XX                           | \*/\*                              |