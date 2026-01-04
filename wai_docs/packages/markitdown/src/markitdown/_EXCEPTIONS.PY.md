# packages/markitdown/src/markitdown/_exceptions.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/_exceptions.py",
  "file_hash": "3a3d13a136045e6f54f68960da8e528bd298b096fcd70661b7b32e5846920e7f",
  "last_updated": "2026-01-04T17:16:52.897905+00:00",
  "functions": {
    "MarkItDownException": {
      "hash": "8dc891be4919c9004a5a213fbb5a0df76273cf67b5c923c757f9dab4308fb62a",
      "lines": "11-18",
      "last_updated": "2026-01-04T17:16:42.289045+00:00"
    },
    "MissingDependencyException": {
      "hash": "416e6854d631031de4f7cfb6cca46dbdf67acac289b6ba2126f48d5940a2be39",
      "lines": "19-33",
      "last_updated": "2026-01-04T17:16:44.820177+00:00"
    },
    "UnsupportedFormatException": {
      "hash": "e76d6369f94ae8a84548d4b1d641e8c5d3ed3f7aa9ff5021ba6daa29422a274e",
      "lines": "34-41",
      "last_updated": "2026-01-04T17:16:46.817676+00:00"
    },
    "FailedConversionAttempt": {
      "hash": "574102a32d7934d85e0394a501dfe33dd0d093338b006648ec9e69cdd2444a12",
      "lines": "42-51",
      "last_updated": "2026-01-04T17:16:49.731008+00:00"
    },
    "FileConversionException": {
      "hash": "83cbcc34d00d2395e9b021a7d0505c768096a3f202d111381be1a14ff21c492c",
      "lines": "52-77",
      "last_updated": "2026-01-04T17:16:52.897782+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/_exceptions.py` implements a set of exception classes and a data structure related to the MarkItDown library, which is designed for file conversion. It defines a base exception class and several specific exceptions that handle different error scenarios during the conversion process. The file also includes a class to represent a failed conversion attempt, encapsulating details about the converter used and any exception information.

The following classes are defined in the file:

1. **MarkItDownException**: This is the base exception class for the MarkItDown library.
2. **MissingDependencyException**: This exception is raised when a required optional dependency for a converter is not installed, indicating that the converter will be skipped if no other suitable converter is available.
3. **UnsupportedFormatException**: This exception is thrown when no suitable converter is found for a given file format.
4. **FailedConversionAttempt**: This class represents a single attempt to convert a file, storing the converter used and optional exception information.
5. **FileConversionException**: This exception is raised when a conversion process fails after a suitable converter has been found. It can include a message and a list of `FailedConversionAttempt` instances detailing the attempts made during the conversion process.

The code imports `Optional`, `List`, and `Any` from the `typing` module, which are used for type hinting in the class definitions and method signatures. The file does not define any external dependencies or services beyond these type hints. The data structures manipulated in this file include lists (for storing multiple `FailedConversionAttempt` instances) and optional types for parameters, allowing for flexible handling of error messages and conversion attempts.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `MarkItDownException`

<details>
<summary><strong>Calls/Dependencies</strong> (1 unique function)</summary>

- `MarkItDownException`

</details>

### `MissingDependencyException`

<details>
<summary><strong>Calls/Dependencies</strong> (3 unique functions)</summary>

- `MissingDependencyException`
- `convert`
- `skipped`

</details>

### `UnsupportedFormatException`

<details>
<summary><strong>Calls/Dependencies</strong> (1 unique function)</summary>

- `UnsupportedFormatException`

</details>

### `FailedConversionAttempt`

**Nested Functions:**
- `__init__`

<details>
<summary><strong>Calls/Dependencies</strong> (2 unique functions)</summary>

- `FailedConversionAttempt`
- `__init__`

</details>

### `FileConversionException`

**Nested Functions:**
- `__init__`

<details>
<summary><strong>Calls/Dependencies</strong> (5 unique functions)</summary>

- `FileConversionException`
- `__init__`
- `len`
- `super`
- `type`

</details>

</details>



## Functions and Classes

## `MarkItDownException`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:11`](/packages/markitdown/src/markitdown/_exceptions.py#L11-L18)

**Dependencies:** `MarkItDownException`  


# MarkItDownException Documentation

## Overview
`MarkItDownException` is a custom exception class that inherits from Python's built-in `Exception` class. It serves as a base exception for the MarkItDown application.

## Parameters
The `MarkItDownException` class does not take any parameters in its constructor. It utilizes the default constructor from the base `Exception` class.

### Constructor
- **Parameters**: None
- **Type**: N/A
- **Usage**: The class can be instantiated without any arguments.

## Return Value
The `MarkItDownException` class does not have a return value as it is an exception class. When an instance of this class is raised, it indicates an error condition specific to the MarkItDown application.

## Dependencies
The `MarkItDownException` class does not have any dependencies on external modules, APIs, or services. It solely relies on the built-in `Exception` class provided by Python.

## Usage Example
To raise a `MarkItDownException`, you can use the following code snippet:

```python
raise MarkItDownException("An error occurred in MarkItDown.")
```

This example demonstrates how to instantiate and raise the `MarkItDownException` with a custom error message.

---
## `MissingDependencyException`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:19`](/packages/markitdown/src/markitdown/_exceptions.py#L19-L33)

**Dependencies:** `MissingDependencyException`, `convert`, `skipped`  


# MissingDependencyException Documentation

## Overview
`MissingDependencyException` is a custom exception class that inherits from `MarkItDownException`. This exception is raised when a converter's `convert()` method is invoked, but the required optional dependency for that converter is not installed. The occurrence of this exception does not halt the execution of the program, as the converter will be skipped, and an error will only be raised if no other suitable converter is available.

## Parameters
The `MissingDependencyException` class does not take any parameters in its constructor. It inherits from `MarkItDownException`, which may have its own parameters, but these are not specified in the provided code.

## Return Value
The `MissingDependencyException` class does not have a return value as it is an exception class. When raised, it indicates that a required dependency is missing, and it can be caught and handled by the calling code.

## Dependencies
The code explicitly depends on the following:
- `MarkItDownException`: This is the base class from which `MissingDependencyException` inherits. The implementation of `MarkItDownException` is not provided in the code snippet.

## Usage Example
To raise the `MissingDependencyException`, you can use the following pattern:

```python
raise MissingDependencyException("The required dependency 'example_dependency' is missing.")
```

In this example, the exception is raised with a message indicating which dependency is missing. This message can be retrieved later when handling the exception.

---
## `UnsupportedFormatException`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:34`](/packages/markitdown/src/markitdown/_exceptions.py#L34-L41)

**Dependencies:** `UnsupportedFormatException`  


# UnsupportedFormatException Class Documentation

## Overview
`UnsupportedFormatException` is a custom exception class that inherits from `MarkItDownException`. This exception is raised when no suitable converter is found for a given file format.

## Parameters
The `UnsupportedFormatException` class does not take any parameters in its constructor. It inherits the behavior of the base class `MarkItDownException`, which may define its own parameters. However, the implementation provided does not specify any additional parameters or constraints.

## Return Value
The `UnsupportedFormatException` class does not return any value. It is used to signal an error condition when an unsupported file format is encountered.

## Dependencies
The `UnsupportedFormatException` class depends on the following:
- `MarkItDownException`: This is the base class from which `UnsupportedFormatException` inherits. The implementation of `MarkItDownException` is not provided in the code snippet.

## Usage Example
To raise an `UnsupportedFormatException`, the following pattern can be used:

```python
raise UnsupportedFormatException("No suitable converter found for the specified file format.")
``` 

This example demonstrates how to instantiate and raise the `UnsupportedFormatException` with a message indicating the reason for the exception.

---
## `FailedConversionAttempt`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:42`](/packages/markitdown/src/markitdown/_exceptions.py#L42-L51)

**Nested Functions:** `__init__`  
**Dependencies:** `FailedConversionAttempt`, `__init__`  


# FailedConversionAttempt Class Documentation

## Overview
The `FailedConversionAttempt` class represents a single attempt to convert a file. It stores information about the converter used and any exception information that may have occurred during the conversion attempt.

## Constructor

### `__init__(self, converter: Any, exc_info: Optional[tuple] = None)`

#### Parameters:
- `converter` (Any): This parameter represents the converter used for the conversion attempt. It can be of any type.
- `exc_info` (Optional[tuple]): This parameter is an optional tuple that contains exception information related to the conversion attempt. If no exception occurred, this parameter can be set to `None`.

#### Usage:
The constructor initializes the `converter` and `exc_info` attributes of the `FailedConversionAttempt` instance.

## Return Value
The constructor does not return a value. Instead, it initializes an instance of the `FailedConversionAttempt` class, which contains the following attributes:
- `self.converter`: Stores the converter used for the conversion attempt.
- `self.exc_info`: Stores the exception information, if any, related to the conversion attempt.

## Dependencies
The class does not have any explicit dependencies on external modules, APIs, or services.

## Example Usage
```python
# Example of creating a FailedConversionAttempt instance
converter_instance = SomeConverter()  # Assuming SomeConverter is defined elsewhere
exception_info = (type(Exception), Exception("Conversion failed"), None)

failed_attempt = FailedConversionAttempt(converter=converter_instance, exc_info=exception_info)
```

---
## `FileConversionException`

**Location:** [`packages/markitdown/src/markitdown/_exceptions.py:52`](/packages/markitdown/src/markitdown/_exceptions.py#L52-L77)

**Nested Functions:** `__init__`  
**Dependencies:** `FileConversionException`, `__init__`, `len`, `super`, `type`  


# FileConversionException Documentation

## Overview
`FileConversionException` is a custom exception class that inherits from `MarkItDownException`. This exception is raised when a file conversion process fails after a suitable converter has been identified.

## Parameters

### `message`
- **Type**: `Optional[str]`
- **Constraints**: Can be `None` or a string.
- **Usage**: This parameter allows for a custom error message to be provided. If it is `None`, a default message is generated based on the number of conversion attempts.

### `attempts`
- **Type**: `Optional[List[FailedConversionAttempt]]`
- **Constraints**: Can be `None` or a list of `FailedConversionAttempt` objects.
- **Usage**: This parameter holds a list of conversion attempts that failed. If provided, the exception message will include details about each attempt, including the type of converter used and any exceptions raised during the conversion process.

## Return Value
The constructor does not return a value but initializes an instance of `FileConversionException`. The instance contains:
- A message string that describes the failure.
- A list of failed conversion attempts, if provided.

## Dependencies
- The class `MarkItDownException` must be defined in the same module or imported from another module.
- The type `FailedConversionAttempt` must be defined in the same module or imported from another module.

## Usage Example
```python
# Assuming FailedConversionAttempt and MarkItDownException are defined

attempts = [
    FailedConversionAttempt(converter=SomeConverter(), exc_info=(ValueError, "Invalid format")),
    FailedConversionAttempt(converter=AnotherConverter(), exc_info=None)
]

try:
    # Code that attempts file conversion
    pass
except Exception:
    raise FileConversionException(attempts=attempts)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
