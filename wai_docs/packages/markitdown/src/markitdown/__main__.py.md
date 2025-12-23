# packages/markitdown/src/markitdown/__main__.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/__main__.py",
  "file_hash": "fb740c426f73a15dec7195c66fdce0470496172b5b5597f23507af76e600bfbd",
  "last_updated": "2025-12-23T15:45:40.417158+00:00",
  "functions": {
    "main": {
      "hash": "f8772009f501df1d7b97db73a72f6d30372624a0f5bdecd12e675a6e0a87c302",
      "lines": "13-202",
      "last_updated": "2025-12-23T15:45:34.522975+00:00"
    },
    "_handle_output": {
      "hash": "e07a680609c58e2d2b4964cbc4ffc7e29ed6aa3edf9500b4547bd88e5d64a546",
      "lines": "203-216",
      "last_updated": "2025-12-23T15:45:38.564179+00:00"
    },
    "_exit_with_error": {
      "hash": "1c34edf950e7be1ee5c238dbca249142b7bf904938c5286287453551274c66b7",
      "lines": "217-221",
      "last_updated": "2025-12-23T15:45:40.417047+00:00"
    }
  }
}
```

</details>



The Python file `__main__.py` in the `markitdown` package implements a command-line interface for converting various file formats to Markdown. It utilizes the `argparse` module to define and parse command-line arguments, allowing users to specify input files, output options, and various hints regarding file characteristics such as extension, MIME type, and charset. The main function, `main`, orchestrates the parsing of these arguments, validates the input, and invokes the Markdown conversion process using the `MarkItDown` class.

The file defines three primary functions: `main`, `_handle_output`, and `_exit_with_error`. The `main` function is responsible for setting up the argument parser, validating the input parameters, and managing the conversion process. The `_handle_output` function (not fully shown in the provided code) is likely responsible for handling the output of the conversion results, while `_exit_with_error` is used to terminate the program with an error message when invalid input is detected. The code also interacts with the `MarkItDown` class and `StreamInfo` data structure from the `_markitdown` module to facilitate the conversion process.

Concrete dependencies in this file include the standard libraries `argparse`, `sys`, `codecs`, and `textwrap`, as well as the `entry_points` function from the `importlib.metadata` module. The file also relies on the `MarkItDown`, `StreamInfo`, and `DocumentConverterResult` classes from the `_markitdown` module. The data structures manipulated include the `StreamInfo`, which encapsulates information about the file's extension, MIME type, and charset, and the command-line arguments parsed into the `args` object, which contains user-specified options for the conversion process.

## Functions and Classes

## `main`

**Location:** [`packages/markitdown/src/markitdown/__main__.py:13`](/packages/markitdown/src/markitdown/__main__.py#L13-L202)

# Function Documentation: `main`

## Description
The `main` function serves as the entry point for a command-line application that converts various file formats to Markdown. It utilizes the `argparse` module to parse command-line arguments and options, processes input files or standard input, and manages output based on user specifications.

## Parameters
The function does not take any parameters directly. Instead, it uses command-line arguments parsed from the user input. The relevant command-line arguments are as follows:

- `-v`, `--version`
  - **Type**: Flag
  - **Usage**: Displays the version number of the program and exits.

- `-o`, `--output`
  - **Type**: `str`
  - **Usage**: Specifies the output file name. If not provided, output is written to standard output.

- `-x`, `--extension`
  - **Type**: `str`
  - **Usage**: Provides a hint about the file extension when reading from standard input. It is processed to ensure it starts with a dot.

- `-m`, `--mime-type`
  - **Type**: `str`
  - **Usage**: Provides a hint about the file's MIME type. It is validated to ensure it contains a single slash.

- `-c`, `--charset`
  - **Type**: `str`
  - **Usage**: Provides a hint about the file's character set. It is validated against known charsets.

- `-d`, `--use-docintel`
  - **Type**: Flag
  - **Usage**: Indicates that Document Intelligence should be used for text extraction. Requires a valid Document Intelligence Endpoint.

- `-e`, `--endpoint`
  - **Type**: `str`
  - **Usage**: Specifies the Document Intelligence Endpoint. Required if using Document Intelligence.

- `-p`, `--use-plugins`
  - **Type**: Flag
  - **Usage**: Indicates that third-party plugins should be used for file conversion.

- `--list-plugins`
  - **Type**: Flag
  - **Usage**: Lists installed third-party plugins and exits.

- `--keep-data-uris`
  - **Type**: Flag
  - **Usage**: Indicates that data URIs should be retained in the output. By default, data URIs are truncated.

- `filename`
  - **Type**: `str` (optional)
  - **Usage**: The name of the file to be converted. If not provided, the function reads from standard input.

## Return Value
The function does not return a value. It performs file conversion and handles output directly based on the provided arguments.

## Dependencies
The function relies on the following external modules:
- `argparse`: For parsing command-line arguments.
- `sys`: For handling standard input and output.
- `codecs`: For character set lookup.
- `entry_points`: To list installed plugins.
- `MarkItDown`: A class presumably defined elsewhere in the codebase for handling the conversion logic.
- `_exit_with_error`: A function presumably defined elsewhere to handle error exits.
- `_handle_output`: A function presumably defined elsewhere to manage output handling.

## Usage Example
To convert a PDF file to Markdown and save the output to a file:
```
markitdown example.pdf -o example.md
```

To read from standard input and convert:
```
cat example.pdf | markitdown
```

To list installed plugins:
```
markitdown --list-plugins
```

---
## `_handle_output`

**Location:** [`packages/markitdown/src/markitdown/__main__.py:203`](/packages/markitdown/src/markitdown/__main__.py#L203-L216)

# Function Documentation: _handle_output

## Description
The `_handle_output` function handles the output of a `DocumentConverterResult` either by writing it to a specified file or printing it to standard output (stdout). If the output is directed to a file, the function writes the `markdown` attribute of the `result` to that file. If no output file is specified, it prints the `markdown` to stdout, handling any potential encoding errors by replacing problematic characters.

## Parameters

- `args`: 
  - Type: `Namespace`
  - Constraints: Must contain an `output` attribute which is a string representing the file path to which the output should be written. If `output` is `None`, the function will print to stdout.
  - Usage: The function checks the `output` attribute to determine whether to write to a file or print to stdout.

- `result`: 
  - Type: `DocumentConverterResult`
  - Constraints: Must have a `markdown` attribute that contains the content to be written or printed. The type of `markdown` is expected to be a string.
  - Usage: The function accesses the `markdown` attribute of `result` to obtain the content for output.

## Return Value
The function does not return a value. Its purpose is to handle output, either by writing to a file or printing to stdout.

## Dependencies
- `sys`: The function uses `sys.stdout.encoding` to determine the encoding for printing to standard output.
- `DocumentConverterResult`: This is a custom class that must be defined elsewhere in the codebase, containing at least the `markdown` attribute.

## Usage Example
```python
from your_module import _handle_output
from your_module import DocumentConverterResult
import argparse

# Example argument parsing
parser = argparse.ArgumentParser()
parser.add_argument('--output', type=str, help='Output file path')
args = parser.parse_args()

# Example result creation
result = DocumentConverterResult(markdown="This is a sample markdown content.")

# Function invocation
_handle_output(args, result)
```

---
## `_exit_with_error`

**Location:** [`packages/markitdown/src/markitdown/__main__.py:217`](/packages/markitdown/src/markitdown/__main__.py#L217-L221)

# Function Documentation: _exit_with_error

## Description
The `_exit_with_error` function prints a specified error message to the standard output and terminates the program with an exit status code of 1.

## Parameters
- `message` (str): A string that represents the error message to be printed. This parameter is required and must be of type `str`.

## Return Value
The function does not return a value. It terminates the program using `sys.exit(1)`.

## Dependencies
- `sys`: The function calls `sys.exit(1)` to terminate the program. Therefore, the `sys` module must be imported for the function to operate correctly.

## Usage Example
```python
import sys

_exit_with_error("An error has occurred.")
```
In this example, the function is called with the string "An error has occurred." as the argument, which will be printed to the console, and the program will exit with a status code of 1.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
