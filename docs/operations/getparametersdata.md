# GetParametersData

Parameter analytics data


## Fields

| Field                                                                      | Type                                                                       | Required                                                                   | Description                                                                | Example                                                                    |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `model`                                                                    | *str*                                                                      | :heavy_check_mark:                                                         | Model identifier                                                           | openai/gpt-4                                                               |
| `supported_parameters`                                                     | List[[operations.SupportedParameter](../operations/supportedparameter.md)] | :heavy_check_mark:                                                         | List of parameters supported by this model                                 | [<br/>"temperature",<br/>"top_p",<br/>"max_tokens"<br/>]                   |