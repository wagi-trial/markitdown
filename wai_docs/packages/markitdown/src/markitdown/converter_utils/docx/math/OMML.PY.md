# packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py",
  "file_hash": "82dc30e0c9cd672a324b6d0d1a5f44c4a823908593ee65406431f975b93d4297",
  "last_updated": "2026-01-04T17:18:25.356700+00:00",
  "functions": {
    "load": {
      "hash": "6d3316330d9820f633e9d518acfa526c30da3e8ffdc67126b7b50c482b386674",
      "lines": "43-48",
      "last_updated": "2026-01-04T17:17:55.925390+00:00"
    },
    "load_string": {
      "hash": "69a2e347f95e3d0639d927c1a67f8cdd24db0959f406fd56facc513bc9899184",
      "lines": "49-54",
      "last_updated": "2026-01-04T17:17:59.111248+00:00"
    },
    "escape_latex": {
      "hash": "11d0d27e7f02aadcc741dbfa19dcfb3e3e57c4048845ff0c92a2a4f89765ebf0",
      "lines": "55-67",
      "last_updated": "2026-01-04T17:18:02.085306+00:00"
    },
    "get_val": {
      "hash": "a9dd3689f472fbeddad24b9873b816785a4629feec27d05aaf57e6b0e4b2a4b0",
      "lines": "68-74",
      "last_updated": "2026-01-04T17:18:05.466575+00:00"
    },
    "Tag2Method": {
      "hash": "e123f03f9b7f903ba95cfc7e65e8ac923b1f8beff4dc47ca333d28bf36b23552",
      "lines": "75-126",
      "last_updated": "2026-01-04T17:18:10.685330+00:00"
    },
    "Pr": {
      "hash": "db73421ed920d8b699b29e0ee4744a775bf5377a3237be9ff81865072ae53b1a",
      "lines": "127-169",
      "last_updated": "2026-01-04T17:18:16.215301+00:00"
    },
    "oMath2Latex": {
      "hash": "ed203725c7094c3eb09c7f0d81a63ad3d82eebde8fea86b672eb9d6a34e5cc9f",
      "lines": "170-401",
      "last_updated": "2026-01-04T17:18:25.356640+00:00"
    }
  }
}
```

</details>



The `omml.py` file implements functionality for processing Office Math Markup Language (OMML) elements and converting them to LaTeX format. It provides methods to load OMML data from a stream or a string, escape LaTeX special characters, and extract values from elements. The primary classes defined in this file are `Tag2Method`, `Pr`, and `oMath2Latex`, which facilitate the parsing and conversion of OMML elements.

The `load` and `load_string` functions parse OMML data and yield LaTeX representations of the `oMath` elements found within. The `escape_latex` function ensures that special LaTeX characters are properly escaped. The `get_val` function retrieves values from a specified store or returns a default value if the key is not found. The `Tag2Method` class serves as a base class for processing OMML tags, providing methods to handle child elements and unknown tags. The `Pr` class extends `Tag2Method` to handle specific OMML properties, while the `oMath2Latex` class is responsible for converting `oMath` elements to LaTeX format.

The code imports the `ElementTree` module from the `defusedxml` package for safe XML parsing, and it imports various constants from a `latex_dict` module, which likely contains mappings and definitions relevant to LaTeX conversion. The file manipulates data structures such as dictionaries and strings to store and process the properties of OMML elements. The `tag2meth` dictionary in both `Tag2Method` and `Pr` classes maps OMML tags to their corresponding processing methods, facilitating a structured approach to handling different types of mathematical expressions.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `load`

<details>
<summary><strong>Calls/Dependencies</strong> (4 unique functions)</summary>

- `findall`
- `load`
- `oMath2Latex`
- `parse`

</details>

### `load_string`

<details>
<summary><strong>Calls/Dependencies</strong> (4 unique functions)</summary>

- `findall`
- `fromstring`
- `load_string`
- `oMath2Latex`

</details>

### `escape_latex`

<details>
<summary><strong>Calls/Dependencies</strong> (5 unique functions)</summary>

- `and`
- `append`
- `escape_latex`
- `join`
- `replace`

</details>

### `get_val`

<details>
<summary><strong>Calls/Dependencies</strong> (2 unique functions)</summary>

- `get`
- `get_val`

</details>

### `Tag2Method`

**Nested Functions:**
- `call_method`
- `process_children_list`
- `process_children_dict`
- `process_children`
- `process_unknow`

<details>
<summary><strong>Calls/Dependencies</strong> (16 unique functions)</summary>

- `Tag2Method`
- `and`
- `call_method`
- `dict`
- `getmethod`
- `isinstance`
- `join`
- `list`
- `method`
- `process_children`
- `process_children_dict`
- `process_children_list`
- `process_unknow`
- `replace`
- `str`
- `yield`

</details>

### `Pr`

**Nested Functions:**
- `__init__`
- `__str__`
- `__unicode__`
- `__getattr__`
- `do_brk`
- `do_common`

<details>
<summary><strong>Calls/Dependencies</strong> (11 unique functions)</summary>

- `Pr`
- `__getattr__`
- `__init__`
- `__str__`
- `__unicode__`
- `do_brk`
- `do_common`
- `format`
- `get`
- `process_children`
- `replace`

</details>

### `oMath2Latex`

**Nested Functions:**
- `__init__`
- `__str__`
- `__unicode__`
- `process_unknow`
- `latex`
- `do_acc`
- `do_bar`
- `do_d`
- `do_spre`
- `do_sub`
- `do_sup`
- `do_f`
- `do_func`
- `do_fname`
- `do_groupchr`
- `do_rad`
- `do_eqarr`
- `do_limlow`
- `do_limupp`
- `do_lim`
- `do_m`
- `do_mr`
- `do_nary`
- `do_r`

<details>
<summary><strong>Calls/Dependencies</strong> (42 unique functions)</summary>

- `NotImplementedError`
- `Pr`
- `__init__`
- `__str__`
- `__unicode__`
- `append`
- `do_acc`
- `do_bar`
- `do_d`
- `do_eqarr`
- `do_f`
- `do_fname`
- `do_func`
- `do_groupchr`
- `do_lim`
- `do_limlow`
- `do_limupp`
- `do_m`
- `do_mr`
- `do_nary`
- `do_r`
- `do_rad`
- `do_spre`
- `do_sub`
- `do_sup`
- `escape_latex`
- `findtext`
- `format`
- `get`
- `get_val`
- `isinstance`
- `join`
- `latex`
- `oMath2Latex`
- `object`
- `process_children`
- `process_children_dict`
- `process_children_list`
- `process_unknow`
- `replace`
- `text`
- `unicode`

</details>

</details>



## Functions and Classes

## `load`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:43`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L43-L48)

