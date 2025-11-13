# OpenResponsesUsage

Token usage information for the response


## Fields

| Field                                                               | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `input_tokens`                                                      | *float*                                                             | :heavy_check_mark:                                                  | N/A                                                                 |
| `input_tokens_details`                                              | [models.InputTokensDetails](../models/inputtokensdetails.md)        | :heavy_check_mark:                                                  | N/A                                                                 |
| `output_tokens`                                                     | *float*                                                             | :heavy_check_mark:                                                  | N/A                                                                 |
| `output_tokens_details`                                             | [models.OutputTokensDetails](../models/outputtokensdetails.md)      | :heavy_check_mark:                                                  | N/A                                                                 |
| `total_tokens`                                                      | *float*                                                             | :heavy_check_mark:                                                  | N/A                                                                 |
| `cost`                                                              | *OptionalNullable[float]*                                           | :heavy_minus_sign:                                                  | Cost of the completion                                              |
| `is_byok`                                                           | *Optional[bool]*                                                    | :heavy_minus_sign:                                                  | Whether a request was made using a Bring Your Own Key configuration |
| `cost_details`                                                      | [Optional[models.CostDetails]](../models/costdetails.md)            | :heavy_minus_sign:                                                  | N/A                                                                 |