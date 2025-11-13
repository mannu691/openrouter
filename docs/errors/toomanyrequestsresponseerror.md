# TooManyRequestsResponseError

Too Many Requests - Rate limit exceeded


## Fields

| Field                                                                                    | Type                                                                                     | Required                                                                                 | Description                                                                              | Example                                                                                  |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `error`                                                                                  | [models.TooManyRequestsResponseErrorData](../models/toomanyrequestsresponseerrordata.md) | :heavy_check_mark:                                                                       | Error data for TooManyRequestsResponse                                                   | {<br/>"code": 429,<br/>"message": "Rate limit exceeded"<br/>}                            |
| `user_id`                                                                                | *OptionalNullable[str]*                                                                  | :heavy_minus_sign:                                                                       | N/A                                                                                      |                                                                                          |