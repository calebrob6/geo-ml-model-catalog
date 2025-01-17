# Model Metadata Specification

This document describes the structure and content of a top-level Model Metadata object.

## Model Metadata Fields

| Field Name           | Type               | Description                                                                         |
|----------------------|--------------------|-------------------------------------------------------------------------------------|
| `model_id`           | string             | **REQUIRED.** A unique string identifier for the model. This ID must be unique across the provider. |
| `algorithm_type`     | [Algorithm Type]\|string | **REQUIRED.** A string identifying the high-level algorithm type that the model employs. STRONGLY RECOMMENDED to use on the standard [Algorithm Type] values, but other values are allowed. |
| `model_type`         | [Model Type]\|string | **REQUIRED.** Identifier for the type of model. STRONGLY RECOMMENDED to use on of the standard [Model Type] values, but other values are allowed. |
| `model_architecture` | string             | Identifies the model architecture used (e.g. RCNN, U-Net, etc.).                    |
| `license`            | string             | **REQUIRED.** The model's license(s). Either a SPDX [License identifier], `various` if multiple licenses apply, or `proprietary` for all other cases. |
| `authors`            | \[[Author]\]       | **REQUIRED.** List of names and contact information for the model author(s).                 |
| `citation`           | [Citation]         | Citation information related to the model.                                          |
| `training`           | [Model Training]   | **REQUIRED.** A description of the data and environment used to train the model.    |
| `inputs`             | \[[Model Input]\]  | **REQUIRED.** A list of [Model Input] objects describing the names and types of model inputs.  |
| `outputs`            | \[[Model Output]\] | **REQUIRED.** A list of [Model Output] objects describing the names and types of model outputs. |
| `runtimes`           | \[[Runtime]\]      | A list of [Runtime] objects describing serialized or containerized versions of the model that can be used to generate inferences. |
| `usage_recommendations` | [Usage Recommendations] | A description of the recommended conditions under which the model can be used. |

### Algorithm Type

This string describes the general type of machine learning algorithm employed by the model. It is STRONGLY RECOMMENDED 
that you use one of the following values, but other values are allowed.

* `"Supervised"`
* `"Unsupervised"`
* `"Semi-Supervised"`
* `"Reinforcement Learning"`

### Model Type

This string provides a more specific description of the type of model. It is STRONGLY RECOMMENDED that you use one of the 
following values, but other values are allowed. Note that not all Model Type values are valid for a given [Algorithm Type].

* `"Object Detection"`
* `"Classification"`
* `"Segmentation"`
* `"Regression"`

### Author

This object describes an author involved in creating the model.

| Field Name      | Type      | Description                                                            |
|-----------------|-----------|------------------------------------------------------------------------|
| `name`          | string    | **REQUIRED.** The full name of the author.                             |
| `organization`  | string    | The name of the organization to which this author is affiliated.       |
| `email`         | string    | **REQUIRED.** A contact email for this author. STRONGLY RECOMMENDED for all authors. | 

### Citation

This object indicates from which publication the model originates and how the model itself should be cited or 
referenced. The object follows the [STAC Scientific Citation Extension], with 2 notable changes: (
    * There is no `sci:` prefix on the field names
    * If `doi` is present, then `citation` is also required

All field descriptions are adapted from the corresponding [STAC Scientific Citation Extension]
definitions. *As per the Scientific Citation Extension spec, at least one field is required.*

| Field Name     | Type                     | Description                                                               |
|----------------|--------------------------|---------------------------------------------------------------------------|
| `doi`          | string                   | The DOI of the data, e.g. `10.1000/xyz123`. This MUST NOT be a DOIs link. |
| `citation`     | string                   | The recommended human-readable reference (citation) to be used by publications citing the model. No specific citation style is suggested, but the citation should contain all information required to find the publication distinctively. **Required if `doi` is present.** |
| `publications` | \[[Publication Object]\] | List of relevant publications referencing and describing the data.        |

#### Publication Object

| Field Name  | Type    | Description                                                                  |
|-------------|---------|------------------------------------------------------------------------------|
| `doi`       | string  | See the description of `doi` field in the [Citation] description above.      |
| `citation`  | string  | See the description of `citation` field in the [Citation] description above. |

### Model Input

This object describes a single model input parameter.

| Field Name    | Type    | Description                                                                  |
|---------------|---------|------------------------------------------------------------------------------|
| `name`        | string  | **REQUIRED.** The name of the parameter.                                     |
| `type`        | string  | **REQUIRED.** The data type of the parameter (e.g. `float32`).               |
| `shape`       | [int]   | **REQUIRED.** The shape of the parameter as an array of integers.      |
| `description` | string  | A human-readable description of the parameter that indicates what type of content is required. |

### Model Output

This object describes a single model output.

| Field Name    | Type    | Description                                                                  |
|---------------|---------|------------------------------------------------------------------------------|
| `name`        | string  | **REQUIRED.** The name of the parameter.                                     |
| `type`        | string  | **REQUIRED.** The data type of the parameter (e.g. `float32`).               |
| `shape`       | [int]   | **REQUIRED.** The shape of the parameter as an array of integers.      |
| `description` | string  | A human-readable description of the parameter that indicates what type of content it contains. |

### Usage Recommendations

**COMING SOON**

[License identifier]: https://spdx.org/licenses/
[STAC Scientific Citation Extension]: https://github.com/radiantearth/stac-spec/tree/v1.0.0-rc.1/extensions/scientific
[Runtime]: ../fragments/runtime
[Model Training]: ../fragments/training
[Algorithm Type]: #algorithm-type
[Model Type]: #model-type
[Author]: #author
[Citation]: #citation
[Model Input]: #model-input
[Model Output]: #model-output
[Usage Recommendations]: #usage-recommendations
[Publication Object]: #publication-object
