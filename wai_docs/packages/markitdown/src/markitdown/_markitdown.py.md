# packages/markitdown/src/markitdown/_markitdown.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/_markitdown.py",
  "file_hash": "84fad9fb75883db1ad790ebd9d918910e0ef862be3bf19d27374b93d02da2057",
  "last_updated": "2025-12-23T15:46:41.610091+00:00",
  "functions": {
    "_load_plugins": {
      "hash": "4ecbc276cc454afd842c6a54f8e280ea85817ae8156db4d755d0c96479bdefc6",
      "lines": "65-84",
      "last_updated": "2025-12-23T15:46:25.644306+00:00"
    },
    "ConverterRegistration": {
      "hash": "4910ea4ac1db77323648a892ec98eb78527a4f267a17fb0e0def0038d8841996",
      "lines": "86-92",
      "last_updated": "2025-12-23T15:46:29.405817+00:00"
    },
    "MarkItDown": {
      "hash": "1f04401c9bf6a8c4a2bb7f3006302ea73362ae47c08587d5e43d46c94cfbe846",
      "lines": "93-777",
      "last_updated": "2025-12-23T15:46:41.610013+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/_markitdown.py` implements functionality for converting various document types and web content into Markdown format. It includes a plugin loading mechanism, a registration system for document converters, and a primary class that orchestrates the conversion process. The file defines the `_load_plugins` function, which lazily loads plugins from the `markitdown.plugin` entry point group, handling any exceptions that occur during the loading process. The `MarkItDown` class serves as the main interface for users to enable built-in converters and plugins, manage requests, and register document converters.

The main classes and functions in the file include:
- `_load_plugins`: A function that loads plugins if they have not already been loaded.
- `ConverterRegistration`: A data class that encapsulates a document converter along with its priority.
- `MarkItDown`: A class that manages the conversion process, initializes built-in and plugin converters, and handles various configurations through its constructor.

The code explicitly imports several modules and classes, including `mimetypes`, `os`, `requests`, and various document converter classes such as `PlainTextConverter`, `HtmlConverter`, and `PdfConverter`. It also utilizes the `requests` library for HTTP requests and `magika` for document processing. The file defines data structures such as `ConverterRegistration`, which uses type hints to specify that it contains a `DocumentConverter` and a `float` priority. The file manipulates lists and dictionaries to manage converters and their configurations, ensuring that specific converters are prioritized over more generic ones during the conversion process.

## Functions and Classes

## `_load_plugins`

**Location:** [`packages/markitdown/src/markitdown/_markitdown.py:65`](/packages/markitdown/src/markitdown/_markitdown.py#L65-L84)

# Documentation for `_load_plugins` Function

## Overview
The `_load_plugins` function is responsible for lazily loading plugins defined in the entry points of the "markitdown.plugin" group. It checks if plugins have already been loaded and, if not, proceeds to load them and handle any exceptions that occur during the loading process.

## Parameters
The function does not accept any parameters.

## Return Value
The function returns a value of type `Union[None, List[Any]]`:
- If plugins have already been loaded, it returns the existing list of plugins stored in the global variable `_plugins`.
- If plugins are loaded for the first time, it returns a list of loaded plugins. If an error occurs while loading a plugin, that plugin is skipped, and a warning is issued.

## Dependencies
The function relies on the following external components:
- `global _plugins`: A global variable that stores the loaded plugins.
- `entry_points`: A function or method that retrieves entry points for the specified group ("markitdown.plugin").
- `traceback`: A module used to format exceptions that occur during plugin loading.
- `warn`: A function that issues a warning message when a plugin fails to load.

## Usage Example
To invoke the `_load_plugins` function, simply call it without any arguments:

```python
loaded_plugins = _load_plugins()
``` 

This call will either return the already loaded plugins or load new plugins from the specified entry points and return them.

---
## `ConverterRegistration`

**Location:** [`packages/markitdown/src/markitdown/_markitdown.py:86`](/packages/markitdown/src/markitdown/_markitdown.py#L86-L92)

# ConverterRegistration Documentation

## Overview
`ConverterRegistration` is a class that encapsulates the registration of a converter along with its associated priority and other metadata. It is designed to hold information about a specific converter implementation.

## Attributes

### converter
- **Type**: `DocumentConverter`
- **Description**: This attribute holds an instance of the `DocumentConverter` class. It represents the converter that is being registered.

### priority
- **Type**: `float`
- **Description**: This attribute specifies the priority of the converter. The priority is a numerical value that can be used to determine the order in which converters are applied or processed.

## Return Value
The `ConverterRegistration` class does not have a return value as it is a class definition. Instances of this class will contain the `converter` and `priority` attributes as defined.

## Dependencies
The code references the `DocumentConverter` class. The implementation of `DocumentConverter` is not provided in the code snippet, but it is required for the `converter` attribute.

## Usage Example
To create an instance of `ConverterRegistration`, you would need to have an instance of `DocumentConverter` available. Below is an example of how to instantiate `ConverterRegistration`:

```python
# Assuming DocumentConverter is defined elsewhere
document_converter_instance = DocumentConverter()  # Create an instance of DocumentConverter
registration = ConverterRegistration()
registration.converter = document_converter_instance
registration.priority = 1.0  # Set the priority
```

In this example, an instance of `DocumentConverter` is created and assigned to the `converter` attribute of `ConverterRegistration`, and a priority value is set.

---
## `MarkItDown`

**Location:** [`packages/markitdown/src/markitdown/_markitdown.py:93`](/packages/markitdown/src/markitdown/_markitdown.py#L93-L777)

# MarkItDown Class Documentation

## Overview
The `MarkItDown` class is a text-based document reader designed to convert various file types or webpages into Markdown format. It supports built-in converters and can be extended with plugins.

## Constructor: `__init__`
The constructor initializes the `MarkItDown` instance.

### Parameters
- `enable_builtins: Union[None, bool]`
  - Default: `None`
  - If `None` or `True`, built-in converters are enabled. If `False`, built-in converters are not enabled.
  
- `enable_plugins: Union[None, bool]`
  - Default: `None`
  - If `True`, plugin converters are enabled. If `False`, plugin converters are not enabled.

- `**kwargs`
  - Additional keyword arguments that can include:
    - `requests_session`: A custom `requests.Session` object for making HTTP requests.
    - `llm_client`: Client for LLM (Large Language Model) operations.
    - `llm_model`: Model identifier for LLM.
    - `llm_prompt`: Prompt for LLM.
    - `exiftool_path`: Path to the ExifTool executable.
    - `style_map`: A mapping for styles.
    - `docintel_endpoint`: Endpoint for Document Intelligence services.
    - `docintel_credential`: Credential for Document Intelligence services.
    - `docintel_file_types`: File types for Document Intelligence services.
    - `docintel_api_version`: API version for Document Intelligence services.

### Return Value
The constructor does not return a value. It initializes the instance variables and registers converters based on the provided parameters.

## Method: `enable_builtins`
Enables and registers built-in converters.

### Parameters
- `**kwargs`
  - Additional keyword arguments passed to the method for converter registration.

### Return Value
This method does not return a value.

## Method: `enable_plugins`
Enables and registers converters provided by plugins.

### Parameters
- `**kwargs`
  - Additional keyword arguments passed to the method for plugin registration.

### Return Value
This method does not return a value.

## Method: `convert`
Converts a given source into Markdown format.

### Parameters
- `source: Union[str, requests.Response, Path, BinaryIO]`
  - The source can be a file path (string or `Path`), a URL, a `requests.Response` object, or a binary stream.
  
- `stream_info: Optional[StreamInfo]`
  - Optional stream information to use for the conversion. If `None`, it is inferred from the source.
  
- `**kwargs: Any`
  - Additional arguments passed to the converter.

### Return Value
- Returns a `DocumentConverterResult` object containing the converted Markdown content.

## Method: `convert_local`
Converts a local file into Markdown format.

### Parameters
- `path: Union[str, Path]`
  - The local file path to convert.
  
- `stream_info: Optional[StreamInfo]`
  - Optional stream information for the conversion.
  
- `file_extension: Optional[str]`
  - Deprecated. Use `stream_info` instead.
  
- `url: Optional[str]`
  - Deprecated. Use `stream_info` instead.
  
- `**kwargs: Any`
  - Additional arguments passed to the converter.

### Return Value
- Returns a `DocumentConverterResult` object containing the converted Markdown content.

## Method: `convert_stream`
Converts a binary stream into Markdown format.

### Parameters
- `stream: BinaryIO`
  - The binary stream to convert.
  
- `stream_info: Optional[StreamInfo]`
  - Optional stream information for the conversion.
  
- `file_extension: Optional[str]`
  - Deprecated. Use `stream_info` instead.
  
- `url: Optional[str]`
  - Deprecated. Use `stream_info` instead.
  
- `**kwargs: Any`
  - Additional arguments passed to the converter.

### Return Value
- Returns a `DocumentConverterResult` object containing the converted Markdown content.

## Method: `convert_url`
Converts a URL into Markdown format.

### Parameters
- `url: str`
  - The URL to convert.
  
- `stream_info: Optional[StreamInfo]`
  - Optional stream information for the conversion.
  
- `file_extension: Optional[str]`
  - Deprecated. Use `stream_info` instead.
  
- `mock_url: Optional[str]`
  - Mock the request as if it came from a different URL.
  
- `**kwargs: Any`
  - Additional arguments passed to the converter.

### Return Value
- Returns a `DocumentConverterResult` object containing the converted Markdown content.

## Method: `convert_uri`
Converts a URI into Markdown format.

### Parameters
- `uri: str`
  - The URI to convert.
  
- `stream_info: Optional[StreamInfo]`
  - Optional stream information for the conversion.
  
- `file_extension: Optional[str]`
  - Deprecated. Use `stream_info` instead.
  
- `mock_url: Optional[str]`
  - Mock the request as if it came from a different URL.
  
- `**kwargs: Any`
  - Additional arguments passed to the converter.

### Return Value
- Returns a `DocumentConverterResult` object containing the converted Markdown content.

## Method: `convert_response`
Converts a `requests.Response` object into Markdown format.

### Parameters
- `response: requests.Response`
  - The response object to convert.
  
- `stream_info: Optional[StreamInfo]`
  - Optional stream information for the conversion.
  
- `file_extension: Optional[str]`
  - Deprecated. Use `stream_info` instead.
  
- `url: Optional[str]`
  - Deprecated. Use `stream_info` instead.
  
- `**kwargs: Any`
  - Additional arguments passed to the converter.

### Return Value
- Returns a `DocumentConverterResult` object containing the converted Markdown content.

## Dependencies
- `requests`: For making HTTP requests.
- `os`: For file path operations.
- `shutil`: For locating executables.
- `re`: For regular expression operations.
- `traceback`: For error handling.
- `mimetypes`: For MIME type guessing.
- `io`: For handling binary streams.
- `magika`: For identifying file types based on content.
- `charset_normalizer`: For detecting character sets.

## Example Usage
```python
from markitdown import MarkItDown

# Create an instance of MarkItDown
reader = MarkItDown(enable_builtins=True, enable_plugins=False)

# Convert a local file to Markdown
result = reader.convert("example.docx")

# Print the converted Markdown content
print(result.text_content)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
