# packages/markitdown/tests/test_cli_vectors.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/tests/test_cli_vectors.py",
  "file_hash": "e74a9369c0527b9c2fc520d5b900f05e84a00127ff67a5d4c6e7482def954a44",
  "last_updated": "2026-01-04T17:24:01.189083+00:00",
  "functions": {
    "shared_tmp_dir": {
      "hash": "d786a5fd205703259976c891c23e47e1bcf665823549ab20b4477ef543f94b74",
      "lines": "39-42",
      "last_updated": "2026-01-04T17:23:42.784749+00:00"
    },
    "test_output_to_stdout": {
      "hash": "29452e9a401d835c0def33b01033af6d6b556732306a3a815c21d7102964c7e2",
      "lines": "44-64",
      "last_updated": "2026-01-04T17:23:46.215084+00:00"
    },
    "test_output_to_file": {
      "hash": "57989101ecdfaa69c304ea964030a99e369cdd50c0db2dff8ddf5a2e677fefa1",
      "lines": "66-96",
      "last_updated": "2026-01-04T17:23:49.948484+00:00"
    },
    "test_input_from_stdin_without_hints": {
      "hash": "59d48aedda7c9cf4d20d08ff75896eb86977a1d62419fe07d3b8a1f581881220",
      "lines": "98-126",
      "last_updated": "2026-01-04T17:23:53.872774+00:00"
    },
    "test_convert_url": {
      "hash": "be6c33b8037ddc012ca765c9ff09ed3100669b06ad54e1e86a7962cd98905ced",
      "lines": "132-150",
      "last_updated": "2026-01-04T17:23:57.890098+00:00"
    },
    "test_output_to_file_with_data_uris": {
      "hash": "583286e9dee29e1275a0035adbfe1cbe50b1119c2d07df56f9fd8caf028aac36",
      "lines": "152-183",
      "last_updated": "2026-01-04T17:24:01.189026+00:00"
    }
  }
}
```

</details>



The Python file `test_cli_vectors.py` implements a suite of tests for the command-line interface (CLI) of the `markitdown` package. It utilizes the `pytest` framework to run various tests that validate the output of the CLI when processing different input files. The tests check for correct output to standard output and files, as well as the handling of input from standard input. Additionally, it includes tests for converting URLs and managing data URIs.

The file defines several functions, each with specific responsibilities:
- `shared_tmp_dir`: A pytest fixture that creates a temporary directory for use during the tests.
- `test_output_to_stdout`: Tests that the CLI correctly outputs to standard output based on provided test vectors.
- `test_output_to_file`: Tests that the CLI correctly writes output to a specified file.
- `test_input_from_stdin_without_hints`: Tests that the CLI can read input from standard input correctly.
- `test_convert_url`: Tests the CLI's ability to convert input from a URL, with a condition to skip this test in CI environments.
- `test_output_to_file_with_data_uris`: Tests the CLI functionality when the `--keep-data-uris` option is enabled.

The code imports several modules, including `os`, `time`, `pytest`, `subprocess`, and `locale`, which are used for file operations, subprocess management, and testing functionalities. It also imports specific test vectors and data structures from a module named `_test_vectors`, which includes `GENERAL_TEST_VECTORS`, `DATA_URI_TEST_VECTORS`, and `FileTestVector`. The file manipulates lists of `FileTestVector` instances, which contain attributes such as `filename`, `must_include`, and `must_not_include`, used to validate the output of the CLI against expected results.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `shared_tmp_dir`

<details>
<summary><strong>Calls/Dependencies</strong> (2 unique functions)</summary>

- `mktemp`
- `shared_tmp_dir`

</details>

### `test_output_to_stdout`

<details>
<summary><strong>Calls/Dependencies</strong> (3 unique functions)</summary>

- `join`
- `run`
- `test_output_to_stdout`

</details>

### `test_output_to_file`

<details>
<summary><strong>Calls/Dependencies</strong> (7 unique functions)</summary>

- `exists`
- `join`
- `open`
- `read`
- `remove`
- `run`
- `test_output_to_file`

</details>

### `test_input_from_stdin_without_hints`

<details>
<summary><strong>Calls/Dependencies</strong> (7 unique functions)</summary>

- `decode`
- `getpreferredencoding`
- `join`
- `open`
- `read`
- `run`
- `test_input_from_stdin_without_hints`

</details>

### `test_convert_url`

<details>
<summary><strong>Calls/Dependencies</strong> (5 unique functions)</summary>

- `decode`
- `getpreferredencoding`
- `run`
- `sleep`
- `test_convert_url`

</details>

### `test_output_to_file_with_data_uris`

<details>
<summary><strong>Calls/Dependencies</strong> (7 unique functions)</summary>

- `exists`
- `join`
- `open`
- `read`
- `remove`
- `run`
- `test_output_to_file_with_data_uris`

</details>

</details>



## Functions and Classes

## `shared_tmp_dir`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:39`](/packages/markitdown/tests/test_cli_vectors.py#L39-L42)

**Dependencies:** `mktemp`, `shared_tmp_dir`  


# Function Documentation: `shared_tmp_dir`

## Description
The `shared_tmp_dir` function creates a temporary directory with a specific prefix using the provided `tmp_path_factory`. It utilizes the `mktemp` method of the `tmp_path_factory` to generate the directory.

## Parameters

### `tmp_path_factory`
- **Type**: `pytest.TempPathFactory`
- **Constraints**: Must be an instance of `pytest.TempPathFactory`, which is typically provided by the pytest framework during test execution.
- **Usage**: This parameter is used to call the `mktemp` method to create a temporary directory.

## Return Value
- **Type**: `pathlib.Path`
- **Content**: The function returns a `Path` object representing the path to the newly created temporary directory. The directory is prefixed with the string "pytest_tmp".

## Dependencies
- The function explicitly calls the `mktemp` method from the `pytest` framework's `TempPathFactory`. Therefore, it depends on the `pytest` module.

## Usage Example
```python
def test_example(tmp_path_factory):
    temp_dir = shared_tmp_dir(tmp_path_factory)
    assert temp_dir.is_dir()  # Verifies that the directory was created
```

---
## `test_output_to_stdout`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:44`](/packages/markitdown/tests/test_cli_vectors.py#L44-L64)

**Dependencies:** `join`, `run`, `test_output_to_stdout`  


# Function Documentation: `test_output_to_stdout`

## Description
The `test_output_to_stdout` function tests the output of a command-line interface (CLI) tool called `markitdown`. It verifies that the output sent to standard output (stdout) matches expected criteria based on the provided test vector.

## Parameters
- `shared_tmp_dir` (Type: `Any`): This parameter is not used within the function's implementation. It is likely intended for use in a broader testing context, possibly to provide a temporary directory for test files.
  
- `test_vector` (Type: `Any`): This parameter is expected to be an object that contains:
  - `filename` (Type: `str`): The name of the test file located in the `TEST_FILES_DIR`. This file is passed to the `markitdown` module for processing.
  - `must_include` (Type: `list[str]`): A list of strings that must be present in the CLI's stdout output.
  - `must_not_include` (Type: `list[str]`): A list of strings that must not be present in the CLI's stdout output.

## Return Value
The function does not return any value (Type: `None`). Instead, it raises an assertion error if the CLI command fails or if the output does not meet the specified criteria.

## Dependencies
- `subprocess`: This module is used to run the CLI command and capture its output.
- `os`: This module is used to construct the file path to the test file.
- `TEST_FILES_DIR`: A variable that must be defined elsewhere in the codebase, representing the directory where test files are stored.

## Usage Example
```python
test_output_to_stdout(shared_tmp_dir, test_vector)
```
In this example, `shared_tmp_dir` should be a temporary directory object, and `test_vector` should be an object with the required attributes (`filename`, `must_include`, and `must_not_include`).

---
## `test_output_to_file`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:66`](/packages/markitdown/tests/test_cli_vectors.py#L66-L96)

**Dependencies:** `exists`, `join`, `open`, `read`, `remove`, `run`, `test_output_to_file`  


# Function Documentation: `test_output_to_file`

## Description
The `test_output_to_file` function tests the output of a command-line interface (CLI) tool by executing it and verifying that the output is correctly written to a specified file. It checks the return code of the command, confirms the existence of the output file, and validates that the output contains certain expected strings while excluding others. Finally, it cleans up by deleting the output file.

## Parameters

- `shared_tmp_dir` (str): 
  - A string representing the path to a temporary directory shared among tests. 
  - This directory is used to store the output file generated by the CLI.

- `test_vector` (object): 
  - An object that contains at least two attributes:
    - `filename` (str): A string representing the name of the input file (without extension) to be processed by the CLI.
    - `must_include` (list of str): A list of strings that must be present in the output file.
    - `must_not_include` (list of str): A list of strings that must not be present in the output file.

## Return Value
The function returns `None`. It performs assertions to validate the output but does not return any data.

## Dependencies
The function relies on the following external modules:
- `os`: Used for file path manipulation and checking file existence.
- `subprocess`: Used to run the CLI command and capture its output.

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

In this example, `test_output_to_file` is called with a temporary directory path and a `TestVector` instance containing the necessary attributes for the test.

---
## `test_input_from_stdin_without_hints`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:98`](/packages/markitdown/tests/test_cli_vectors.py#L98-L126)

**Dependencies:** `decode`, `getpreferredencoding`, `join`, `open`, `read`, `run`, `test_input_from_stdin_without_hints`  


# Function Documentation: `test_input_from_stdin_without_hints`

## Description
The `test_input_from_stdin_without_hints` function tests the command-line interface (CLI) of the `markitdown` module to ensure it correctly reads input from standard input (stdin). The function reads a binary input file, executes the CLI with that input, and checks the output against expected strings.

## Parameters

- `shared_tmp_dir`: 
  - **Type**: `Any`
  - **Constraints**: This parameter is not explicitly used in the function implementation but may be part of the testing framework's setup.
  - **Usage**: It is likely intended for managing temporary directories for tests.

- `test_vector`: 
  - **Type**: `Any` (expected to have attributes `filename`, `must_include`, and `must_not_include`)
  - **Constraints**: The `test_vector` object must have:
    - `filename`: A string representing the name of the test file.
    - `must_include`: A list of strings that must be present in the output.
    - `must_not_include`: A list of strings that must not be present in the output.
  - **Usage**: The `filename` is used to locate the input file, while `must_include` and `must_not_include` are used for assertions on the output.

## Return Value
- **Type**: `None`
- **Content**: The function does not return a value. It performs assertions that will raise exceptions if the conditions are not met.

## Dependencies
- `os`: Used to construct file paths.
- `subprocess`: Used to run the CLI command.
- `locale`: Used to get the preferred encoding for decoding the output.
- `markitdown`: The module being tested, invoked as a subprocess.

## Usage Example
```python
test_input_from_stdin_without_hints(shared_tmp_dir, test_vector)
```
In this example, `shared_tmp_dir` should be provided by the testing framework, and `test_vector` should be an object containing the necessary attributes (`filename`, `must_include`, `must_not_include`).

---
## `test_convert_url`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:132`](/packages/markitdown/tests/test_cli_vectors.py#L132-L150)

**Dependencies:** `decode`, `getpreferredencoding`, `run`, `sleep`, `test_convert_url`  


# Function Documentation: test_convert_url

## Description
The `test_convert_url` function tests the conversion of a stream without stream information by executing a command-line interface (CLI) command using the `subprocess` module. It captures the output of the command and verifies that certain expected strings are present or absent in the output.

## Parameters

- `shared_tmp_dir` (Type: `str`): 
  - This parameter is intended to represent a temporary directory. However, it is not utilized within the function's implementation. It is included to match the function signature.

- `test_vector` (Type: `object`): 
  - This parameter is expected to be an object that contains the following attributes:
    - `filename` (Type: `str`): The name of the file to be processed, which is used to construct the command-line argument for the subprocess call.
    - `must_include` (Type: `list` of `str`): A list of strings that must be present in the output of the command for the test to pass.
    - `must_not_include` (Type: `list` of `str`): A list of strings that must not be present in the output of the command for the test to pass.

## Return Value
The function does not return a value. It raises an `AssertionError` if the CLI command exits with a non-zero return code or if the output does not meet the specified inclusion and exclusion criteria.

## Dependencies
- `subprocess`: Used to run the CLI command and capture its output.
- `time`: Used to introduce a delay of 1 second to avoid hitting rate limits.
- `locale`: Used to get the preferred encoding for decoding the output from the subprocess.
- `TEST_FILES_URL`: A constant (assumed to be defined elsewhere in the code) that represents the base URL for test files.

## Usage Example
```python
test_vector = {
    'filename': 'example_file.md',
    'must_include': ['Expected string 1', 'Expected string 2'],
    'must_not_include': ['Unexpected string 1', 'Unexpected string 2']
}

test_convert_url(shared_tmp_dir='/tmp', test_vector=test_vector)
``` 

In this example, the function is invoked with a temporary directory and a test vector containing a filename and lists of strings to check in the output.

---
## `test_output_to_file_with_data_uris`

**Location:** [`packages/markitdown/tests/test_cli_vectors.py:152`](/packages/markitdown/tests/test_cli_vectors.py#L152-L183)

**Dependencies:** `exists`, `join`, `open`, `read`, `remove`, `run`, `test_output_to_file_with_data_uris`  


# Function Documentation: test_output_to_file_with_data_uris

## Description
The `test_output_to_file_with_data_uris` function tests the command-line interface (CLI) functionality of the `markitdown` module when the `--keep-data-uris` option is enabled. It verifies that the output file is created correctly and contains the expected data.

## Parameters
- `shared_tmp_dir` (Type: `str`): A directory path used for temporary file storage. This directory is utilized to construct the path for the output file.
- `test_vector` (Type: `object`): An object that contains the following attributes:
  - `filename` (Type: `str`): The name of the input file (without extension) that is processed by the `markitdown` module.
  - `must_include` (Type: `list` of `str`): A list of strings that must be present in the output data.
  - `must_not_include` (Type: `list` of `str`): A list of strings that must not be present in the output data.

## Return Value
The function does not return any value. Its return type is `None`.

## Dependencies
The function explicitly calls the following external modules:
- `os`: Used for file path operations and checking file existence.
- `subprocess`: Used to run the `markitdown` module as a subprocess.
- `TEST_FILES_DIR`: A variable that should be defined elsewhere in the code, representing the directory where test files are located.

## Usage Example
```python
test_output_to_file_with_data_uris(shared_tmp_dir="/path/to/tmp", test_vector=TestVector(filename="example", must_include=["expected string"], must_not_include=["unexpected string"]))
```

In this example, `shared_tmp_dir` is set to a temporary directory path, and `test_vector` is an instance of a class or structure that contains the filename and lists of strings to check in the output.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
