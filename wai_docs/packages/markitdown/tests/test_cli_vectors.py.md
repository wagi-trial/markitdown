# packages/markitdown/tests/test_cli_vectors.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/tests/test_cli_vectors.py",
  "file_hash": "e74a9369c0527b9c2fc520d5b900f05e84a00127ff67a5d4c6e7482def954a44",
  "last_updated": "2025-12-23T15:54:15.276951+00:00",
  "functions": {
    "shared_tmp_dir": {
      "hash": "d786a5fd205703259976c891c23e47e1bcf665823549ab20b4477ef543f94b74",
      "lines": "39-42",
      "last_updated": "2025-12-23T15:53:55.116922+00:00"
    },
    "test_output_to_stdout": {
      "hash": "29452e9a401d835c0def33b01033af6d6b556732306a3a815c21d7102964c7e2",
      "lines": "44-64",
      "last_updated": "2025-12-23T15:53:59.240398+00:00"
    },
    "test_output_to_file": {
      "hash": "57989101ecdfaa69c304ea964030a99e369cdd50c0db2dff8ddf5a2e677fefa1",
      "lines": "66-96",
      "last_updated": "2025-12-23T15:54:02.821909+00:00"
    },
    "test_input_from_stdin_without_hints": {
      "hash": "59d48aedda7c9cf4d20d08ff75896eb86977a1d62419fe07d3b8a1f581881220",
      "lines": "98-126",
      "last_updated": "2025-12-23T15:54:07.219766+00:00"
    },
    "test_convert_url": {
      "hash": "be6c33b8037ddc012ca765c9ff09ed3100669b06ad54e1e86a7962cd98905ced",
      "lines": "132-150",
      "last_updated": "2025-12-23T15:54:10.814098+00:00"
    },
    "test_output_to_file_with_data_uris": {
      "hash": "583286e9dee29e1275a0035adbfe1cbe50b1119c2d07df56f9fd8caf028aac36",
      "lines": "152-183",
      "last_updated": "2025-12-23T15:54:15.276869+00:00"
    }
  }
}
```

</details>



The Python file `test_cli_vectors.py` implements a series of tests for the command-line interface (CLI) of the `markitdown` package. It utilizes the `pytest` framework to validate the functionality of the CLI by executing various commands and checking their outputs against expected results. The tests focus on verifying the correctness of output to standard output, output to files, input from standard input, and the handling of URLs and data URIs.

The main functions defined in this file include:
- `shared_tmp_dir`: A fixture that creates a temporary directory for use in tests.
- `test_output_to_stdout`: Tests that the CLI outputs the correct content to standard output based on provided test vectors.
- `test_output_to_file`: Tests that the CLI writes the correct content to a specified output file.
- `test_input_from_stdin_without_hints`: Tests that the CLI reads input from standard input correctly and produces the expected output.
- `test_convert_url`: Tests the CLI's ability to handle URL inputs, with a condition to skip these tests in CI environments.
- `test_output_to_file_with_data_uris`: Tests the CLI's functionality when the `--keep-data-uris` option is enabled, ensuring that the output file contains the expected content.

The file imports several modules, including `os`, `time`, `pytest`, `subprocess`, and `locale`. It also imports specific test vectors and data structures from a module named `_test_vectors`, which includes `GENERAL_TEST_VECTORS`, `DATA_URI_TEST_VECTORS`, and `FileTestVector`. The code manipulates lists of `FileTestVector` instances, which contain attributes for filenames and expected output strings. The tests utilize subprocess calls to execute the CLI commands and capture their outputs for validation against the expected results defined in the test vectors.

## Functions and Classes

## `shared_tmp_dir`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:39`](/packages/markitdown/tests/test_cli_vectors.py#L39-L42)

# Function Documentation: `shared_tmp_dir`

## Description
The `shared_tmp_dir` function creates a temporary directory with a specified prefix using the `tmp_path_factory` object. The directory is named "pytest_tmp" and is created in the context of the pytest framework.

## Parameters
- `tmp_path_factory` (Type: `pytest.TempPathFactory`): 
  - This parameter is an instance of `TempPathFactory` provided by the pytest framework.
  - It is used to create temporary directories and files during testing.
  
## Return Value
- Returns a `pathlib.Path` object that represents the path to the newly created temporary directory.
- The directory is prefixed with "pytest_tmp".

## Dependencies
- The function explicitly depends on the `pytest` framework, specifically the `TempPathFactory` class, which is part of the pytest testing utilities.

## Usage Example
```python
def test_example(tmp_path_factory):
    temp_dir = shared_tmp_dir(tmp_path_factory)
    assert temp_dir.is_dir()  # This checks that the directory was created successfully.
```

---
## `test_output_to_stdout`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:44`](/packages/markitdown/tests/test_cli_vectors.py#L44-L64)

# Function Documentation: `test_output_to_stdout`

## Description
The `test_output_to_stdout` function tests the output of a command-line interface (CLI) tool called `markitdown`. It executes the tool with a specified test file and verifies that the output to standard output (stdout) contains certain expected strings while not containing others.

## Parameters

### `shared_tmp_dir`
- **Type**: `Any`
- **Constraints**: This parameter is not used within the function body.
- **Usage**: It is included in the function signature, likely for compatibility with a testing framework that provides a temporary directory for tests.

### `test_vector`
- **Type**: An object with attributes `filename`, `must_include`, and `must_not_include`.
- **Constraints**: 
  - `filename`: A string representing the name of the test file to be processed by the CLI.
  - `must_include`: A list of strings that must be present in the CLI output.
  - `must_not_include`: A list of strings that must not be present in the CLI output.
- **Usage**: The `filename` is used to construct the path to the test file, while `must_include` and `must_not_include` are used to validate the output of the CLI.

## Return Value
- **Type**: `None`
- **Content**: The function does not return any value. It raises an assertion error if the CLI command fails or if the output does not meet the specified conditions.

## Dependencies
- **Modules**:
  - `subprocess`: Used to run the CLI command and capture its output.
  - `os`: Used to construct the file path for the test file.
  
## Usage Example
```python
class TestVector:
    filename = "example.md"
    must_include = ["Expected output string"]
    must_not_include = ["Unexpected output string"]

test_output_to_stdout(shared_tmp_dir, TestVector())
``` 

In this example, `TestVector` is a class that simulates the structure expected for the `test_vector` parameter. The function is called with a temporary directory and an instance of `TestVector`.

---
## `test_output_to_file`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:66`](/packages/markitdown/tests/test_cli_vectors.py#L66-L96)

# Function Documentation: `test_output_to_file`

## Description
The `test_output_to_file` function tests the output of a command-line interface (CLI) tool by verifying that it correctly writes output to a specified file. The function executes the CLI tool with a specified input file and checks the resulting output file for expected content.

## Parameters

- `shared_tmp_dir` (str): 
  - A directory path where temporary files can be created. This directory is used to construct the path for the output file.
  
- `test_vector` (object): 
  - An object that contains the following attributes:
    - `filename` (str): The name of the input file (without extension) that will be processed by the CLI tool.
    - `must_include` (list of str): A list of strings that must be present in the output file.
    - `must_not_include` (list of str): A list of strings that must not be present in the output file.

## Return Value
The function does not return any value. Its return type is `None`.

## Dependencies
The function relies on the following external modules:
- `os`: Used for file path manipulation and checking file existence.
- `subprocess`: Used to execute the CLI command and capture its output.

## Usage Example
```python
class TestVector:
    filename = "example_input"
    must_include = ["expected string 1", "expected string 2"]
    must_not_include = ["unexpected string 1", "unexpected string 2"]

shared_tmp_dir = "/path/to/temp/dir"
test_vector = TestVector()

test_output_to_file(shared_tmp_dir, test_vector)
``` 

In this example, the function `test_output_to_file` is invoked with a temporary directory and a `TestVector` instance that specifies the input filename and the strings to check for in the output.

---
## `test_input_from_stdin_without_hints`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:98`](/packages/markitdown/tests/test_cli_vectors.py#L98-L126)

# Function Documentation: `test_input_from_stdin_without_hints`

## Description
The `test_input_from_stdin_without_hints` function tests the command-line interface (CLI) of the `markitdown` module to ensure it correctly reads input from standard input (stdin). It reads a binary input file, executes the CLI with that input, and verifies the output against expected strings.

## Parameters

- `shared_tmp_dir`: 
  - Type: `Any`
  - Constraints: None specified in the code.
  - Usage: This parameter is not explicitly used within the function but may be part of the testing framework's context.

- `test_vector`: 
  - Type: `Any`
  - Constraints: Must have attributes `filename`, `must_include`, and `must_not_include`.
  - Usage: 
    - `test_vector.filename` is used to construct the path to the input file.
    - `test_vector.must_include` is a list of strings that must be present in the CLI output.
    - `test_vector.must_not_include` is a list of strings that must not be present in the CLI output.

## Return Value
- Type: `None`
- The function does not return any value. It raises assertions if the CLI execution does not meet the expected conditions.

## External Dependencies
- `os`: Used to construct file paths.
- `subprocess`: Used to execute the CLI command.
- `locale`: Used to get the preferred encoding for decoding the output.
- `TEST_FILES_DIR`: A constant that must be defined elsewhere in the code, representing the directory containing test files.

## Usage Example
```python
test_input_from_stdin_without_hints(shared_tmp_dir, test_vector)
```
In this example, `shared_tmp_dir` is provided as a temporary directory for testing, and `test_vector` is an object containing the necessary attributes for the test.

---
## `test_convert_url`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:132`](/packages/markitdown/tests/test_cli_vectors.py#L132-L150)

# Function Documentation: test_convert_url

## Description
The `test_convert_url` function tests the conversion of a stream using a specified test vector. It executes a command-line interface (CLI) command to convert a file and verifies the output against expected strings.

## Parameters
- `shared_tmp_dir` (Type: `str`): This parameter is not used within the function but is included to match the function signature. It is expected to be a temporary directory path.
  
- `test_vector` (Type: `object`): This parameter is expected to have the following attributes:
  - `filename` (Type: `str`): Represents the name of the file to be processed.
  - `must_include` (Type: `list` of `str`): A list of strings that must be present in the output of the CLI command.
  - `must_not_include` (Type: `list` of `str`): A list of strings that must not be present in the output of the CLI command.

## Return Value
The function does not return a value. Instead, it asserts conditions based on the output of the CLI command. If any assertion fails, an `AssertionError` is raised with a message indicating the failure.

## Dependencies
- `subprocess`: Used to run the CLI command.
- `time`: Used to introduce a delay to avoid hitting rate limits.
- `locale`: Used to get the preferred encoding for decoding the output of the CLI command.

## Usage Example
```python
class TestVector:
    def __init__(self, filename, must_include, must_not_include):
        self.filename = filename
        self.must_include = must_include
        self.must_not_include = must_not_include

test_vector = TestVector(
    filename='example.md',
    must_include=['Expected String 1', 'Expected String 2'],
    must_not_include=['Unexpected String 1']
)

test_convert_url('/path/to/shared/tmp/dir', test_vector)
```

---
## `test_output_to_file_with_data_uris`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:152`](/packages/markitdown/tests/test_cli_vectors.py#L152-L183)

# Function Documentation: `test_output_to_file_with_data_uris`

## Description
The `test_output_to_file_with_data_uris` function tests the command-line interface (CLI) functionality of the `markitdown` module when the `--keep-data-uris` option is enabled. It verifies that the output file is created correctly and contains the expected data while ensuring that certain unwanted strings are not present.

## Parameters
- `shared_tmp_dir` (type: `str`): A temporary directory shared among tests where the output file will be created. This parameter is used to construct the path for the output file.
  
- `test_vector` (type: `object`): An object that contains at least two attributes:
  - `filename` (type: `str`): The name of the input file (without extension) to be processed by the `markitdown` module.
  - `must_include` (type: `list` of `str`): A list of strings that must be present in the output data.
  - `must_not_include` (type: `list` of `str`): A list of strings that must not be present in the output data.

## Return Value
The function does not return any value. Its return type is `None`.

## Dependencies
The function relies on the following external modules:
- `os`: Used for file path manipulation and checking file existence.
- `subprocess`: Used to run the `markitdown` CLI command and capture its output.

## Usage Example
```python
# Example invocation of the function
test_output_to_file_with_data_uris(shared_tmp_dir="/tmp", test_vector=test_vector_instance)
```
In this example, `shared_tmp_dir` is set to `"/tmp"` and `test_vector_instance` is an instance of a class or structure that contains the necessary attributes (`filename`, `must_include`, and `must_not_include`).

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
