# packages/markitdown/src/markitdown/converters/_image_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_image_converter.py",
  "file_hash": "481fa76914c9c5216aa68f7095a27d11bd5961c129525bc8c307521f6476c20c",
  "last_updated": "2026-01-04T17:20:45.327906+00:00",
  "functions": {
    "ImageConverter": {
      "hash": "a86647684e51ba42a8661c20995abeb53b44b874439f44cced1985f2f0660088",
      "lines": "16-139",
      "last_updated": "2026-01-04T17:20:45.327830+00:00"
    }
  }
}
```

</details>



The file `packages/markitdown/src/markitdown/converters/_image_converter.py` implements an `ImageConverter` class that is responsible for converting image files into markdown format. This conversion process includes extracting metadata from the images, provided that the `exiftool` is installed, and generating a description of the image using a multimodal language model (LLM) if a client for the LLM is configured. The class checks for accepted image MIME types and file extensions before processing the images.

The `ImageConverter` class contains several methods: 
- `accepts`: This method determines if a given file stream is acceptable based on its MIME type or file extension, returning a boolean value.
- `convert`: This method performs the main conversion operation, extracting metadata from the image and optionally generating a description using the LLM. It returns a `DocumentConverterResult` containing the generated markdown content.
- `_get_llm_description`: This private method prepares and sends a request to the LLM API to obtain a description of the image. It encodes the image as a base64 data URI and formats the request appropriately.

The code explicitly imports several modules, including `BinaryIO`, `Any`, and `Union` from the `typing` module, `base64`, and `mimetypes`. It also imports `exiftool_metadata` from the `_exiftool` module, `DocumentConverter` and `DocumentConverterResult` from the `_base_converter` module, and `StreamInfo` from the `_stream_info` module. The file manipulates data structures such as `StreamInfo` for metadata about the file stream and constructs a markdown string to represent the image's metadata and description. The LLM API is accessed through a client object, which is expected to have a `chat.completions.create` method for generating responses.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `ImageConverter`

**Nested Functions:**
- `accepts`
- `convert`
- `_get_llm_description`

<details>
<summary><strong>Calls/Dependencies</strong> (19 unique functions)</summary>

- `DocumentConverterResult`
- `ImageConverter`
- `LLM`
- `_get_llm_description`
- `accepts`
- `b64encode`
- `convert`
- `create`
- `decode`
- `exiftool_metadata`
- `get`
- `guess_type`
- `lower`
- `metadata`
- `read`
- `seek`
- `startswith`
- `strip`
- `tell`

</details>

</details>



## Functions and Classes

## `ImageConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_image_converter.py:16`](/packages/markitdown/src/markitdown/converters/_image_converter.py#L16-L139)

**Nested Functions:** `accepts`, `convert`, `_get_llm_description`  
**Dependencies:** `DocumentConverterResult`, `ImageConverter`, `LLM`, `_get_llm_description`, `accepts`, `b64encode`, `convert`, `create`, `decode`, `exiftool_metadata`, `get`, `guess_type`, `lower`, `metadata`, `read` *(+4 more)*  


# ImageConverter Documentation

## Class: ImageConverter

The `ImageConverter` class extends the `DocumentConverter` class and is responsible for converting image files to markdown format. It extracts metadata from images using `exiftool` (if available) and generates a description using a multimodal language model (LLM) if an `llm_client` is configured.

### Method: accepts

#### Description
The `accepts` method determines if the provided file stream and stream information are acceptable for conversion based on file extensions and MIME types.

#### Parameters
- `file_stream` (BinaryIO): The input stream of the image file.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension of the image.
- `**kwargs` (Any): Additional keyword arguments.

#### Returns
- `bool`: Returns `True` if the file extension or MIME type is acceptable, otherwise returns `False`.

### Method: convert

#### Description
The `convert` method processes the image file stream, extracts metadata, and generates a markdown representation of the image, including a description if an LLM client is provided.

#### Parameters
- `file_stream` (BinaryIO): The input stream of the image file.
- `stream_info` (StreamInfo): An object containing metadata about the stream.
- `**kwargs` (Any): Additional keyword arguments, which may include:
  - `exiftool_path` (str): The path to the `exiftool` executable.
  - `llm_client`: An instance of the LLM client used to generate descriptions.
  - `llm_model` (str): The model identifier for the LLM.
  - `llm_prompt` (str): A custom prompt for the LLM description.

#### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): The generated markdown content, including extracted metadata and LLM-generated description.

### Method: _get_llm_description

#### Description
The `_get_llm_description` method generates a description for the image using the LLM client by sending the image data as a base64-encoded string.

#### Parameters
- `file_stream` (BinaryIO): The input stream of the image file.
- `stream_info` (StreamInfo): An object containing metadata about the stream.
- `client`: The LLM client instance used to make API calls.
- `model`: The model identifier for the LLM.
- `prompt` (str, optional): A custom prompt for the LLM description. Defaults to "Write a detailed caption for this image." if not provided.

#### Returns
- `Union[None, str]`: Returns the generated description as a string if successful; otherwise, returns `None`.

### Dependencies
- `exiftool`: Required for extracting metadata from images.
- `base64`: Used for encoding the image data.
- `mimetypes`: Used for determining the content type of the image.
- An LLM client (e.g., OpenAI API) is required for generating descriptions.

### Usage Example
```python
from io import BytesIO

# Assuming `stream_info` is an instance of StreamInfo with appropriate attributes
file_stream = BytesIO(open("path/to/image.jpg", "rb").read())
converter = ImageConverter()

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info, exiftool_path="/path/to/exiftool", llm_client=my_llm_client, llm_model="gpt-3.5-turbo")
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
