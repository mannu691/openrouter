# GetParametersResponse

Returns the parameters for the specified model


## Fields

| Field                                                                                         | Type                                                                                          | Required                                                                                      | Description                                                                                   | Example                                                                                       |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `data`                                                                                        | [operations.GetParametersData](../operations/getparametersdata.md)                            | :heavy_check_mark:                                                                            | Parameter analytics data                                                                      | {<br/>"model": "openai/gpt-4",<br/>"supported_parameters": [<br/>"temperature",<br/>"top_p",<br/>"max_tokens"<br/>]<br/>} |