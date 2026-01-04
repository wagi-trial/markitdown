# packages/markitdown/src/markitdown/_markitdown.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/_markitdown.py",
  "file_hash": "84fad9fb75883db1ad790ebd9d918910e0ef862be3bf19d27374b93d02da2057",
  "last_updated": "2026-01-04T17:17:15.201167+00:00",
  "functions": {
    "_load_plugins": {
      "hash": "4ecbc276cc454afd842c6a54f8e280ea85817ae8156db4d755d0c96479bdefc6",
      "lines": "65-84",
      "last_updated": "2026-01-04T17:17:00.731256+00:00"
    },
    "ConverterRegistration": {
      "hash": "4910ea4ac1db77323648a892ec98eb78527a4f267a17fb0e0def0038d8841996",
      "lines": "86-92",
      "last_updated": "2026-01-04T17:17:03.627770+00:00"
    },
    "MarkItDown": {
      "hash": "1f04401c9bf6a8c4a2bb7f3006302ea73362ae47c08587d5e43d46c94cfbe846",
      "lines": "93-777",
      "last_updated": "2026-01-04T17:17:15.201110+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/_markitdown.py` implements functionality for loading document converters and managing their registration for converting various file types and web pages into Markdown format. The primary operations include lazy loading of plugins, registering built-in converters, and managing their priorities for conversion tasks.

The file defines three main components: the function `_load_plugins`, the class `ConverterRegistration`, and the class `MarkItDown`. The `_load_plugins` function is responsible for loading plugins defined in the `markitdown.plugin` entry point group, handling any exceptions that occur during the loading process. The `ConverterRegistration` class is a data structure that encapsulates a document converter and its associated priority. The `MarkItDown` class serves as the main interface for the document reader, allowing for the enabling of built-in converters and plugins, and managing the registration of various document converters such as `PlainTextConverter`, `HtmlConverter`, and others.

Concrete dependencies in this file include standard libraries such as `mimetypes`, `os`, `re`, `shutil`, and `requests`, as well as third-party libraries like `magika` and `charset_normalizer`. The code also imports custom modules from the same package, including `_stream_info`, `_uri_utils`, and `_base_converter`. The data structures manipulated include lists for storing converters and a dataclass for converter registration, which utilizes type hints to specify the expected types of its attributes. The file also employs exception classes like `FileConversionException` and `UnsupportedFormatException` to handle specific error scenarios during conversion processes.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `_load_plugins`

<details>
<summary><strong>Calls/Dependencies</strong> (6 unique functions)</summary>

- `_load_plugins`
- `append`
- `entry_points`
- `format_exc`
- `load`
- `warn`

</details>

### `MarkItDown`

**Nested Functions:**
- `__init__`
- `enable_builtins`
- `enable_plugins`
- `convert`
- `convert_local`
- `convert_stream`
- `convert_url`
- `convert_uri`
- `convert_response`
- `_convert`
- `register_page_converter`
- `register_converter`
- `_get_stream_info_guesses`
- `_normalize_charset`

<details>
<summary><strong>Calls/Dependencies</strong> (103 unique functions)</summary>

- `AudioConverter`
- `BingSerpConverter`
- `BytesIO`
- `ConverterRegistration`
- `CsvConverter`
- `DocumentIntelligenceConverter`
- `DocxConverter`
- `EpubConverter`
- `FailedConversionAttempt`
- `FileConversionException`
- `Files`
- `HtmlConverter`
- `ImageConverter`
- `IpynbConverter`
- `Magika`
- `OutlookMsgConverter`
- `PRIORITY_SPECIFIC_FILE_FORMAT`
- `PdfConverter`
- `PlainTextConverter`
- `PptxConverter`
- `RssConverter`
- `Session`
- `StreamInfo`
- `TypeError`
- `UnsupportedFormatException`
- `ValueError`
- `WikipediaConverter`
- `XlsConverter`
- `XlsxConverter`
- `YouTubeConverter`
- `ZipConverter`
- `__init__`
- `_convert`
- `_get_stream_info_guesses`
- `_load_plugins`
- `_normalize_charset`
- `abspath`
- `accept`
- `accepts`
- `any`
- `append`
- `basename`
- `best`
- `callable`
- `charset`
- `content`
- `convert`
- `convert_local`
- `convert_response`
- `convert_stream`
- *(and 53 more...)*

</details>

</details>



## Functions and Classes

## `_load_plugins`

**Location:** [`packages/markitdown/src/markitdown/_markitdown.py:65`](/packages/markitdown/src/markitdown/_markitdown.py#L65-L84)

**Dependencies:** `_load_plugins`, `append`, `entry_points`, `format_exc`, `load`, `warn`  


# Documentation for `_load_plugins` Function

## Description
The `_load_plugins` function is responsible for lazily loading plugins defined in the entry points of the "markitdown.plugin" group. It checks if the plugins have already been loaded and, if not, proceeds to load them. If a plugin fails to load, a warning is issued, and the function continues loading the remaining plugins.

## Parameters
The function does not accept any parameters.

## Return Value
The function returns a value of type `Union[None, List[Any]]`. 
- If the plugins have already been loaded, it returns the existing list of plugins stored in the global variable `_plugins`.
- If the plugins are not loaded, it returns a new list containing the loaded plugins. If no plugins are successfully loaded, it returns an empty list.

## Dependencies
The function relies on the following external modules and functions:
- `entry_points`: This function is called to retrieve entry points for the "markitdown.plugin" group.
- `traceback`: This module is used to format the stack trace in case of an exception during plugin loading.
- `warn`: This function is called to issue a warning message when a plugin fails to load.
- `_plugins`: This is a global variable that stores the list of loaded plugins.

## Usage Example
```python
# Assuming the necessary imports and global variable _plugins are defined
_plugins = None  # Initialize the global variable

# Call the function to load plugins
loaded_plugins = _load_plugins()

# Check the loaded plugins
print(loaded_plugins)
```

---
## `ConverterRegistration`

**Location:** [`packages/markitdown/src/markitdown/_markitdown.py:86`](/packages/markitdown/src/markitdown/_markitdown.py#L86-L92)

# ConverterRegistration Documentation

## Overview
`ConverterRegistration` is a class that represents the registration of a converter along with its associated priority and other metadata. This class is designed to hold information about a specific converter, which is expected to be an instance of `DocumentConverter`.

## Attributes

### converter
- **Type**: `DocumentConverter`
- **Description**: This attribute holds an instance of the `DocumentConverter` class. It represents the converter that is being registered.

### priority
- **Type**: `float`
- **Description**: This attribute holds a floating-point number that indicates the priority of the converter. The priority can be used to determine the order in which converters are applied or executed.

## Return Value
The `ConverterRegistration` class does not have a return value as it is a class definition. Instances of this class will contain the attributes `converter` and `priority` as defined.

## Dependencies
The code explicitly references the `DocumentConverter` class. There are no other external modules, APIs, or services invoked in the provided code.

## Usage Example
To create an instance of `ConverterRegistration`, you would need to first create an instance of `DocumentConverter`. Below is an example of how to instantiate `ConverterRegistration`:

```python
# Assuming DocumentConverter is defined elsewhere
document_converter_instance = DocumentConverter()  # Create an instance of DocumentConverter
registration = ConverterRegistration()  # Create an instance of ConverterRegistration
registration.converter = document_converter_instance  # Assign the DocumentConverter instance
registration.priority = 1.0  # Set the priority
```

This example demonstrates how to instantiate the `ConverterRegistration` class and assign values to its attributes.

---
## `MarkItDown`

**Location:** [`packages/markitdown/src/markitdown/_markitdown.py:93`](/packages/markitdown/src/markitdown/_markitdown.py#L93-L777)

**Nested Functions:** `__init__`, `enable_builtins`, `enable_plugins`, `convert`, `convert_local`, `convert_stream`, `convert_url`, `convert_uri`, `convert_response`, `_convert`, `register_page_converter`, `register_converter`, `_get_stream_info_guesses`, `_normalize_charset`  
**Dependencies:** `AudioConverter`, `BingSerpConverter`, `BytesIO`, `ConverterRegistration`, `CsvConverter`, `DocumentIntelligenceConverter`, `DocxConverter`, `EpubConverter`, `FailedConversionAttempt`, `FileConversionException`, `Files`, `HtmlConverter`, `ImageConverter`, `IpynbConverter`, `Magika` *(+88 more)*  


# MarkItDown Class Documentation

## Overview
The `MarkItDown` class is a text-based document reader designed to convert various file types or webpages into Markdown format. It supports built-in converters and can also utilize plugins for additional functionality.

## Constructor: `__init__`
The constructor initializes the `MarkItDown` instance and sets up the necessary configurations.

### Parameters
- `enable_builtins` (Union[None, bool], optional): Controls whether built-in converters are enabled. Defaults to `None`, which enables built-ins by default.
- `enable_plugins` (Union[None, bool], optional): Controls whether plugin converters are enabled. Defaults to `None`.
- `**kwargs`: Additional keyword arguments that may include:
  - `requests_session` (requests.Session, optional): A custom requests session to be used for HTTP requests.
  - `llm_client` (Any, optional): Client for LLM operations.
  - `llm_model` (Union[str, None], optional): Model identifier for LLM.
  - `llm_prompt` (Union[str, None], optional): Prompt for LLM.
  - `exiftool_path` (Union[str, None], optional): Path to the ExifTool executable.
  - `style_map` (Union[str, None], optional): Style mapping for conversion.
  - `docintel_endpoint` (Union[str, None], optional): Endpoint for Document Intelligence services.
  - `docintel_credential` (Union[str, None], optional): Credentials for Document Intelligence services.
  - `docintel_file_types` (Union[List[str], None], optional): File types for Document Intelligence services.
  - `docintel_api_version` (Union[str, None], optional): API version for Document Intelligence services.

### Return Value
The constructor does not return a value.

## Method: `enable_builtins`
Enables and registers built-in converters.

### Parameters
- `**kwargs`: Additional keyword arguments passed to the method.

### Return Value
This method does not return a value.

## Method: `enable_plugins`
Enables and registers converters provided by plugins.

### Parameters
- `**kwargs`: Additional keyword arguments passed to the method.

### Return Value
This method does not return a value.

## Method: `convert`
Converts a source document into Markdown format.

### Parameters
- `source` (Union[str, requests.Response, Path, BinaryIO]): The source can be a path (string or Path), URL, or a requests response object.
- `stream_info` (Optional[StreamInfo], optional): Additional stream information for conversion. If `None`, it is inferred from the source.
- `**kwargs`: Additional arguments passed to the converter.

### Return Value
Returns a `DocumentConverterResult` containing the converted Markdown content.

## Method: `convert_local`
Converts a local file into Markdown format.

### Parameters
- `path` (Union[str, Path]): The path to the local file.
- `stream_info` (Optional[StreamInfo], optional): Additional stream information for conversion.
- `file_extension` (Optional[str], optional): Deprecated; use `stream_info` instead.
- `url` (Optional[str], optional): Deprecated; use `stream_info` instead.
- `**kwargs`: Additional arguments passed to the converter.

### Return Value
Returns a `DocumentConverterResult` containing the converted Markdown content.

## Method: `convert_stream`
Converts a binary stream into Markdown format.

### Parameters
- `stream` (BinaryIO): The binary stream to convert.
- `stream_info` (Optional[StreamInfo], optional): Additional stream information for conversion.
- `file_extension` (Optional[str], optional): Deprecated; use `stream_info` instead.
- `url` (Optional[str], optional): Deprecated; use `stream_info` instead.
- `**kwargs`: Additional arguments passed to the converter.

### Return Value
Returns a `DocumentConverterResult` containing the converted Markdown content.

## Method: `convert_url`
Converts a URL into Markdown format.

### Parameters
- `url` (str): The URL to convert.
- `stream_info` (Optional[StreamInfo], optional): Additional stream information for conversion.
- `file_extension` (Optional[str], optional): Deprecated; use `stream_info` instead.
- `mock_url` (Optional[str], optional): Mock the request as if it came from a different URL.
- `**kwargs`: Additional arguments passed to the converter.

### Return Value
Returns a `DocumentConverterResult` containing the converted Markdown content.

## Method: `convert_uri`
Converts a URI into Markdown format.

### Parameters
- `uri` (str): The URI to convert.
- `stream_info` (Optional[StreamInfo], optional): Additional stream information for conversion.
- `file_extension` (Optional[str], optional): Deprecated; use `stream_info` instead.
- `mock_url` (Optional[str], optional): Mock the request as if it came from a different URL.
- `**kwargs`: Additional arguments passed to the converter.

### Return Value
Returns a `DocumentConverterResult` containing the converted Markdown content.

## Method: `convert_response`
Converts a `requests.Response` object into Markdown format.

### Parameters
- `response` (requests.Response): The response object to convert.
- `stream_info` (Optional[StreamInfo], optional): Additional stream information for conversion.
- `file_extension` (Optional[str], optional): Deprecated; use `stream_info` instead.
- `url` (Optional[str], optional): Deprecated; use `stream_info` instead.
- `**kwargs`: Additional arguments passed to the converter.

### Return Value
Returns a `DocumentConverterResult` containing the converted Markdown content.

## Dependencies
- `requests`: Used for making HTTP requests.
- `os`: Used for file path operations.
- `shutil`: Used for locating executables.
- `re`: Used for regular expressions.
- `traceback`: Used for error handling.
- `mimetypes`: Used for MIME type guessing.
- `io`: Used for handling binary streams.
- `magika`: Used for identifying file types from streams.
- `charset_normalizer`: Used for guessing character sets.

## Usage Example
```python
from markitdown import MarkItDown

# Create an instance of MarkItDown
reader = MarkItDown()

# Convert a local file to Markdown
result = reader.convert("example.txt")

# Print the converted Markdown content
print(result.text_content)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
