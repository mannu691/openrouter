# CreateEmbeddingsResponseBody

Embedding response


## Fields

| Field                                                                  | Type                                                                   | Required                                                               | Description                                                            |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `id`                                                                   | *Optional[str]*                                                        | :heavy_minus_sign:                                                     | N/A                                                                    |
| `object`                                                               | [models.CreateEmbeddingsObject](../models/createembeddingsobject.md)   | :heavy_check_mark:                                                     | N/A                                                                    |
| `data`                                                                 | List[[models.CreateEmbeddingsData](../models/createembeddingsdata.md)] | :heavy_check_mark:                                                     | N/A                                                                    |
| `model`                                                                | *str*                                                                  | :heavy_check_mark:                                                     | N/A                                                                    |
| `usage`                                                                | [Optional[models.Usage]](../models/usage.md)                           | :heavy_minus_sign:                                                     | N/A                                                                    |