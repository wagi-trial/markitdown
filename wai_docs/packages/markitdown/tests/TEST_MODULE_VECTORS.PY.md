# packages/markitdown/tests/test_module_vectors.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/tests/test_module_vectors.py",
  "file_hash": "5beede9a668820885154cec341d94f0fc4705c81208e8acf92b61200a4cc9eec",
  "last_updated": "2026-01-04T17:32:00.058874+00:00",
  "functions": {
    "test_guess_stream_info": {
      "hash": "4e6b2c735a6029b983be5b66c117ffccee858c67b853fafa5763fb6bd0d7d713",
      "lines": "28-56",
      "last_updated": "2026-01-04T17:31:32.825024+00:00"
    },
    "test_convert_local": {
      "hash": "0bcbe41497cef57ff96b53aa48847959fab2360481558338518f8c67a93ffc71",
      "lines": "58-70",
      "last_updated": "2026-01-04T17:31:36.410732+00:00"
    },
    "test_convert_stream_with_hints": {
      "hash": "f0c7b15dfa5f2b0950169299acc1c26f61af65349a578278b509e60625575dad",
      "lines": "72-91",
      "last_updated": "2026-01-04T17:31:39.993146+00:00"
    },
    "test_convert_stream_without_hints": {
      "hash": "8c4c8c153be8a1afcc64445196fc8e130fe73cc570aac7b52ad530db8bb4dab8",
      "lines": "93-104",
      "last_updated": "2026-01-04T17:31:43.791511+00:00"
    },
    "test_convert_http_uri": {
      "hash": "e44bd03c63e486861c48192532f9a7774d6ec993a1bee417ada85c099d3668ab",
      "lines": "110-125",
      "last_updated": "2026-01-04T17:31:46.985463+00:00"
    },
    "test_convert_file_uri": {
      "hash": "c79c87dd87cf00be195fcb677aa80b3cb2ce1965f072d8c9361de08c8fd97e9b",
      "lines": "127-140",
      "last_updated": "2026-01-04T17:31:50.429962+00:00"
    },
    "test_convert_data_uri": {
      "hash": "7a567dc3b5cba17d2c5fe2d81043b000412e349259ac10181dd9353e3ca77b5e",
      "lines": "142-161",
      "last_updated": "2026-01-04T17:31:53.658781+00:00"
    },
    "test_convert_keep_data_uris": {
      "hash": "7e5f9b60a3e356e4979499e909826ac827c97f727853416ceba314e7e7a02523",
      "lines": "163-179",
      "last_updated": "2026-01-04T17:31:56.375024+00:00"
    },
    "test_convert_stream_keep_data_uris": {
      "hash": "13cf6aa6bff05461c685e48d2e98eecf08c9ff1073fc3a7aae49d66c98052afd",
      "lines": "181-201",
      "last_updated": "2026-01-04T17:32:00.058809+00:00"
    }
  }
}
```

</details>



The Python file `test_module_vectors.py` implements a series of unit tests for the `MarkItDown` library, specifically focusing on the conversion of various input streams into Markdown format. The tests validate the functionality of the `MarkItDown` class by checking its ability to guess stream information, convert local files, and handle different types of URIs including HTTP, file, and data URIs. The tests are designed to ensure that the output Markdown contains expected strings while excluding others, thereby verifying the correctness of the conversion process.

The file defines several test functions, each responsible for a specific aspect of the conversion process:
- `test_guess_stream_info`: Tests the ability of `MarkItDown` to infer stream information from a file.
- `test_convert_local`: Tests the conversion of a local file to Markdown.
- `test_convert_stream_with_hints`: Tests conversion when stream information is provided.
- `test_convert_stream_without_hints`: Tests conversion without any stream information.
- `test_convert_http_uri`: Tests conversion from an HTTP/HTTPS URI.
- `test_convert_file_uri`: Tests conversion from a file URI.
- `test_convert_data_uri`: Tests conversion from a data URI.
- `test_convert_keep_data_uris`: Tests conversion while preserving data URIs.
- `test_convert_stream_keep_data_uris`: Tests stream conversion with data URIs preserved.

The code imports several modules, including `os`, `time`, `pytest`, and `base64`, as well as `Path` from the `pathlib` module. It also imports `MarkItDown` and `StreamInfo` from the `markitdown` package. The tests utilize environmental variables to conditionally skip tests that query external URLs when running in CI environments. The data structures manipulated in the tests include instances of `StreamInfo`, which encapsulate metadata about the streams being processed, and various test vectors defined in the imported `_test_vectors` module, which provide input data and expected outcomes for the tests.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `test_guess_stream_info`

<details>
<summary><strong>Calls/Dependencies</strong> (8 unique functions)</summary>

- `MarkItDown`
- `StreamInfo`
- `_get_stream_info_guesses`
- `basename`
- `join`
- `open`
- `splitext`
- `test_guess_stream_info`

</details>

### `test_convert_local`

<details>
<summary><strong>Calls/Dependencies</strong> (4 unique functions)</summary>

- `MarkItDown`
- `convert`
- `join`
- `test_convert_local`

</details>

### `test_convert_stream_with_hints`

<details>
<summary><strong>Calls/Dependencies</strong> (7 unique functions)</summary>

- `MarkItDown`
- `StreamInfo`
- `convert`
- `join`
- `open`
- `splitext`
- `test_convert_stream_with_hints`

</details>

### `test_convert_stream_without_hints`

<details>
<summary><strong>Calls/Dependencies</strong> (5 unique functions)</summary>

- `MarkItDown`
- `convert`
- `join`
- `open`
- `test_convert_stream_without_hints`

</details>

### `test_convert_http_uri`

<details>
<summary><strong>Calls/Dependencies</strong> (4 unique functions)</summary>

- `MarkItDown`
- `convert`
- `sleep`
- `test_convert_http_uri`

</details>

### `test_convert_file_uri`

<details>
<summary><strong>Calls/Dependencies</strong> (6 unique functions)</summary>

- `MarkItDown`
- `Path`
- `as_uri`
- `convert`
- `join`
- `test_convert_file_uri`

</details>

### `test_convert_data_uri`

<details>
<summary><strong>Calls/Dependencies</strong> (8 unique functions)</summary>

- `MarkItDown`
- `b64encode`
- `convert`
- `decode`
- `join`
- `open`
- `read`
- `test_convert_data_uri`

</details>

### `test_convert_keep_data_uris`

<details>
<summary><strong>Calls/Dependencies</strong> (4 unique functions)</summary>

- `MarkItDown`
- `convert`
- `join`
- `test_convert_keep_data_uris`

</details>

### `test_convert_stream_keep_data_uris`

<details>
<summary><strong>Calls/Dependencies</strong> (7 unique functions)</summary>

- `MarkItDown`
- `StreamInfo`
- `convert`
- `join`
- `open`
- `splitext`
- `test_convert_stream_keep_data_uris`

</details>

</details>



## Functions and Classes

## `test_guess_stream_info`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:28`](/packages/markitdown/tests/test_module_vectors.py#L28-L56)

**Dependencies:** `MarkItDown`, `StreamInfo`, `_get_stream_info_guesses`, `basename`, `join`, `open`, `splitext`, `test_guess_stream_info`  


# Function Documentation: test_guess_stream_info

## Description
The `test_guess_stream_info` function tests the ability of the `MarkItDown` class to guess stream information based on a provided test vector. It reads a file from a specified local path, generates guesses for its stream information, and asserts that the first guess matches the expected MIME type, file extension, and character set defined in the test vector.

## Parameters
- `test_vector` (Type: `object`): An object containing the following attributes:
  - `filename` (Type: `str`): The name of the file to be tested. This is used to construct the local file path and to check against specific exceptions.
  - `mimetype` (Type: `str`): The expected MIME type of the file. This is used for assertion to verify the first guess's MIME type.
  - `charset` (Type: `str`): The expected character set of the file. This is used for assertion to verify the first guess's character set.

## Return Value
The function does not return any value. It performs assertions to validate the guessed stream information against the expected values. If the assertions fail, an `AssertionError` will be raised.

## Dependencies
- `os`: This module is used to handle file path operations.
- `MarkItDown`: This class is instantiated to access the `_get_stream_info_guesses` method.
- `StreamInfo`: This class is used to create a base guess object containing the filename, local path, and expected extension.

## Usage Example
```python
class TestVector:
    def __init__(self, filename, mimetype, charset):
        self.filename = filename
        self.mimetype = mimetype
        self.charset = charset

test_vector = TestVector("example_file.txt", "text/plain", "UTF-8")
test_guess_stream_info(test_vector)
```

---
## `test_convert_local`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:58`](/packages/markitdown/tests/test_module_vectors.py#L58-L70)

**Dependencies:** `MarkItDown`, `convert`, `join`, `test_convert_local`  


# Function Documentation: `test_convert_local`

## Description
The `test_convert_local` function tests the conversion of a local file using the `MarkItDown` class. It verifies that the output of the conversion contains certain expected strings and does not contain others.

## Parameters
- `test_vector` (Type: `object`): 
  - This parameter is expected to be an object that contains the following attributes:
    - `filename` (Type: `str`): The name of the file to be converted. This is used to construct the full path to the file by joining it with the `TEST_FILES_DIR` directory.
    - `url` (Type: `str`): A URL that may be passed to the `convert` method of the `MarkItDown` class.
    - `must_include` (Type: `list` of `str`): A list of strings that must be present in the conversion result.
    - `must_not_include` (Type: `list` of `str`): A list of strings that must not be present in the conversion result.

## Return Value
The function does not return a value. Instead, it asserts conditions based on the content of the `result.markdown` output from the `convert` method. If any assertion fails, an `AssertionError` is raised.

## Dependencies
- `MarkItDown`: This class is instantiated within the function and is expected to have a method called `convert`.
- `os`: The `os.path.join` function is used to construct the file path.
- `TEST_FILES_DIR`: This variable is expected to be defined in the scope where the function is called, representing the directory containing test files.

## Usage Example
```python
# Assuming the necessary imports and definitions are in place
class TestVector:
    def __init__(self, filename, url, must_include, must_not_include):
        self.filename = filename
        self.url = url
        self.must_include = must_include
        self.must_not_include = must_not_include

test_vector = TestVector(
    filename='example.md',
    url='http://example.com',
    must_include=['Expected String'],
    must_not_include=['Unexpected String']
)

test_convert_local(test_vector)
```

---
## `test_convert_stream_with_hints`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:72`](/packages/markitdown/tests/test_module_vectors.py#L72-L91)

**Dependencies:** `MarkItDown`, `StreamInfo`, `convert`, `join`, `open`, `splitext`, `test_convert_stream_with_hints`  


# Function Documentation: `test_convert_stream_with_hints`

## Description
The `test_convert_stream_with_hints` function tests the conversion of a stream using the `MarkItDown` class. It verifies that the resulting markdown output contains specific strings and does not contain others, based on the provided test vector.

## Parameters
- `test_vector`: An object that contains the following attributes:
  - `filename` (str): The name of the file to be opened for reading as a binary stream.
  - `mimetype` (str): The MIME type of the file, used in the `StreamInfo` object.
  - `charset` (str): The character set of the file, used in the `StreamInfo` object.
  - `url` (str): A URL associated with the test vector, passed to the `convert` method.
  - `must_include` (list of str): A list of strings that must be present in the resulting markdown output.
  - `must_not_include` (list of str): A list of strings that must not be present in the resulting markdown output.

## Return Value
The function does not return a value. It performs assertions to validate the contents of the markdown output generated by the `MarkItDown.convert` method.

## Dependencies
- `os`: Used for file path manipulation with `os.path.splitext` and `os.path.join`.
- `MarkItDown`: A class that provides a `convert` method for converting streams to markdown.
- `StreamInfo`: A class used to encapsulate information about the stream, including its extension, MIME type, and character set.

## Usage Example
```python
test_vector = {
    'filename': 'example_file.txt',
    'mimetype': 'text/plain',
    'charset': 'utf-8',
    'url': 'http://example.com',
    'must_include': ['expected string 1', 'expected string 2'],
    'must_not_include': ['unexpected string 1', 'unexpected string 2']
}

test_convert_stream_with_hints(test_vector)
```

---
## `test_convert_stream_without_hints`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:93`](/packages/markitdown/tests/test_module_vectors.py#L93-L104)

**Dependencies:** `MarkItDown`, `convert`, `join`, `open`, `test_convert_stream_without_hints`  


# Function Documentation: test_convert_stream_without_hints

## Description
The `test_convert_stream_without_hints` function tests the conversion of a stream that does not contain any stream information. It uses the `MarkItDown` class to convert the content of a specified file and verifies that certain strings are included or excluded from the resulting markdown output.

## Parameters
- `test_vector` (Type: `object`): An object that contains the following attributes:
  - `filename` (Type: `str`): The name of the file to be opened and converted. This file is located in the directory specified by `TEST_FILES_DIR`.
  - `url` (Type: `str`): A URL that is passed to the `convert` method of the `MarkItDown` instance.
  - `must_include` (Type: `list` of `str`): A list of strings that must be present in the resulting markdown output.
  - `must_not_include` (Type: `list` of `str`): A list of strings that must not be present in the resulting markdown output.

## Return Value
The function does not return a value. It performs assertions to validate the content of the markdown output generated by the `MarkItDown.convert` method.

## Dependencies
- `os`: The `os` module is used to construct the file path for the test file.
- `MarkItDown`: An instance of the `MarkItDown` class is created to perform the conversion of the stream.
- `TEST_FILES_DIR`: A predefined constant that specifies the directory where test files are located.

## Usage Example
```python
test_vector = {
    'filename': 'example_file.md',
    'url': 'http://example.com',
    'must_include': ['expected string 1', 'expected string 2'],
    'must_not_include': ['unexpected string 1', 'unexpected string 2']
}
test_convert_stream_without_hints(test_vector)
```

---
## `test_convert_http_uri`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:110`](/packages/markitdown/tests/test_module_vectors.py#L110-L125)

**Dependencies:** `MarkItDown`, `convert`, `sleep`, `test_convert_http_uri`  


# Function Documentation: test_convert_http_uri

## Description
The `test_convert_http_uri` function tests the conversion of an HTTP or HTTPS URI using the `MarkItDown` class. It verifies that the resulting markdown output contains specific strings and does not contain others, based on the provided test vector.

## Parameters
- **test_vector** (Type: `TestVector`)
  - Constraints: Must be an instance of the `TestVector` class.
  - Usage: 
    - `test_vector.filename` is used to construct the URI for the conversion.
    - `test_vector.url` is passed as a mock URL for locating the file.
    - `test_vector.must_include` is a list of strings that must be present in the resulting markdown.
    - `test_vector.must_not_include` is a list of strings that must not be present in the resulting markdown.

## Return Value
- The function does not return a value. It performs assertions to validate the content of the `result.markdown`.

## Dependencies
- **MarkItDown**: The function instantiates an object of the `MarkItDown` class to perform the conversion.
- **time**: The function uses `time.sleep(1)` to pause execution for 1 second to avoid hitting rate limits.
- **TEST_FILES_URL**: This variable is used to construct the URL for the file to be converted. It must be defined in the scope where this function is called.
- **assert**: The function uses assertions to check for the presence and absence of strings in the resulting markdown.

## Usage Example
```python
test_vector = TestVector(
    filename="example_file.md",
    url="http://example.com/example_file.md",
    must_include=["Expected String 1", "Expected String 2"],
    must_not_include=["Unexpected String 1", "Unexpected String 2"]
)

test_convert_http_uri(test_vector)
```

---
## `test_convert_file_uri`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:127`](/packages/markitdown/tests/test_module_vectors.py#L127-L140)

**Dependencies:** `MarkItDown`, `Path`, `as_uri`, `convert`, `join`, `test_convert_file_uri`  


# Function Documentation: test_convert_file_uri

## Description
The `test_convert_file_uri` function tests the conversion of a file URI to Markdown format using the `MarkItDown` class. It verifies that specific strings are included or excluded in the resulting Markdown output based on the provided test vector.

## Parameters
- `test_vector` (Type: `object`): An object that contains the following attributes:
  - `filename` (Type: `str`): The name of the file used to construct the file URI.
  - `url` (Type: `str`): A URL that is passed to the `convert` method of the `MarkItDown` instance.
  - `must_include` (Type: `list` of `str`): A list of strings that must be present in the resulting Markdown output.
  - `must_not_include` (Type: `list` of `str`): A list of strings that must not be present in the resulting Markdown output.

## Return Value
The function does not return a value. It performs assertions to validate the contents of the `result.markdown`. If any assertion fails, an `AssertionError` is raised.

## Dependencies
- `os`: Used to join the `TEST_FILES_DIR` and `test_vector.filename` to create a file path.
- `Path` from the `pathlib` module: Used to convert the file path to a URI.
- `MarkItDown`: A class that must be defined elsewhere in the codebase, which provides the `convert` method for converting file URIs to Markdown.

## Usage Example
```python
# Assuming test_vector is defined with appropriate attributes
test_vector = {
    'filename': 'example.txt',
    'url': 'http://example.com',
    'must_include': ['Expected string 1', 'Expected string 2'],
    'must_not_include': ['Unexpected string 1']
}

test_convert_file_uri(test_vector)
```

---
## `test_convert_data_uri`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:142`](/packages/markitdown/tests/test_module_vectors.py#L142-L161)

**Dependencies:** `MarkItDown`, `b64encode`, `convert`, `decode`, `join`, `open`, `read`, `test_convert_data_uri`  


# Function Documentation: test_convert_data_uri

## Description
The `test_convert_data_uri` function tests the conversion of a data URI into Markdown format using the `MarkItDown` class. It reads a file specified by the `test_vector`, encodes its contents in base64, constructs a data URI, and verifies that the resulting Markdown output contains or does not contain specified strings.

## Parameters

- **test_vector** (`TestVector`): An object that contains the following attributes:
  - **filename** (`str`): The name of the file to be read for conversion. This file is expected to be located in the directory specified by `TEST_FILES_DIR`.
  - **mimetype** (`str`): The MIME type associated with the file being converted. This is used to construct the data URI.
  - **url** (`str`): A URL that may be passed to the `convert` method of the `MarkItDown` instance.
  - **must_include** (`list` of `str`): A list of strings that must be present in the resulting Markdown output.
  - **must_not_include** (`list` of `str`): A list of strings that must not be present in the resulting Markdown output.

## Return Value
The function does not return a value. It performs assertions to validate the contents of the Markdown output against the specified `must_include` and `must_not_include` lists.

## Dependencies
The function relies on the following external modules and classes:
- `os`: Used to construct the file path for the test file.
- `base64`: Used to encode the file contents in base64 format.
- `MarkItDown`: A class that is instantiated to perform the conversion of the data URI to Markdown format.

## Usage Example
```python
test_vector = TestVector(
    filename="example.txt",
    mimetype="text/plain",
    url="http://example.com",
    must_include=["expected string"],
    must_not_include=["unexpected string"]
)
test_convert_data_uri(test_vector)
```

---
## `test_convert_keep_data_uris`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:163`](/packages/markitdown/tests/test_module_vectors.py#L163-L179)

**Dependencies:** `MarkItDown`, `convert`, `join`, `test_convert_keep_data_uris`  


# Function Documentation: test_convert_keep_data_uris

## Description
The `test_convert_keep_data_uris` function tests the functionality of the `MarkItDown` API when the `keep_data_uris` option is enabled. It verifies that the conversion of a local file to Markdown format includes or excludes specific strings as defined in the `test_vector`.

## Parameters

- `test_vector` (Type: `object`):
  - This parameter is expected to have the following attributes:
    - `filename` (Type: `str`): The name of the file to be converted, which is used to construct the file path.
    - `url` (Type: `str`): A URL that may be used in the conversion process.
    - `must_include` (Type: `list` of `str`): A list of strings that must be present in the resulting Markdown output.
    - `must_not_include` (Type: `list` of `str`): A list of strings that must not be present in the resulting Markdown output.

## Return Value
The function does not return a value. It performs assertions to validate the contents of the `result.markdown` output against the specified `must_include` and `must_not_include` strings.

## Dependencies
- `os`: The function uses the `os.path.join` method to construct the file path for the local file conversion.
- `MarkItDown`: The function instantiates an object of the `MarkItDown` class to perform the conversion.
- `TEST_FILES_DIR`: This variable is expected to be defined in the scope where the function is called, representing the directory containing test files.

## Usage Example
```python
# Assuming test_vector is defined with the required attributes
test_convert_keep_data_uris(test_vector)
```

---
## `test_convert_stream_keep_data_uris`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:181`](/packages/markitdown/tests/test_module_vectors.py#L181-L201)

**Dependencies:** `MarkItDown`, `StreamInfo`, `convert`, `join`, `open`, `splitext`, `test_convert_stream_keep_data_uris`  


# Function Documentation: test_convert_stream_keep_data_uris

## Description
The `test_convert_stream_keep_data_uris` function tests the conversion of a stream using the `MarkItDown` class. It specifically verifies that the conversion process retains data URIs when the `keep_data_uris` flag is set to `True`. The function checks that certain strings are included in the resulting markdown output and that others are not.

## Parameters
- `test_vector` (Type: `object`): An object that contains the following attributes:
  - `filename` (Type: `str`): The name of the file to be opened and converted.
  - `mimetype` (Type: `str`): The MIME type associated with the file.
  - `charset` (Type: `str`): The character set of the file.
  - `url` (Type: `str`): A URL that may be used in the conversion process.
  - `must_include` (Type: `list` of `str`): A list of strings that must be present in the resulting markdown.
  - `must_not_include` (Type: `list` of `str`): A list of strings that must not be present in the resulting markdown.

## Return Value
The function does not return a value. It performs assertions to validate the content of the `result.markdown` output against the `must_include` and `must_not_include` lists.

## Dependencies
- `os`: Used to manipulate file paths.
- `MarkItDown`: A class that is instantiated to perform the conversion.
- `StreamInfo`: A class used to encapsulate stream information, including file extension, MIME type, and character set.
- `TEST_FILES_DIR`: A constant that should define the directory where test files are located.

## Usage Example
```python
test_vector = {
    'filename': 'example_file.md',
    'mimetype': 'text/markdown',
    'charset': 'utf-8',
    'url': 'http://example.com',
    'must_include': ['Expected string 1', 'Expected string 2'],
    'must_not_include': ['Unexpected string 1', 'Unexpected string 2']
}

test_convert_stream_keep_data_uris(test_vector)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