**Dependencies:** `findall`, `load`, `oMath2Latex`, `parse`  


# Function Documentation: load

## Description
The `load` function parses an XML document from a given input stream and yields LaTeX representations of mathematical expressions found within the document. The function specifically looks for elements in the XML that correspond to the `oMath` tag within a specified namespace.

## Parameters
- `stream`: 
  - **Type**: `file-like object`
  - **Constraints**: The object must support the file interface, allowing it to be read by the `ET.parse()` method.
  - **Usage**: This parameter is passed directly to the `ET.parse()` function to create an XML tree structure from the input stream.

## Return Value
- **Type**: `generator`
- **Contents**: The generator yields LaTeX strings, each representing a mathematical expression extracted from the `oMath` elements found in the parsed XML document.

## Dependencies
- The function relies on the following external modules:
  - `xml.etree.ElementTree` (imported as `ET`): Used for parsing the XML document.
  - A function named `oMath2Latex`: This function is called to convert each `oMath` element into its LaTeX representation. The implementation of `oMath2Latex` is not provided in the code snippet.

## Usage Example
```python
import xml.etree.ElementTree as ET

# Assuming oMath2Latex is defined elsewhere
def oMath2Latex(omath):
    # Implementation of conversion from oMath to LaTeX
    pass

# Example XML stream
xml_stream = open('math_expressions.xml', 'r')

# Load and process the XML stream
for latex in load(xml_stream):
    print(latex)

xml_stream.close()
```

