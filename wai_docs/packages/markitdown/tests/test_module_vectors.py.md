# packages/markitdown/tests/test_module_vectors.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/tests/test_module_vectors.py",
  "file_hash": "5beede9a668820885154cec341d94f0fc4705c81208e8acf92b61200a4cc9eec",
  "last_updated": "2025-12-23T15:58:45.638104+00:00",
  "functions": {
    "test_guess_stream_info": {
      "hash": "4e6b2c735a6029b983be5b66c117ffccee858c67b853fafa5763fb6bd0d7d713",
      "lines": "28-56",
      "last_updated": "2025-12-23T15:58:11.104957+00:00"
    },
    "test_convert_local": {
      "hash": "0bcbe41497cef57ff96b53aa48847959fab2360481558338518f8c67a93ffc71",
      "lines": "58-70",
      "last_updated": "2025-12-23T15:58:14.435061+00:00"
    },
    "test_convert_stream_with_hints": {
      "hash": "f0c7b15dfa5f2b0950169299acc1c26f61af65349a578278b509e60625575dad",
      "lines": "72-91",
      "last_updated": "2025-12-23T15:58:18.465626+00:00"
    },
    "test_convert_stream_without_hints": {
      "hash": "8c4c8c153be8a1afcc64445196fc8e130fe73cc570aac7b52ad530db8bb4dab8",
      "lines": "93-104",
      "last_updated": "2025-12-23T15:58:23.218989+00:00"
    },
    "test_convert_http_uri": {
      "hash": "e44bd03c63e486861c48192532f9a7774d6ec993a1bee417ada85c099d3668ab",
      "lines": "110-125",
      "last_updated": "2025-12-23T15:58:27.712971+00:00"
    },
    "test_convert_file_uri": {
      "hash": "c79c87dd87cf00be195fcb677aa80b3cb2ce1965f072d8c9361de08c8fd97e9b",
      "lines": "127-140",
      "last_updated": "2025-12-23T15:58:31.485499+00:00"
    },
    "test_convert_data_uri": {
      "hash": "7a567dc3b5cba17d2c5fe2d81043b000412e349259ac10181dd9353e3ca77b5e",
      "lines": "142-161",
      "last_updated": "2025-12-23T15:58:36.144621+00:00"
    },
    "test_convert_keep_data_uris": {
      "hash": "7e5f9b60a3e356e4979499e909826ac827c97f727853416ceba314e7e7a02523",
      "lines": "163-179",
      "last_updated": "2025-12-23T15:58:41.662156+00:00"
    },
    "test_convert_stream_keep_data_uris": {
      "hash": "13cf6aa6bff05461c685e48d2e98eecf08c9ff1073fc3a7aae49d66c98052afd",
      "lines": "181-201",
      "last_updated": "2025-12-23T15:58:45.638006+00:00"
    }
  }
}
```

</details>



The Python file `test_module_vectors.py` implements a suite of unit tests for the `MarkItDown` class from the `markitdown` package. The tests focus on verifying the functionality of converting various input types into Markdown format, including local files, streams, HTTP/HTTPS URIs, file URIs, and data URIs. The tests utilize parameterized inputs defined in `GENERAL_TEST_VECTORS` and `DATA_URI_TEST_VECTORS`, which provide a structured way to validate the conversion process against expected outcomes.

The main functions defined in this file include:
- `test_guess_stream_info`: Tests the ability to infer stream information from a file.
- `test_convert_local`: Tests the conversion of a local file to Markdown.
- `test_convert_stream_with_hints`: Tests conversion when stream information is provided.
- `test_convert_stream_without_hints`: Tests conversion with no stream information.
- `test_convert_http_uri`: Tests conversion from an HTTP/HTTPS URI, with a skip condition for CI environments.
- `test_convert_file_uri`: Tests conversion from a file URI.
- `test_convert_data_uri`: Tests conversion from a data URI.
- `test_convert_keep_data_uris`: Tests conversion with the `keep_data_uris` option enabled for local files.
- `test_convert_stream_keep_data_uris`: Tests conversion with the `keep_data_uris` option enabled for streams.

The file imports several modules, including `os`, `time`, `pytest`, and `base64`, as well as `Path` from `pathlib`. It also imports `MarkItDown` and `StreamInfo` from the `markitdown` package. The tests manipulate instances of `StreamInfo` to provide metadata about the files being tested. The test vectors contain attributes such as `filename`, `mimetype`, `charset`, `must_include`, and `must_not_include`, which are used to validate the correctness of the conversion results. The tests assert that the output Markdown includes or excludes specific strings based on the provided test vectors.

## Functions and Classes

## `test_guess_stream_info`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:28`](/packages/markitdown/tests/test_module_vectors.py#L28-L56)

# Function Documentation: `test_guess_stream_info`

## Description
The `test_guess_stream_info` function tests the ability of the `MarkItDown` class to guess stream information based on a provided test vector. It reads a file from a specified local path, generates guesses for its stream information, and asserts that the first guess matches the expected mimetype, extension, and charset defined in the test vector.

## Parameters
- `test_vector` (Type: `object`)
  - Constraints: Must have attributes `filename`, `mimetype`, and `charset`.
  - Usage: Represents the test case containing the filename to be tested, the expected mimetype, and the expected charset.

## Return Value
- Type: `None`
- The function does not return a value. It raises an assertion error if the guessed stream information does not match the expected values for the provided test vector, except for specific cases where it is designed to return early without assertions.

## Dependencies
- `os`: Used to construct the local file path.
- `MarkItDown`: A class that is instantiated to create an object used for guessing stream information.
- `StreamInfo`: A class used to create a base guess for the stream information.

## Usage Example
```python
# Assuming test_vector is an object with the required attributes
test_vector = SomeTestVectorClass(filename="example_file.txt", mimetype="text/plain", charset="utf-8")
test_guess_stream_info(test_vector)
```

---
## `test_convert_local`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:58`](/packages/markitdown/tests/test_module_vectors.py#L58-L70)

# Function Documentation: `test_convert_local`

## Description
The `test_convert_local` function tests the conversion of a local file using the `MarkItDown` class. It verifies that the conversion result contains specific strings and does not contain others, based on the provided `test_vector`.

## Parameters

- `test_vector` (Type: `TestVector`)
  - Constraints: Must be an instance of the `TestVector` class.
  - Usage: The `test_vector` is used to access the `filename`, `url`, `must_include`, and `must_not_include` attributes. The `filename` is used to construct the path to the local file, and the `url` is passed as an argument to the `convert` method of the `MarkItDown` instance. The `must_include` and `must_not_include` attributes are lists of strings that are checked against the conversion result.

## Return Value
The function does not return a value. It performs assertions to validate the contents of the `result.markdown`. If any assertion fails, an `AssertionError` is raised.

## Dependencies
- `os`: The `os.path.join` function is used to construct the file path.
- `MarkItDown`: An instance of this class is created to perform the conversion.
- `TEST_FILES_DIR`: A variable that should be defined elsewhere in the code, representing the directory where test files are located.

## Usage Example
```python
# Assuming TestVector is defined and TEST_FILES_DIR is set
test_vector = TestVector(filename='example.md', url='http://example.com', 
                         must_include=['Expected String'], 
                         must_not_include=['Unexpected String'])
test_convert_local(test_vector)
```

---
## `test_convert_stream_with_hints`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:72`](/packages/markitdown/tests/test_module_vectors.py#L72-L91)

# Function Documentation: test_convert_stream_with_hints

## Description
The `test_convert_stream_with_hints` function tests the conversion of a stream into Markdown format using the `MarkItDown` class. It verifies that the resulting Markdown output contains specific strings and does not contain others, based on the provided `test_vector`.

## Parameters

- **test_vector** (`TestVector`): An object that contains the following attributes:
  - `filename` (`str`): The name of the file to be opened for reading as a binary stream.
  - `mimetype` (`str`): The MIME type of the file, used in the `StreamInfo` object.
  - `charset` (`str`): The character set of the file, used in the `StreamInfo` object.
  - `url` (`str`): A URL associated with the file, passed to the `convert` method.
  - `must_include` (`list[str]`): A list of strings that must be present in the resulting Markdown output.
  - `must_not_include` (`list[str]`): A list of strings that must not be present in the resulting Markdown output.

## Return Value
The function does not return a value. It performs assertions to validate the contents of the Markdown output against the expected strings.

## Dependencies
- **os**: The function uses `os.path.splitext` to extract the file extension from the filename.
- **MarkItDown**: The function creates an instance of `MarkItDown` to perform the conversion.
- **StreamInfo**: The function creates an instance of `StreamInfo` to encapsulate stream metadata.
- **TEST_FILES_DIR**: A constant that specifies the directory where test files are located.

## Usage Example
```python
test_vector = TestVector(
    filename='example.txt',
    mimetype='text/plain',
    charset='utf-8',
    url='http://example.com',
    must_include=['Expected string 1', 'Expected string 2'],
    must_not_include=['Unexpected string 1', 'Unexpected string 2']
)

test_convert_stream_with_hints(test_vector)
```

---
## `test_convert_stream_without_hints`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:93`](/packages/markitdown/tests/test_module_vectors.py#L93-L104)

# Documentation for `test_convert_stream_without_hints`

## Function Overview
`test_convert_stream_without_hints` is a test function designed to validate the conversion of a stream of data into markdown format without any additional stream information. It utilizes the `MarkItDown` class to perform the conversion and checks the output against expected content.

## Parameters
- `test_vector` (Type: `object`):
  - This parameter is expected to be an object that contains:
    - `filename` (Type: `str`): The name of the file to be opened and converted. This should be a valid filename that exists in the directory specified by `TEST_FILES_DIR`.
    - `url` (Type: `str`): A URL that may be used in the conversion process, passed as an argument to the `convert` method.
    - `must_include` (Type: `list` of `str`): A list of strings that must be present in the resulting markdown output.
    - `must_not_include` (Type: `list` of `str`): A list of strings that must not be present in the resulting markdown output.

## Return Value
The function does not return a value. Instead, it asserts conditions based on the output of the conversion. If any assertion fails, an `AssertionError` will be raised.

## Dependencies
- `MarkItDown`: This class is instantiated within the function and is responsible for converting the input stream to markdown format.
- `os`: This module is used to construct the file path for the input stream.
- `TEST_FILES_DIR`: This variable is expected to be defined in the scope where this function is executed. It should contain the directory path where test files are located.

## Usage Example
```python
# Assuming test_vector is defined with appropriate attributes
test_vector = {
    'filename': 'example_file.md',
    'url': 'http://example.com',
    'must_include': ['Expected string 1', 'Expected string 2'],
    'must_not_include': ['Unexpected string 1', 'Unexpected string 2']
}

test_convert_stream_without_hints(test_vector)
``` 

In this example, the `test_vector` object is constructed with a filename, a URL, and lists of strings that are expected to be included or excluded from the markdown output. The function is then invoked with this `test_vector`.

---
## `test_convert_http_uri`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:110`](/packages/markitdown/tests/test_module_vectors.py#L110-L125)

# Function Documentation: test_convert_http_uri

## Description
The `test_convert_http_uri` function tests the conversion of an HTTP or HTTPS URI using the `MarkItDown` class. It performs the following steps:
1. Instantiates a `MarkItDown` object.
2. Pauses execution for 1 second to avoid hitting rate limits.
3. Calls the `convert` method of the `MarkItDown` instance with a constructed URL and a mock URL for the test vector.
4. Asserts that certain strings are included in the resulting markdown output and that other strings are not included.

## Parameters
- `test_vector` (Type: `object`)
  - Constraints: Must have attributes `filename`, `url`, `must_include`, and `must_not_include`.
  - Usage: 
    - `test_vector.filename` is used to construct the URL for the `convert` method.
    - `test_vector.url` is passed as a mock URL to the `convert` method.
    - `test_vector.must_include` is an iterable containing strings that must be present in the resulting markdown.
    - `test_vector.must_not_include` is an iterable containing strings that must not be present in the resulting markdown.

## Return Value
The function does not return a value. It performs assertions to validate the contents of the markdown output generated by the `convert` method.

## Dependencies
- `MarkItDown`: This class must be defined in the codebase and is used to perform the conversion of the URI.
- `time`: The `sleep` function from this module is used to introduce a delay.
- `TEST_FILES_URL`: This variable must be defined in the codebase and is used to construct the URL for the `convert` method.

## Usage Example
```python
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

test_convert_http_uri(test_vector)
```

---
## `test_convert_file_uri`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:127`](/packages/markitdown/tests/test_module_vectors.py#L127-L140)

# Function Documentation: test_convert_file_uri

## Description
The `test_convert_file_uri` function tests the conversion of a file URI to Markdown format using the `MarkItDown` class. It verifies that certain expected strings are included in the resulting Markdown output and that certain other strings are not included.

## Parameters
- `test_vector` (type: `TestVector`): An object that contains the following attributes:
  - `filename` (type: `str`): The name of the file used to create the file URI.
  - `url` (type: `str`): A URL associated with the test vector.
  - `must_include` (type: `list` of `str`): A list of strings that must be present in the resulting Markdown output.
  - `must_not_include` (type: `list` of `str`): A list of strings that must not be present in the resulting Markdown output.

## Return Value
The function does not return a value. It performs assertions to validate the contents of the `result.markdown` against the `must_include` and `must_not_include` attributes of the `test_vector`.

## Dependencies
- `os`: Used to construct the file path for the test file.
- `Path` from `pathlib`: Used to create a URI from the file path.
- `MarkItDown`: A class that provides the `convert` method for converting a file URI to Markdown format.
- `TEST_FILES_DIR`: A constant that specifies the directory where test files are located.

## Usage Example
```python
test_vector = TestVector(
    filename='example.md',
    url='http://example.com',
    must_include=['Expected String 1', 'Expected String 2'],
    must_not_include=['Unexpected String']
)

test_convert_file_uri(test_vector)
```

---
## `test_convert_data_uri`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:142`](/packages/markitdown/tests/test_module_vectors.py#L142-L161)

# Function Documentation: test_convert_data_uri

## Description
The `test_convert_data_uri` function tests the conversion of a data URI into markdown format using the `MarkItDown` class. It reads a file specified by the `test_vector`, encodes its content in base64, and constructs a data URI. The function then verifies that certain strings are included or excluded in the resulting markdown output.

## Parameters
- `test_vector`: An object that contains the following attributes:
  - `filename` (str): The name of the file to be read for conversion. This file is expected to be located in the directory specified by `TEST_FILES_DIR`.
  - `mimetype` (str): The MIME type associated with the file being converted. This is used to construct the data URI.
  - `url` (str): A URL that may be passed to the `convert` method of the `MarkItDown` instance.
  - `must_include` (list of str): A list of strings that must be present in the resulting markdown output.
  - `must_not_include` (list of str): A list of strings that must not be present in the resulting markdown output.

## Return Value
The function does not return a value. Instead, it asserts conditions based on the presence or absence of specified strings in the markdown output generated by the `MarkItDown.convert` method.

## Dependencies
The function relies on the following external modules:
- `os`: Used for file path manipulation.
- `base64`: Used for encoding the file content in base64 format.
- `MarkItDown`: A class that is expected to have a method named `convert`, which takes a data URI and an optional URL parameter.

## Usage Example
```python
test_vector = {
    'filename': 'example.txt',
    'mimetype': 'text/plain',
    'url': 'http://example.com',
    'must_include': ['expected string 1', 'expected string 2'],
    'must_not_include': ['unexpected string 1', 'unexpected string 2']
}
test_convert_data_uri(test_vector)
``` 

In this example, `test_vector` is a dictionary that simulates the expected structure of the `test_vector` parameter, which is passed to the `test_convert_data_uri` function for testing.

---
## `test_convert_keep_data_uris`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:163`](/packages/markitdown/tests/test_module_vectors.py#L163-L179)

# Function Documentation: test_convert_keep_data_uris

## Description
The `test_convert_keep_data_uris` function tests the functionality of the `convert` method from the `MarkItDown` class when the `keep_data_uris` parameter is set to `True`. It verifies that the output markdown contains specific strings and does not contain others, based on the provided `test_vector`.

## Parameters

- **test_vector** (Type: `object`)
  - Constraints: Must have attributes `filename`, `url`, `must_include`, and `must_not_include`.
  - Usage: 
    - `filename`: Used to construct the path to the test file by joining it with `TEST_FILES_DIR`.
    - `url`: Passed as an argument to the `convert` method.
    - `must_include`: A list of strings that must be present in the result's markdown output.
    - `must_not_include`: A list of strings that must not be present in the result's markdown output.

## Return Value
The function does not return a value. Instead, it performs assertions to validate the contents of the `result.markdown`. If any assertion fails, an `AssertionError` will be raised.

## Dependencies
- `os`: Used to join the `TEST_FILES_DIR` with the `test_vector.filename`.
- `MarkItDown`: A class that contains the `convert` method being tested.
- `TEST_FILES_DIR`: A global variable that should be defined elsewhere in the codebase, representing the directory containing test files.

## Usage Example
```python
test_vector = {
    'filename': 'example_file.md',
    'url': 'http://example.com',
    'must_include': ['Expected string 1', 'Expected string 2'],
    'must_not_include': ['Unexpected string 1', 'Unexpected string 2']
}

test_convert_keep_data_uris(test_vector)
``` 

Note: The `test_vector` in the usage example is represented as a dictionary for illustrative purposes. In the actual implementation, it should be an object with the specified attributes.

---
## `test_convert_stream_keep_data_uris`

**Location:** [`packages/markitdown/tests/test_module_vectors.py:181`](/packages/markitdown/tests/test_module_vectors.py#L181-L201)

# Function Documentation: test_convert_stream_keep_data_uris

## Description
The `test_convert_stream_keep_data_uris` function tests the conversion of a stream using the `MarkItDown` class. It checks that specific strings are included or excluded in the resulting markdown output based on the provided test vector.

## Parameters
- `test_vector`: An object that contains the following attributes:
  - `filename` (str): The name of the file to be opened for reading as a binary stream.
  - `mimetype` (str): The MIME type associated with the file.
  - `charset` (str): The character set used for the file.
  - `url` (str): A URL that may be used in the conversion process.
  - `must_include` (list of str): A list of strings that must be present in the resulting markdown.
  - `must_not_include` (list of str): A list of strings that must not be present in the resulting markdown.

## Return Value
The function does not return a value. It performs assertions to validate the content of the `result.markdown` against the `must_include` and `must_not_include` attributes of the `test_vector`.

## Dependencies
- `os`: The `os` module is used to manipulate file paths.
- `MarkItDown`: An instance of the `MarkItDown` class is created to perform the conversion.
- `StreamInfo`: An instance of the `StreamInfo` class is created to hold metadata about the stream.
- `TEST_FILES_DIR`: A constant that specifies the directory where test files are located.

## Usage Example
```python
test_vector = {
    'filename': 'example_file.md',
    'mimetype': 'text/markdown',
    'charset': 'utf-8',
    'url': 'http://example.com',
    'must_include': ['# Example Header', 'Some important content'],
    'must_not_include': ['This should not be present']
}

test_convert_stream_keep_data_uris(test_vector)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
