# CompletionResponse


## Fields

| Field                                                            | Type                                                             | Required                                                         | Description                                                      |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| `id`                                                             | *str*                                                            | :heavy_check_mark:                                               | N/A                                                              |
| `object`                                                         | *Literal["text_completion"]*                                     | :heavy_check_mark:                                               | N/A                                                              |
| `created`                                                        | *float*                                                          | :heavy_check_mark:                                               | N/A                                                              |
| `model`                                                          | *str*                                                            | :heavy_check_mark:                                               | N/A                                                              |
| `system_fingerprint`                                             | *Optional[str]*                                                  | :heavy_minus_sign:                                               | N/A                                                              |
| `choices`                                                        | List[[models.CompletionChoice](../models/completionchoice.md)]   | :heavy_check_mark:                                               | N/A                                                              |
| `usage`                                                          | [Optional[models.CompletionUsage]](../models/completionusage.md) | :heavy_minus_sign:                                               | N/A                                                              |