---
## `load_string`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:49`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L49-L54)

**Dependencies:** `findall`, `fromstring`, `load_string`, `oMath2Latex`  


# Function Documentation: load_string

## Description
The `load_string` function parses an XML string and yields LaTeX representations of mathematical expressions contained within the XML. It specifically looks for elements named `oMath` within the XML structure and converts each found element to its LaTeX equivalent using the `oMath2Latex` function.

## Parameters
- `string` (str): 
  - The input parameter is expected to be a string that contains XML data.
  - The string must be well-formed XML; otherwise, an exception may be raised during parsing.

## Return Value
- The function returns a generator that yields values produced by the `oMath2Latex` function.
- Each yielded value represents the LaTeX conversion of an `oMath` element found in the input XML string.

## Dependencies
- The function relies on the following external components:
  - `ET`: This refers to the `xml.etree.ElementTree` module, which is used for parsing the XML string.
  - `OMML_NS`: A namespace variable (not defined in the provided code) that is expected to be a string representing the XML namespace for the `oMath` elements.
  - `oMath2Latex`: A function (not defined in the provided code) that takes an XML element and converts it to a LaTeX string.

## Usage Example
```python
xml_string = '<root xmlns="http://www.w3.org/2000/svg"><oMath>...</oMath></root>'
for latex in load_string(xml_string):
    print(latex)
``` 

In this example, `xml_string` is a string containing XML data. The `load_string` function is called with this string, and it iterates over the LaTeX representations of each `oMath` element found in the XML.

---
## `escape_latex`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:55`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L55-L67)

**Dependencies:** `and`, `append`, `escape_latex`, `join`, `replace`  


# Function Documentation: escape_latex

## Description
The `escape_latex` function processes a string to escape specific characters that are used in LaTeX formatting. It replaces certain characters with their escaped versions by prefixing them with a backslash (`\`). The function ensures that backslashes are handled correctly and that characters are only escaped when they are not preceded by another backslash.

## Parameters
- `strs` (str): 
  - A string that may contain characters requiring escaping for LaTeX.
  - The function replaces double backslashes (`\\`) with a single backslash (`\`) before processing the string.

## Return Value
- Returns a string:
  - The output string contains the original characters from `strs`, with specific characters escaped by prefixing them with a backslash. The specific characters to be escaped are defined in the `CHARS` variable, and the output is constructed by joining the processed characters with a separator defined by the `BLANK` variable.

## Dependencies
- The function relies on the following external variables:
  - `CHARS`: A collection of characters that need to be escaped in LaTeX. This variable must be defined in the scope where the function is used.
  - `BACKSLASH`: A string representing a backslash (`\`). This variable must also be defined in the scope where the function is used.
  - `BLANK`: A string used as a separator when joining the processed characters. This variable must be defined in the scope where the function is used.

## Usage Example
```python
CHARS = {'#', '$', '%', '&', '_', '{', '}', '~', '^'}
BACKSLASH = '\\'
BLANK = ''

escaped_string = escape_latex("This is a test string with special characters: # $ % & _ { } ~ ^")
print(escaped_string)
```

---
## `get_val`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:68`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L68-L74)

**Dependencies:** `get`, `get_val`  


# Function Documentation: get_val

## Description
The `get_val` function retrieves a value associated with a specified key from a store. If the key is not found in the store, it returns the key itself. If the key is `None`, it returns a default value if provided.

## Parameters

- `key` (any type): 
  - This parameter is used to specify the key for which the value is to be retrieved from the store. 
  - If `key` is `None`, the function will return the `default` value.
  
- `default` (any type, optional): 
  - This parameter specifies the value to return if `key` is `None`.
  - The default value is `None` if not provided.

