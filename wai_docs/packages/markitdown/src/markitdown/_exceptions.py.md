# packages/markitdown/src/markitdown/_exceptions.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/_exceptions.py",
  "file_hash": "3a3d13a136045e6f54f68960da8e528bd298b096fcd70661b7b32e5846920e7f",
  "last_updated": "2025-12-23T15:46:16.183405+00:00",
  "functions": {
    "MarkItDownException": {
      "hash": "8dc891be4919c9004a5a213fbb5a0df76273cf67b5c923c757f9dab4308fb62a",
      "lines": "11-18",
      "last_updated": "2025-12-23T15:46:04.084442+00:00"
    },
    "MissingDependencyException": {
      "hash": "416e6854d631031de4f7cfb6cca46dbdf67acac289b6ba2126f48d5940a2be39",
      "lines": "19-33",
      "last_updated": "2025-12-23T15:46:07.112281+00:00"
    },
    "UnsupportedFormatException": {
      "hash": "e76d6369f94ae8a84548d4b1d641e8c5d3ed3f7aa9ff5021ba6daa29422a274e",
      "lines": "34-41",
      "last_updated": "2025-12-23T15:46:09.233481+00:00"
    },
    "FailedConversionAttempt": {
      "hash": "574102a32d7934d85e0394a501dfe33dd0d093338b006648ec9e69cdd2444a12",
      "lines": "42-51",
      "last_updated": "2025-12-23T15:46:12.239832+00:00"
    },
    "FileConversionException": {
      "hash": "83cbcc34d00d2395e9b021a7d0505c768096a3f202d111381be1a14ff21c492c",
      "lines": "52-77",
      "last_updated": "2025-12-23T15:46:16.183324+00:00"
    }
  }
}
```

</details>



The file `packages/markitdown/src/markitdown/_exceptions.py` implements a set of custom exception classes and a data structure to handle errors related to file conversion operations in the MarkItDown library. It defines a base exception class and several specific exceptions that are used to signal different error conditions encountered during the conversion process.

The main classes defined in this file are:
- `MarkItDownException`: The base exception class for all exceptions related to MarkItDown.
- `MissingDependencyException`: Raised when a required optional dependency for a converter is not installed, allowing the conversion process to skip the converter without terminating the entire operation.
- `UnsupportedFormatException`: Raised when no suitable converter is available for the provided file format.
- `FailedConversionAttempt`: A data structure that encapsulates a single attempt to convert a file, storing the converter used and any exception information.
- `FileConversionException`: Raised when a conversion attempt fails after finding a suitable converter. It includes an optional message and a list of `FailedConversionAttempt` instances to provide detailed information about the conversion attempts.

The file imports `Optional`, `List`, and `Any` from the `typing` module, which are used to define type hints for function parameters and return types. The code does not interact with external services or APIs, focusing solely on exception handling and data structures relevant to the MarkItDown library's file conversion functionality. The data structures defined include the `FailedConversionAttempt`, which holds references to the converter and exception information, and the various exception classes that provide specific error messages related to conversion issues.

## Functions and Classes

## `MarkItDownException`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:11`](/packages/markitdown/src/markitdown/_exceptions.py#L11-L18)

# MarkItDownException Documentation

## Overview
`MarkItDownException` is a custom exception class that inherits from Python's built-in `Exception` class. It serves as a base exception for the MarkItDown application.

## Parameters
The `MarkItDownException` class does not define any additional parameters or attributes beyond those provided by the base `Exception` class. It does not have a custom constructor, so it uses the default behavior of the `Exception` class.

### Inherited Parameters
- `args`: A tuple of arguments passed to the exception. This can be used to provide an error message or additional context when raising the exception.

## Return Value
The `MarkItDownException` class does not return any value. It is used to raise exceptions in the code where it is implemented.

## Dependencies
The `MarkItDownException` class does not have any dependencies on external modules, APIs, or services. It relies solely on the built-in `Exception` class provided by Python.

## Usage Example
To raise a `MarkItDownException`, the following pattern can be used:

```python
raise MarkItDownException("An error occurred in MarkItDown.")
```

This invocation raises the `MarkItDownException` with a specified error message.

---
## `MissingDependencyException`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:19`](/packages/markitdown/src/markitdown/_exceptions.py#L19-L33)

# MissingDependencyException Documentation

## Overview
`MissingDependencyException` is a custom exception class that inherits from `MarkItDownException`. This exception is raised when a converter's `convert()` method is invoked, but a required optional dependency is not installed. The presence of this exception indicates that the converter will be skipped, and an error will only be raised if no other suitable converter is available.

## Parameters
The `MissingDependencyException` class does not take any parameters in its constructor. It inherits from `MarkItDownException`, which may have its own parameters, but these are not specified in the provided code.

### Inherited Parameters
- If `MarkItDownException` has a constructor that accepts parameters, those would be applicable here, but the specific parameters are not detailed in the provided code.

## Return Value
The `MissingDependencyException` class does not return a value. It is used to signal an error condition when a required dependency is missing. When raised, it can carry an error message that indicates which dependency is missing.

## Dependencies
The code does not explicitly call any external modules, APIs, or services. However, it relies on the existence of the `MarkItDownException` class, which must be defined elsewhere in the codebase.

## Usage Example
To raise a `MissingDependencyException`, the following pattern can be used:

```python
raise MissingDependencyException("The required dependency 'example-package' is missing.")
```

This example demonstrates how to instantiate and raise the exception with a message indicating the missing dependency.

---
## `UnsupportedFormatException`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:34`](/packages/markitdown/src/markitdown/_exceptions.py#L34-L41)

# UnsupportedFormatException Documentation

## Overview
`UnsupportedFormatException` is a custom exception class that inherits from `MarkItDownException`. This exception is raised when a suitable converter cannot be found for a given file format.

## Parameters
The `UnsupportedFormatException` class does not take any parameters in its constructor. It inherits from `MarkItDownException`, which may have its own parameters, but these are not specified in the provided code.

## Return Value
The `UnsupportedFormatException` does not return a value. It is used to signal an error condition related to unsupported file formats.

## Dependencies
The `UnsupportedFormatException` class depends on the `MarkItDownException` class, which must be defined elsewhere in the codebase. There are no external modules, APIs, or services explicitly called in the provided implementation.

## Usage Example
To raise this exception, you can use the following invocation pattern:

```python
raise UnsupportedFormatException("No suitable converter found for the specified file format.")
``` 

This example demonstrates how to raise the `UnsupportedFormatException` with a message indicating the reason for the exception.

---
## `FailedConversionAttempt`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:42`](/packages/markitdown/src/markitdown/_exceptions.py#L42-L51)

# FailedConversionAttempt Class Documentation

## Overview
The `FailedConversionAttempt` class represents a single attempt to convert a file. It stores information about the converter used and any exceptions that occurred during the conversion process.

## Constructor

### `__init__(self, converter: Any, exc_info: Optional[tuple] = None)`

#### Parameters
- `converter` (Any): This parameter represents the converter used for the file conversion. The type is not restricted, allowing for any object to be passed.
- `exc_info` (Optional[tuple]): This parameter is optional and defaults to `None`. It is intended to hold exception information, typically captured using the `sys.exc_info()` function, which returns a tuple of exception type, value, and traceback.

#### Usage
The constructor initializes two instance variables:
- `self.converter`: Stores the converter object passed to the constructor.
- `self.exc_info`: Stores the exception information tuple if provided; otherwise, it remains `None`.

## Return Value
The constructor does not return a value. It initializes an instance of the `FailedConversionAttempt` class.

## Dependencies
The code does not explicitly import any external modules or libraries. However, it is common to use the `sys` module for capturing exception information, which is implied but not shown in the provided code.

## Example Usage
```python
# Example of creating a FailedConversionAttempt instance
converter_instance = SomeConverter()  # Replace with an actual converter instance
exception_info = (TypeError, ValueError("An error occurred"), None)  # Example exception info

failed_attempt = FailedConversionAttempt(converter=converter_instance, exc_info=exception_info)
```

---
## `FileConversionException`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:52`](/packages/markitdown/src/markitdown/_exceptions.py#L52-L77)

# FileConversionException Class Documentation

## Overview
The `FileConversionException` class is a custom exception that is thrown when a file conversion process fails after a suitable converter has been found. This class extends from `MarkItDownException`.

## Constructor
The constructor initializes the exception with a message and a list of failed conversion attempts.

### Parameters
- `message` (Optional[str]): A string that describes the error. If not provided, a default message is generated based on the number of attempts.
  
- `attempts` (Optional[List[FailedConversionAttempt]]): A list of `FailedConversionAttempt` objects that represent the attempts made to convert the file. This parameter is used to generate detailed error messages based on the attempts.

### Implementation Details
- If `message` is `None` and `attempts` is also `None`, the default message "File conversion failed." is used.
- If `attempts` is provided, the message includes the number of attempts made. For each attempt:
  - If `exc_info` is `None`, the message indicates that the converter provided no execution info.
  - If `exc_info` is present, the message includes the type of exception thrown and the associated message.

### Return Value
The constructor does not return a value but initializes an instance of `FileConversionException` with the specified message and attempts.

## Dependencies
- The class inherits from `MarkItDownException`, which must be defined elsewhere in the codebase.
- The class relies on the `FailedConversionAttempt` type, which must also be defined in the codebase.

## Usage Example
```python
# Example of creating a FileConversionException with attempts
failed_attempts = [
    FailedConversionAttempt(converter=SomeConverter(), exc_info=(ValueError, "Invalid format")),
    FailedConversionAttempt(converter=AnotherConverter(), exc_info=None)
]

exception = FileConversionException(attempts=failed_attempts)
raise exception
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
