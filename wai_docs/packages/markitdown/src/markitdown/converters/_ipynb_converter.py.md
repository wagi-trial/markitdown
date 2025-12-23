# packages/markitdown/src/markitdown/converters/_ipynb_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_ipynb_converter.py",
  "file_hash": "32ae36fe7f395dbc5c0a3fd3f09b62f2e7c96dba77362530c4f325a7f19ab70e",
  "last_updated": "2025-12-23T15:50:48.779593+00:00",
  "functions": {
    "IpynbConverter": {
      "hash": "d6135afb5c2e77fa50e432305a1c4f41d906121bffaad99a204ccc64c07927c6",
      "lines": "15-97",
      "last_updated": "2025-12-23T15:50:48.779465+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_ipynb_converter.py` implements functionality for converting Jupyter Notebook files (.ipynb) into Markdown format. It defines the `IpynbConverter` class, which extends the `DocumentConverter` class. This class includes methods for accepting input files based on their MIME type and extension, as well as converting the content of the notebooks into Markdown format.

The main methods in the `IpynbConverter` class are `accepts`, `convert`, and `_convert`. The `accepts` method checks if the provided file stream is a valid Jupyter Notebook by examining its MIME type and file extension, and by reading its content to verify the presence of specific JSON keys. The `convert` method reads the notebook content, decodes it, and calls the `_convert` method, which processes the JSON structure of the notebook to generate Markdown output. The `_convert` method handles different cell types (markdown, code, and raw) and constructs the corresponding Markdown representation, while also attempting to extract a title from the notebook's metadata or the first markdown cell.

The file imports several modules, including `BinaryIO`, `Any`, and `json` from the standard library, as well as custom modules such as `DocumentConverter`, `DocumentConverterResult`, `FileConversionException`, and `StreamInfo`. It utilizes data structures such as lists for accepted file extensions and MIME type prefixes, and it manipulates dictionaries to access the JSON content of the Jupyter Notebook. The class also raises a `FileConversionException` in case of errors during the conversion process, ensuring that any issues are properly reported.

## Functions and Classes

## `IpynbConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_ipynb_converter.py:15`](/packages/markitdown/src/markitdown/converters/_ipynb_converter.py#L15-L97)

# IpynbConverter Documentation

## Overview
`IpynbConverter` is a class that extends `DocumentConverter` and is responsible for converting Jupyter Notebook files (with the `.ipynb` extension) into Markdown format. The conversion process involves reading the notebook's JSON content and formatting it appropriately based on the types of cells present in the notebook.

## Methods

### accepts

```python
def accepts(
    self,
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> bool
```

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the contents of the file to be checked for acceptance.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `mimetype` (str): The MIME type of the file, which is checked against predefined prefixes.
  - `extension` (str): The file extension, which is checked against accepted file extensions.
- `**kwargs` (Any): Additional options that can be passed to the converter, not utilized in this method.

#### Returns
- `bool`: Returns `True` if the file is accepted for conversion (either by extension or by MIME type indicating it is a Jupyter Notebook), otherwise returns `False`.

### convert

```python
def convert(
    self,
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> DocumentConverterResult
```

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the contents of the Jupyter Notebook file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including the character set for decoding.
- `**kwargs` (Any): Additional options that can be passed to the converter, not utilized in this method.

#### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): The converted Markdown text generated from the notebook.
  - `title` (str or None): The title extracted from the notebook metadata or the first Markdown cell heading.

### _convert

```python
def _convert(self, notebook_content: dict) -> DocumentConverterResult
```

#### Parameters
- `notebook_content` (dict): A dictionary representation of the Jupyter Notebook's JSON content.

#### Returns
- `DocumentConverterResult`: An object containing the converted Markdown text and the title.

## Exceptions
- `FileConversionException`: Raised if an error occurs during the conversion process, with a message detailing the error.

## Dependencies
- The class relies on the following external modules:
  - `json`: Used to parse the JSON content of the Jupyter Notebook.
  - `DocumentConverter`: The parent class that `IpynbConverter` extends.
  - `DocumentConverterResult`: The data structure returned by the `convert` method.
  - `StreamInfo`: A data structure that provides information about the file stream.

## Usage Example

```python
from io import BytesIO

# Create an instance of IpynbConverter
converter = IpynbConverter()

# Example file stream and stream info
file_stream = BytesIO(b'{"cells":[{"cell_type":"markdown","source":["# Title"]},{"cell_type":"code","source":["print(\\"Hello World\\")"]}],"metadata":{}}')
stream_info = StreamInfo(mimetype="application/json", extension=".ipynb", charset="utf-8")

# Check if the converter accepts the file
if converter.accepts(file_stream, stream_info):
    # Convert the file
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)  # Outputs the converted Markdown
    print(result.title)      # Outputs the title extracted from the notebook
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