- `store` (dict, optional): 
  - This parameter represents a dictionary-like object from which to retrieve the value associated with `key`.
  - The default value is `CHR`, which must be defined elsewhere in the code.
  - If `store` is falsy (e.g., `None` or an empty dictionary), the function will return the `key`.

## Return Value
- The function returns:
  - The value associated with `key` from `store` if `key` is not `None` and `store` is truthy.
  - The `key` itself if `key` is not `None` and `store` is falsy.
  - The `default` value if `key` is `None`.

## Dependencies
- The function uses a variable `CHR`, which must be defined in the scope where the function is called. No external modules, APIs, or services are explicitly called within the function.

## Usage Example
```python
result = get_val('example_key', default='default_value', store={'example_key': 'example_value'})
# result will be 'example_value'

result = get_val(None, default='default_value')
# result will be 'default_value'

result = get_val('non_existent_key', store={})
# result will be 'non_existent_key'
```

---
## `Tag2Method`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:75`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L75-L126)

**Nested Functions:** `call_method`, `process_children_list`, `process_children_dict`, `process_children`, `process_unknow`  
**Dependencies:** `Tag2Method`, `and`, `call_method`, `dict`, `getmethod`, `isinstance`, `join`, `list`, `method`, `process_children`, `process_children_dict`, `process_children_list`, `process_unknow`, `replace`, `str` *(+1 more)*  


# Tag2Method Class Documentation

## Overview
The `Tag2Method` class provides methods for processing XML-like elements (referred to as `elm`) and invoking associated methods based on their tags. It includes functionality to process child elements and return results in various formats.

## Methods

### call_method(elm, stag=None)
- **Parameters**:
  - `elm` (Element): An XML-like element whose tag will be processed.
  - `stag` (str, optional): A string representing the tag name without the namespace. If not provided, it is derived from `elm.tag` by removing the `OMML_NS` namespace.
- **Returns**: 
  - Calls a method associated with the tag `stag` if it exists in `self.tag2meth`. Returns the result of that method call, or `None` if no method is found.

### process_children_list(elm, include=None)
- **Parameters**:
  - `elm` (Element): An XML-like element whose children will be processed.
  - `include` (set of str, optional): A set of tag names that should be included in the processing. If provided, only tags in this set will be processed.
- **Returns**: 
  - An iterable of tuples, each containing:
    - `stag` (str): The tag name of the child element without the namespace.
    - `t`: The result of calling the associated method or the result of `process_unknow`.
    - `_e` (Element): The child element itself.
  
### process_children_dict(elm, include=None)
- **Parameters**:
  - `elm` (Element): An XML-like element whose children will be processed.
  - `include` (set of str, optional): A set of tag names that should be included in the processing.
- **Returns**: 
  - A dictionary where keys are tag names (without the namespace) and values are the results of processing those tags.

### process_children(elm, include=None)
- **Parameters**:
  - `elm` (Element): An XML-like element whose children will be processed.
  - `include` (set of str, optional): A set of tag names that should be included in the processing.
- **Returns**: 
  - A string that concatenates the results of processing child elements. If a result is an instance of `Tag2Method`, it is converted to a string.

### process_unknow(elm, stag)
- **Parameters**:
  - `elm` (Element): An XML-like element that could not be processed by a known method.
  - `stag` (str): The tag name of the element that could not be processed.
- **Returns**: 
  - Always returns `None`.

## Dependencies
- The class relies on a variable `OMML_NS` which is expected to be defined in the scope where this class is used. This variable is used to remove the namespace from the tags of the elements.
- The class uses a dictionary `self.tag2meth` which is expected to map tag names to corresponding methods.

## Usage Example
```python
tag2method_instance = Tag2Method()
result_list = tag2method_instance.process_children_list(some_element, include={'tag1', 'tag2'})
result_dict = tag2method_instance.process_children_dict(some_element, include={'tag1', 'tag2'})
result_string = tag2method_instance.process_children(some_element, include={'tag1', 'tag2'})
```

---
## `Pr`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:127`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L127-L169)

