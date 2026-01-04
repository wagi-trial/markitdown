# packages/markitdown/src/markitdown/__main__.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/__main__.py",
  "file_hash": "fb740c426f73a15dec7195c66fdce0470496172b5b5597f23507af76e600bfbd",
  "last_updated": "2026-01-04T17:16:20.115218+00:00",
  "functions": {
    "main": {
      "hash": "f8772009f501df1d7b97db73a72f6d30372624a0f5bdecd12e675a6e0a87c302",
      "lines": "13-202",
      "last_updated": "2026-01-04T17:16:15.664169+00:00"
    },
    "_handle_output": {
      "hash": "e07a680609c58e2d2b4964cbc4ffc7e29ed6aa3edf9500b4547bd88e5d64a546",
      "lines": "203-216",
      "last_updated": "2026-01-04T17:16:18.388774+00:00"
    },
    "_exit_with_error": {
      "hash": "1c34edf950e7be1ee5c238dbca249142b7bf904938c5286287453551274c66b7",
      "lines": "217-221",
      "last_updated": "2026-01-04T17:16:20.115149+00:00"
    }
  }
}
```

</details>



The Python file `__main__.py` in the `markitdown` package implements a command-line interface for converting various file formats to Markdown. It utilizes the `argparse` module to handle command-line arguments, allowing users to specify input files, output files, and various options related to file processing. The main function orchestrates the parsing of arguments, validates input, and invokes the `MarkItDown` class for file conversion based on the provided parameters.

The file defines three functions: `main`, `_handle_output`, and `_exit_with_error`. The `main` function is responsible for setting up the argument parser, processing input arguments, and managing the conversion workflow. It handles options such as output file specification, MIME type hints, and the use of Document Intelligence for text extraction. The `_handle_output` function is invoked to manage the output of the conversion results, while `_exit_with_error` is used to terminate the program with an error message when invalid input is detected. The code also imports several modules, including `argparse`, `sys`, `codecs`, and `textwrap`, and it relies on the `MarkItDown`, `StreamInfo`, and `DocumentConverterResult` classes from the `_markitdown` module for the core functionality of file conversion.

The file manipulates several data structures, including command-line arguments parsed into an `argparse.Namespace` object, and it constructs a `StreamInfo` object to encapsulate file extension, MIME type, and charset information. The code also interacts with external services through the Document Intelligence API, requiring a valid endpoint when the `--use-docintel` option is specified. The file supports plugin architecture by listing installed third-party plugins using the `entry_points` function from the `importlib.metadata` module, enhancing its extensibility for additional file conversion capabilities.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `main`

<details>
<summary><strong>Calls/Dependencies</strong> (26 unique functions)</summary>

- `ArgumentParser`
- `MarkItDown`
- `StreamInfo`
- `URIs`
- `_exit_with_error`
- `_handle_output`
- `add_argument`
- `charset`
- `convert`
- `convert_stream`
- `count`
- `dedent`
- `entry_points`
- `exit`
- `extension`
- `len`
- `list`
- `lookup`
- `lower`
- `main`
- `p`
- `parse_args`
- `print`
- `startswith`
- `strip`
- `t`

</details>

### `_handle_output`

<details>
<summary><strong>Calls/Dependencies</strong> (6 unique functions)</summary>

- `_handle_output`
- `decode`
- `encode`
- `open`
- `print`
- `write`

</details>

### `_exit_with_error`

<details>
<summary><strong>Calls/Dependencies</strong> (3 unique functions)</summary>

- `_exit_with_error`
- `exit`
- `print`

</details>

</details>



## Functions and Classes

## `main`

**Location:** [`packages/markitdown/src/markitdown/__main__.py:13`](/packages/markitdown/src/markitdown/__main__.py#L13-L202)

**Dependencies:** `ArgumentParser`, `MarkItDown`, `StreamInfo`, `URIs`, `_exit_with_error`, `_handle_output`, `add_argument`, `charset`, `convert`, `convert_stream`, `count`, `dedent`, `entry_points`, `exit`, `extension` *(+11 more)*  


# Function Documentation: `main`

## Description
The `main` function serves as the entry point for a command-line interface (CLI) tool that converts various file formats to Markdown. It utilizes the `argparse` module to handle command-line arguments and options, processes input files, and manages output based on user specifications.

## Parameters
The `main` function does not take any parameters directly. Instead, it processes command-line arguments defined through `argparse`. The following arguments are supported:

- `-v`, `--version`
  - **Type**: Flag
  - **Description**: Displays the version number of the program and exits.

- `-o`, `--output`
  - **Type**: String
  - **Description**: Specifies the output file name. If not provided, the output is written to standard output (stdout).

- `-x`, `--extension`
  - **Type**: String
  - **Description**: Provides a hint about the file extension (e.g., when reading from stdin).

- `-m`, `--mime-type`
  - **Type**: String
  - **Description**: Provides a hint about the file's MIME type.

- `-c`, `--charset`
  - **Type**: String
  - **Description**: Provides a hint about the file's charset (e.g., UTF-8).

- `-d`, `--use-docintel`
  - **Type**: Flag
  - **Description**: Enables the use of Document Intelligence to extract text instead of offline conversion. Requires a valid Document Intelligence Endpoint.

- `-e`, `--endpoint`
  - **Type**: String
  - **Description**: Specifies the Document Intelligence Endpoint. This is required if using Document Intelligence.

- `-p`, `--use-plugins`
  - **Type**: Flag
  - **Description**: Enables the use of third-party plugins to convert files. Use `--list-plugins` to see installed plugins.

- `--list-plugins`
  - **Type**: Flag
  - **Description**: Lists installed third-party plugins and exits.

- `--keep-data-uris`
  - **Type**: Flag
  - **Description**: Retains data URIs (like base64-encoded images) in the output. By default, data URIs are truncated.

- `filename`
  - **Type**: String (optional)
  - **Description**: The name of the file to be converted. If not provided, the function reads from standard input (stdin).

## Return Value
The `main` function does not return a value. It performs operations based on the parsed arguments and manages output accordingly.

## Dependencies
The function relies on the following external modules and services:
- `argparse`: For parsing command-line arguments.
- `sys`: For handling standard input and output.
- `codecs`: For character set lookups.
- `StreamInfo`: A custom class presumably defined elsewhere in the codebase, used to encapsulate file stream information.
- `MarkItDown`: A custom class presumably defined elsewhere in the codebase, responsible for converting files to Markdown format.
- Document Intelligence service: Required if the `--use-docintel` flag is specified.

## Usage Example
To convert a PDF file to Markdown and save the output to a file named `example.md`, use the following command:

```
markitdown example.pdf -o example.md
```

To read from standard input and convert the content, use:

```
cat example.pdf | markitdown
```

To list installed plugins, use:

```
markitdown --list-plugins
```

---
## `_handle_output`

**Location:** [`packages/markitdown/src/markitdown/__main__.py:203`](/packages/markitdown/src/markitdown/__main__.py#L203-L216)

**Dependencies:** `_handle_output`, `decode`, `encode`, `open`, `print`, `write`  


# Function Documentation: _handle_output

## Description
The `_handle_output` function handles the output of a `DocumentConverterResult` either by writing it to a specified file or printing it to standard output (stdout). If an output file is specified in the `args` parameter, the function writes the `markdown` attribute of the `result` to that file. If no output file is specified, the function prints the `markdown` to stdout, ensuring that any encoding errors are handled gracefully.

## Parameters
- `args`: An object that contains the following attribute:
  - `output` (str or None): A string representing the file path to which the output should be written. If `None`, the function will print to stdout.
  
- `result`: An instance of `DocumentConverterResult`, which must contain:
  - `markdown` (str): A string that represents the markdown content to be output.

## Return Value
The function does not return any value (return type is `None`).

## External Dependencies
- `sys`: The function uses `sys.stdout.encoding` to determine the encoding of the standard output for printing purposes.

## Usage Example
```python
class DocumentConverterResult:
    def __init__(self, markdown):
        self.markdown = markdown

args = type('Args', (object,), {'output': 'output.md'})()
result = DocumentConverterResult(markdown="# Sample Markdown Content")

_handle_output(args, result)
```

In this example, the markdown content will be written to a file named `output.md`. If `args.output` were `None`, the markdown content would be printed to the console instead.

---
## `_exit_with_error`

**Location:** [`packages/markitdown/src/markitdown/__main__.py:217`](/packages/markitdown/src/markitdown/__main__.py#L217-L221)

**Dependencies:** `_exit_with_error`, `exit`, `print`  


# Function Documentation: _exit_with_error

## Description
The `_exit_with_error` function prints a specified error message to the standard output and then terminates the program with an exit status of 1.

## Parameters
- **message** (str): A string that contains the error message to be printed. This parameter is required and must be of type `str`.

## Return Value
The function does not return a value. It terminates the program execution using `sys.exit(1)`.

## Dependencies
- The function uses the `sys` module, which must be imported for the function to operate correctly. The `sys.exit()` function is called to terminate the program.

## Usage Example
```python
_exit_with_error("An error has occurred.")
``` 

In this example, the string "An error has occurred." will be printed to the standard output, and the program will exit with a status code of 1.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
