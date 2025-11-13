# Architecture

Model architecture information


## Fields

| Field                                                      | Type                                                       | Required                                                   | Description                                                | Example                                                    |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `tokenizer`                                                | [Nullable[models.Tokenizer]](../models/tokenizer.md)       | :heavy_check_mark:                                         | N/A                                                        | GPT                                                        |
| `instruct_type`                                            | [Nullable[models.InstructType]](../models/instructtype.md) | :heavy_check_mark:                                         | Instruction format type                                    |                                                            |
| `modality`                                                 | *Nullable[str]*                                            | :heavy_check_mark:                                         | Primary modality of the model                              | text                                                       |
| `input_modalities`                                         | List[[models.InputModality](../models/inputmodality.md)]   | :heavy_check_mark:                                         | Supported input modalities                                 |                                                            |
| `output_modalities`                                        | List[[models.OutputModality](../models/outputmodality.md)] | :heavy_check_mark:                                         | Supported output modalities                                |                                                            |