# packages/markitdown/src/markitdown/converters/_image_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_image_converter.py",
  "file_hash": "481fa76914c9c5216aa68f7095a27d11bd5961c129525bc8c307521f6476c20c",
  "last_updated": "2025-12-23T15:50:35.557083+00:00",
  "functions": {
    "ImageConverter": {
      "hash": "a86647684e51ba42a8661c20995abeb53b44b874439f44cced1985f2f0660088",
      "lines": "16-139",
      "last_updated": "2025-12-23T15:50:35.557004+00:00"
    }
  }
}
```

</details>



The file `_image_converter.py` implements the `ImageConverter` class, which is responsible for converting image files into markdown format. This conversion process involves extracting metadata from the images using the `exiftool_metadata` function and generating a description of the image through a multimodal language model (LLM) if an LLM client is provided. The class defines methods to determine if a file can be accepted for conversion based on its MIME type or file extension and to perform the actual conversion.

The main functions and methods in the `ImageConverter` class include:
- `accepts`: This method checks if the provided file stream and stream information correspond to accepted image MIME types or file extensions.
- `convert`: This method performs the conversion of the image file to markdown format, including extracting metadata and generating an LLM-based description.
- `_get_llm_description`: This private method interacts with the LLM client to generate a description of the image based on the provided prompt and the image data encoded in base64.

The code explicitly imports several modules, including `BinaryIO`, `Any`, and `Union` from the `typing` module, as well as `base64`, `mimetypes`, and functions from other modules within the same package. It relies on an external service, specifically the OpenAI API, to generate image descriptions. The file manipulates data structures such as `DocumentConverterResult`, which encapsulates the resulting markdown content, and `StreamInfo`, which contains metadata about the file being processed. The code also defines constants for accepted MIME type prefixes and file extensions used in the conversion process.

## Functions and Classes

## `ImageConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_image_converter.py:16`](/packages/markitdown/src/markitdown/converters/_image_converter.py#L16-L139)

# ImageConverter Documentation

## Overview
The `ImageConverter` class extends the `DocumentConverter` class and is designed to convert image files into Markdown format. It extracts metadata from images using `exiftool` and generates a description using a configured multimodal language model (LLM) client.

## Method: `accepts`

### Description
The `accepts` method determines whether the provided file stream is acceptable for conversion based on its MIME type and file extension.

### Parameters
- `file_stream` (BinaryIO): The input stream of the file to be checked.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
- `**kwargs` (Any): Additional keyword arguments (not used in this method).

### Returns
- `bool`: Returns `True` if the file extension or MIME type matches accepted formats; otherwise, returns `False`.

## Method: `convert`

### Description
The `convert` method processes the input file stream, extracts metadata, and generates a Markdown representation of the image.

### Parameters
- `file_stream` (BinaryIO): The input stream of the image file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the stream.
- `**kwargs` (Any): Additional keyword arguments that can include:
  - `exiftool_path` (str): Path to the `exiftool` executable.
  - `llm_client`: An instance of the LLM client for generating descriptions.
  - `llm_model` (str): The model to be used by the LLM client.
  - `llm_prompt` (str): A custom prompt for the LLM (optional).

### Returns
- `DocumentConverterResult`: An object containing the generated Markdown content in the `markdown` attribute.

## Method: `_get_llm_description`

### Description
The `_get_llm_description` method generates a description of the image using the specified LLM client and model.

### Parameters
- `file_stream` (BinaryIO): The input stream of the image file.
- `stream_info` (StreamInfo): An object containing metadata about the stream.
- `client`: The LLM client used to generate the description.
- `model` (str): The model used by the LLM client.
- `prompt` (str, optional): A custom prompt for the LLM. Defaults to "Write a detailed caption for this image." if not provided.

### Returns
- `Union[None, str]`: Returns the generated description as a string, or `None` if an error occurs.

## Dependencies
- `exiftool`: Required for extracting metadata from images.
- LLM client: Required for generating descriptions of images.
- `base64`: Used for encoding the image data.
- `mimetypes`: Used for guessing the MIME type of the file if not provided.

## Usage Example
```python
from io import BytesIO

# Create an instance of ImageConverter
converter = ImageConverter()

# Prepare a file stream and stream info
file_stream = BytesIO(image_data)  # image_data is a byte representation of the image
stream_info = StreamInfo(mimetype='image/jpeg', extension='jpg')

# Check if the converter accepts the file
if converter.accepts(file_stream, stream_info):
    result = converter.convert(
        file_stream,
        stream_info,
        exiftool_path='/usr/local/bin/exiftool',
        llm_client=my_llm_client,
        llm_model='gpt-3.5-turbo',
        llm_prompt='Describe this image.'
    )
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