**Nested Functions:** `__init__`, `__str__`, `__unicode__`, `__getattr__`, `do_brk`, `do_common`  
**Dependencies:** `Pr`, `__getattr__`, `__init__`, `__str__`, `__unicode__`, `do_brk`, `do_common`, `format`, `get`, `process_children`, `replace`  


# Documentation for the `Pr` Class

## Overview
The `Pr` class is a subclass of `Tag2Method` that processes XML-like elements and extracts specific attributes into a dictionary. It provides methods to handle specific tags and their associated values.

## Constructor

### `__init__(self, elm)`
- **Parameter**: 
  - `elm`: An object representing an XML element. The type is expected to be compatible with XML element structures.
- **Usage**: The constructor initializes the `__innerdict` attribute as an empty dictionary and processes the children of the provided `elm` to populate the `text` attribute.

## Methods

### `__str__(self)`
- **Return Type**: `str`
- **Description**: Returns the string representation of the `Pr` object, which is the value of the `text` attribute.

### `__unicode__(self)`
- **Return Type**: `str`
- **Description**: Returns the Unicode string representation of the `Pr` object by calling the `__str__` method.

### `__getattr__(self, name)`
- **Parameter**: 
  - `name`: A string representing the name of the attribute to retrieve.
- **Return Type**: `Any`
- **Description**: Returns the value associated with `name` from the `__innerdict` dictionary. If the attribute is not found, it returns `None`.

### `do_brk(self, elm)`
- **Parameter**: 
  - `elm`: An object representing an XML element. The type is expected to be compatible with XML element structures.
- **Return Type**: `Any`
- **Description**: Sets the `brk` key in the `__innerdict` to the value of `BRK` and returns `BRK`.

### `do_common(self, elm)`
- **Parameter**: 
  - `elm`: An object representing an XML element. The type is expected to be compatible with XML element structures.
- **Return Type**: `None`
- **Description**: Extracts the tag name from `elm`, checks if it is in the `__val_tags` tuple, retrieves the value of the attribute formatted as `{OMML_NS}val`, and stores it in the `__innerdict` under the tag name.

## Class Attributes
- `text`: A string that holds the processed text from the XML element's children.
- `__val_tags`: A tuple containing the valid tag names: `("chr", "pos", "begChr", "endChr", "type")`.
- `__innerdict`: A private dictionary used to store extracted values from the XML element.

## Instance Attributes
- `tag2meth`: A dictionary mapping tag names to their corresponding methods for processing.

## Dependencies
- The class relies on the `Tag2Method` superclass.
- It uses `OMML_NS`, which should be defined elsewhere in the codebase, to format attribute names.

## Usage Example
```python
# Assuming `elm` is an XML element object compatible with the expected structure
pr_instance = Pr(elm)
print(pr_instance)  # Outputs the processed text
value = pr_instance.chr  # Accesses the 'chr' attribute from __innerdict
```

---
## `oMath2Latex`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:170`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L170-L401)

**Nested Functions:** `__init__`, `__str__`, `__unicode__`, `process_unknow`, `latex`, `do_acc`, `do_bar`, `do_d`, `do_spre`, `do_sub`, `do_sup`, `do_f`, `do_func`, `do_fname`, `do_groupchr`, `do_rad`, `do_eqarr`, `do_limlow`, `do_limupp`, `do_lim`, `do_m`, `do_mr`, `do_nary`, `do_r`  
**Dependencies:** `NotImplementedError`, `Pr`, `__init__`, `__str__`, `__unicode__`, `append`, `do_acc`, `do_bar`, `do_d`, `do_eqarr`, `do_f`, `do_fname`, `do_func`, `do_groupchr`, `do_lim` *(+27 more)*  


# oMath2Latex Class Documentation

## Overview
The `oMath2Latex` class is designed to convert oMath elements from the Office Math Markup Language (OMML) into LaTeX format. It inherits from the `Tag2Method` class and utilizes a dictionary (`_t_dict`) to map tags to LaTeX representations.

## Constructor
### `__init__(self, element)`
- **Parameters**:
  - `element`: An object representing an oMath element. The type is not explicitly defined but is expected to be compatible with the methods used within the class.
- **Usage**: Initializes the instance and processes the children of the provided `element` to generate LaTeX output, stored in the `_latex` attribute.

## Properties
### `latex`
- **Type**: `str`
- **Description**: Returns the LaTeX representation generated during initialization.

## Methods
### `process_unknow(self, elm, stag)`
- **Parameters**:
  - `elm`: An element to process.
  - `stag`: A string representing the tag name.
- **Returns**: 
  - Processes the element based on the tag. If the tag is in `__direct_tags`, it processes children. If the tag ends with "Pr", it calls `Pr(elm)`. Otherwise, it returns `None`.

### `do_acc(self, elm)`
- **Parameters**:
  - `elm`: An element representing an accent.
- **Returns**: A string formatted according to the accent properties and the child element.

### `do_bar(self, elm)`
- **Parameters**:
  - `elm`: An element representing a bar.
- **Returns**: A string formatted with the bar properties and the child element.

### `do_d(self, elm)`
- **Parameters**:
  - `elm`: An element representing a delimiter.
- **Returns**: A string formatted with delimiter properties and the child element.

### `do_sub(self, elm)`
- **Parameters**:
  - `elm`: An element representing a subscript.
- **Returns**: A string formatted as a subscript.

### `do_sup(self, elm)`
- **Parameters**:
  - `elm`: An element representing a superscript.
- **Returns**: A string formatted as a superscript.

### `do_f(self, elm)`
- **Parameters**:
  - `elm`: An element representing a fraction.
- **Returns**: A string formatted as a fraction.

### `do_func(self, elm)`
- **Parameters**:
  - `elm`: An element representing a function application.
- **Returns**: A string representing the function name with its arguments.

### `do_fname(self, elm)`
- **Parameters**:
  - `elm`: An element representing a function name.
- **Returns**: A string representing the function name.

### `do_groupchr(self, elm)`
- **Parameters**:
  - `elm`: An element representing a group character.
- **Returns**: A string formatted with group character properties and the child element.

### `do_rad(self, elm)`
- **Parameters**:
  - `elm`: An element representing a radical.
- **Returns**: A string formatted as a radical, optionally including a degree.

### `do_eqarr(self, elm)`
- **Parameters**:
  - `elm`: An element representing an array.
- **Returns**: A string formatted as an array.

### `do_limlow(self, elm)`
- **Parameters**:
  - `elm`: An element representing a lower limit.
- **Returns**: A string formatted as a lower limit.

### `do_limupp(self, elm)`
- **Parameters**:
  - `elm`: An element representing an upper limit.
- **Returns**: A string formatted as an upper limit.

### `do_lim(self, elm)`
- **Parameters**:
  - `elm`: An element representing a limit.
- **Returns**: A string representing the limit.

### `do_m(self, elm)`
- **Parameters**:
  - `elm`: An element representing a matrix.
- **Returns**: A string formatted as a matrix.

### `do_mr(self, elm)`
- **Parameters**:
  - `elm`: An element representing a single row of a matrix.
- **Returns**: A string formatted as a matrix row.

### `do_nary(self, elm)`
- **Parameters**:
  - `elm`: An element representing an n-ary operation.
- **Returns**: A string formatted as an n-ary operation.

### `do_r(self, elm)`
- **Parameters**:
  - `elm`: An element representing a text node.
- **Returns**: A string containing the text converted to LaTeX symbols.

## Dependencies
- The class references several external functions and constants, including:
  - `get_val`
  - `escape_latex`
  - Constants such as `CHR_DEFAULT`, `POS_DEFAULT`, `D_DEFAULT`, `F_DEFAULT`, `FUNC`, `LIM_FUNC`, `LIM_UPP`, `M`, `ALN`, `BRK`, `BLANK`, and others.

## Usage Example
```python
element = ...  # An instance of an oMath element
latex_converter = oMath2Latex(element)
latex_output = str(latex_converter)
print(latex_output)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
