# packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py",
  "file_hash": "82dc30e0c9cd672a324b6d0d1a5f44c4a823908593ee65406431f975b93d4297",
  "last_updated": "2025-12-23T15:47:56.883198+00:00",
  "functions": {
    "load": {
      "hash": "6d3316330d9820f633e9d518acfa526c30da3e8ffdc67126b7b50c482b386674",
      "lines": "43-48",
      "last_updated": "2025-12-23T15:47:23.293900+00:00"
    },
    "load_string": {
      "hash": "69a2e347f95e3d0639d927c1a67f8cdd24db0959f406fd56facc513bc9899184",
      "lines": "49-54",
      "last_updated": "2025-12-23T15:47:26.136294+00:00"
    },
    "escape_latex": {
      "hash": "11d0d27e7f02aadcc741dbfa19dcfb3e3e57c4048845ff0c92a2a4f89765ebf0",
      "lines": "55-67",
      "last_updated": "2025-12-23T15:47:28.871716+00:00"
    },
    "get_val": {
      "hash": "a9dd3689f472fbeddad24b9873b816785a4629feec27d05aaf57e6b0e4b2a4b0",
      "lines": "68-74",
      "last_updated": "2025-12-23T15:47:32.918328+00:00"
    },
    "Tag2Method": {
      "hash": "e123f03f9b7f903ba95cfc7e65e8ac923b1f8beff4dc47ca333d28bf36b23552",
      "lines": "75-126",
      "last_updated": "2025-12-23T15:47:38.415073+00:00"
    },
    "Pr": {
      "hash": "db73421ed920d8b699b29e0ee4744a775bf5377a3237be9ff81865072ae53b1a",
      "lines": "127-169",
      "last_updated": "2025-12-23T15:47:44.644044+00:00"
    },
    "oMath2Latex": {
      "hash": "ed203725c7094c3eb09c7f0d81a63ad3d82eebde8fea86b672eb9d6a34e5cc9f",
      "lines": "170-401",
      "last_updated": "2025-12-23T15:47:56.883124+00:00"
    }
  }
}
```

</details>



The `omml.py` file implements functionality for processing Office Math Markup Language (OMML) elements and converting them into LaTeX format. It provides operations to load OMML from both a stream and a string, escape LaTeX special characters, and extract values from OMML elements. The file defines classes that facilitate the conversion process, specifically handling various OMML tags and their corresponding LaTeX representations.

The main functions in this file include `load` and `load_string`, which parse OMML input and yield LaTeX representations of the `oMath` elements found. The `escape_latex` function is responsible for escaping special LaTeX characters in a given string. The `get_val` function retrieves values from a specified key, with an option to use a default value or a store dictionary. The `Tag2Method` class serves as a base class for processing OMML tags, while the `Pr` and `oMath2Latex` classes extend this functionality to handle specific OMML elements and convert them into LaTeX format.

The file imports the `ElementTree` module from the `defusedxml` package for safe XML parsing and utilizes a set of constants from the `latex_dict` module, which includes character mappings and formatting options. The data structures manipulated in this file include XML elements represented by the `ElementTree` library, dictionaries for storing tag values, and strings for LaTeX output. The classes defined in the file encapsulate the logic for processing OMML elements and converting them into a LaTeX-compatible format.

## Functions and Classes

## `load`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:43`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L43-L48)

# Function Documentation: load

## Description
The `load` function parses an XML document from a given input stream and yields LaTeX representations of mathematical objects found within the document. The function specifically looks for elements named `oMath` within the XML structure, which are expected to be in the namespace defined by `OMML_NS`. For each `oMath` element found, the function calls `oMath2Latex` to convert it to LaTeX format.

## Parameters
- `stream`: 
  - **Type**: `file-like object`
  - **Constraints**: The object must support the file interface (i.e., it should be readable and provide a stream of XML data).
  - **Usage**: This parameter is passed directly to the `ET.parse` function to read and parse the XML content.

## Return Value
- **Type**: Generator
- **Contents**: The generator yields LaTeX strings, each representing the conversion of an `oMath` element found in the XML document.

## Dependencies
- The function depends on the following external modules:
  - `xml.etree.ElementTree` (imported as `ET`): This module is used for parsing the XML document.
  - `oMath2Latex`: This function is called to convert `oMath` elements to LaTeX format. The implementation of `oMath2Latex` is not provided in the code snippet.

## Usage Example
```python
with open('math_document.xml', 'r') as file_stream:
    for latex in load(file_stream):
        print(latex)
``` 

In this example, the `load` function is called with a file stream that reads from `math_document.xml`. The function yields LaTeX representations of each `oMath` element found in the XML, which are then printed to the console.

---
## `load_string`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:49`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L49-L54)

# Function Documentation: load_string

## Description
The `load_string` function parses an XML string and yields LaTeX representations of mathematical objects found within the XML. The function specifically looks for elements tagged with the namespace `OMML_NS` and the local name `oMath`.

## Parameters
- `string` (str): 
  - The XML string to be parsed. 
  - It must be a well-formed XML string containing elements that match the specified namespace and local name.

## Return Value
- The function returns a generator that yields values produced by the `oMath2Latex` function for each `oMath` element found in the XML. 
- Each yielded value represents a LaTeX conversion of the corresponding `oMath` element.

## Dependencies
- The function relies on the following external components:
  - `ET` (ElementTree): This module is used to parse the XML string.
  - `OMML_NS`: A variable that defines the namespace used to locate `oMath` elements.
  - `oMath2Latex`: A function that converts `oMath` elements to their LaTeX representation.

## Usage Example
```python
xml_string = "<root xmlns='http://schemas.openxmlformats.org/officeDocument/2006/math'><oMath>...</oMath></root>"
for latex in load_string(xml_string):
    print(latex)
```

---
## `escape_latex`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:55`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L55-L67)

# Function Documentation: escape_latex

## Description
The `escape_latex` function processes a string to escape specific characters that are significant in LaTeX formatting. It replaces certain characters with their escaped versions by prefixing them with a backslash (`\`). The function also handles existing backslashes by replacing double backslashes (`\\`) with a single backslash (`\`).

## Parameters
- `strs` (str): 
  - A string that may contain characters that need to be escaped for LaTeX.
  - The function processes this string to escape characters defined in the `CHARS` constant.

## Return Value
- Returns a string:
  - The output string contains the original characters from `strs`, with specific characters escaped by prefixing them with a backslash, ensuring they are treated as literals in LaTeX.

## Dependencies
- The function relies on the following external constants:
  - `CHARS`: A collection of characters that need to be escaped in LaTeX.
  - `BACKSLASH`: A string representing a backslash (`\`).
  - `BLANK`: A string used to join the list of characters into a single string.

## Usage Example
```python
escaped_string = escape_latex("This is a test string with special characters: # $ % & _ { } ~ ^")
```

---
## `get_val`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:68`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L68-L74)

# Function Documentation: get_val

## Description
The `get_val` function retrieves a value based on a provided key. If the key is not `None`, it checks a specified store for the key's corresponding value. If the store is not provided or does not contain the key, it returns the key itself. If the key is `None`, it returns a default value.

## Parameters

- `key` (any type): 
  - This parameter is used to specify the key for which the value is to be retrieved. 
  - If `key` is `None`, the function will return the `default` value.

- `default` (any type, optional):
  - This parameter specifies the value to return if `key` is `None`.
  - The default value is `None`.

- `store` (dict-like, optional):
  - This parameter is expected to be a dictionary or an object that supports the `get` method.
  - The default value is `CHR`, which is assumed to be defined elsewhere in the code.
  - If `store` is provided and contains the `key`, the corresponding value from `store` is returned; otherwise, the `key` itself is returned.

## Return Value
The function returns:
- The value associated with `key` from `store` if `key` is not `None` and `store` contains `key`.
- The `key` itself if `key` is not `None` and `store` does not contain `key`.
- The `default` value if `key` is `None`.

## Dependencies
The function relies on the existence of a variable `CHR`, which must be defined in the scope where the function is called. There are no explicit imports or external module dependencies in the provided code.

## Usage Example
```python
result = get_val('example_key', default='default_value', store={'example_key': 'example_value'})
# result will be 'example_value'

result = get_val(None, default='default_value')
# result will be 'default_value'

result = get_val('non_existing_key', default='default_value', store={'example_key': 'example_value'})
# result will be 'non_existing_key'
```

---
## `Tag2Method`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:75`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L75-L126)

# Tag2Method Class Documentation

## Overview
The `Tag2Method` class provides methods for processing XML-like elements, specifically focusing on handling child elements based on their tags. It includes functionality to call specific methods associated with tags, process child elements into different formats, and handle unknown tags.

## Methods

### call_method
```python
def call_method(self, elm, stag=None)
```
- **Parameters**:
  - `elm` (Element): The element to process, expected to have a `tag` attribute.
  - `stag` (str, optional): A string representing the tag name without the namespace. If not provided, it is derived from `elm.tag` by removing the `OMML_NS` namespace.
  
- **Returns**:
  - The result of the method associated with the tag if it exists; otherwise, returns `None`.

### process_children_list
```python
def process_children_list(self, elm, include=None)
```
- **Parameters**:
  - `elm` (Element): The parent element whose children will be processed.
  - `include` (iterable, optional): A collection of tag names to include in processing. If provided, only tags in this collection will be processed.
  
- **Returns**:
  - An iterable of tuples, each containing:
    - `stag` (str): The tag name of the child element without the namespace.
    - `t`: The result of calling the method associated with the tag or the result of processing an unknown tag.
    - `_e` (Element): The child element itself.

### process_children_dict
```python
def process_children_dict(self, elm, include=None)
```
- **Parameters**:
  - `elm` (Element): The parent element whose children will be processed.
  - `include` (iterable, optional): A collection of tag names to include in processing.
  
- **Returns**:
  - A dictionary where keys are tag names (without the namespace) and values are the results of processing the corresponding child elements.

### process_children
```python
def process_children(self, elm, include=None)
```
- **Parameters**:
  - `elm` (Element): The parent element whose children will be processed.
  - `include` (iterable, optional): A collection of tag names to include in processing.
  
- **Returns**:
  - A string that concatenates the results of processing child elements.

### process_unknow
```python
def process_unknow(self, elm, stag)
```
- **Parameters**:
  - `elm` (Element): The unknown element to process.
  - `stag` (str): The tag name of the unknown element.
  
- **Returns**:
  - Always returns `None`.

## Dependencies
- The class references `OMML_NS`, which is expected to be a predefined constant representing a namespace string.
- The class expects that the elements processed have a `tag` attribute and can be iterated over as a list.

## Usage Example
```python
tag_processor = Tag2Method()
result_list = tag_processor.process_children_list(some_element, include=['tag1', 'tag2'])
result_dict = tag_processor.process_children_dict(some_element)
result_string = tag_processor.process_children(some_element)
```

---
## `Pr`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:127`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L127-L169)

# Documentation for the `Pr` Class

## Overview
The `Pr` class is a subclass of `Tag2Method` that processes XML-like elements and stores specific attributes in an internal dictionary. It provides methods to handle certain tags and their associated values.

## Constructor

### `__init__(self, elm)`
- **Parameters**:
  - `elm`: An object representing an XML element. The type is not explicitly defined but is expected to have a `tag` attribute and a `get` method for retrieving attributes.
- **Usage**: The constructor initializes an internal dictionary (`__innerdict`) and processes the children of the provided element (`elm`) to set the `text` attribute.

## Methods

### `__str__(self)`
- **Returns**: A string representation of the `Pr` object, which is the value of the `text` attribute.

### `__unicode__(self)`
- **Returns**: A Unicode string representation of the `Pr` object by calling the `__str__` method.

### `__getattr__(self, name)`
- **Parameters**:
  - `name`: A string representing the name of the attribute to retrieve.
- **Returns**: The value associated with `name` in the `__innerdict` dictionary, or `None` if the attribute does not exist.

### `do_brk(self, elm)`
- **Parameters**:
  - `elm`: An object representing an XML element. The type is not explicitly defined.
- **Returns**: The constant `BRK`, which is expected to be defined elsewhere in the code.

### `do_common(self, elm)`
- **Parameters**:
  - `elm`: An object representing an XML element. The type is not explicitly defined.
- **Returns**: `None`. This method processes the element's tag and retrieves a value associated with it, storing it in the `__innerdict` if the tag is one of the predefined valid tags.

## Attributes

### `text`
- A string that holds the processed text from the children of the provided element during initialization.

### `__val_tags`
- A tuple containing the valid tags: `("chr", "pos", "begChr", "endChr", "type")`.

### `__innerdict`
- A dictionary used to store attribute values associated with specific tags.

### `tag2meth`
- A dictionary mapping tag names to their corresponding methods for processing. The keys are tag names, and the values are method references.

## Dependencies
- The class depends on the `Tag2Method` superclass, which is not defined in the provided code.
- It uses the `OMML_NS` constant to construct attribute names for XML elements. This constant must be defined elsewhere in the code.
- The constant `BRK` is referenced in the `do_brk` method and must also be defined elsewhere.

## Usage Example
```python
elm = ...  # An XML element object with a tag and attributes
pr_instance = Pr(elm)
print(pr_instance)  # Outputs the processed text
chr_value = pr_instance.chr  # Accesses the 'chr' attribute from __innerdict
```

---
## `oMath2Latex`

**Location:** [`packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py:170`](/packages/markitdown/src/markitdown/converter_utils/docx/math/omml.py#L170-L401)

# oMath2Latex Class Documentation

## Overview
The `oMath2Latex` class is designed to convert oMath elements from the Office Math Markup Language (OMML) into LaTeX format. It extends the `Tag2Method` class and utilizes a mapping of tags to methods for processing various mathematical constructs.

## Constructor

### `__init__(self, element)`
- **Parameters**: 
  - `element`: An object representing an oMath element. The type is not explicitly defined in the code but is expected to be compatible with the methods that process children elements.
- **Usage**: Initializes the class by processing the children of the provided `element` and storing the resulting LaTeX string in the `_latex` attribute.

## Properties

### `latex`
- **Type**: `str`
- **Description**: Returns the LaTeX representation of the processed oMath element.

## Methods

### `process_unknow(self, elm, stag)`
- **Parameters**:
  - `elm`: An object representing an oMath element.
  - `stag`: A string representing the tag name of the element.
- **Returns**: 
  - `str` or `None`: Returns processed children if the tag is in `__direct_tags` or if it ends with "Pr". Returns `None` otherwise.

### `do_acc(self, elm)`
- **Parameters**: 
  - `elm`: An object representing an accent element.
- **Returns**: 
  - `str`: LaTeX string for the accent applied to the element.

### `do_bar(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a bar element.
- **Returns**: 
  - `str`: LaTeX string for the bar applied to the element.

### `do_d(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a delimiter element.
- **Returns**: 
  - `str`: LaTeX string for the delimiter.

### `do_sub(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a subscript element.
- **Returns**: 
  - `str`: LaTeX string for the subscript.

### `do_sup(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a superscript element.
- **Returns**: 
  - `str`: LaTeX string for the superscript.

### `do_f(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a fraction element.
- **Returns**: 
  - `str`: LaTeX string for the fraction.

### `do_func(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a function-apply element.
- **Returns**: 
  - `str`: LaTeX string for the function.

### `do_fname(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a function name element.
- **Returns**: 
  - `str`: LaTeX string for the function name.

### `do_groupchr(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a group character element.
- **Returns**: 
  - `str`: LaTeX string for the group character.

### `do_rad(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a radical element.
- **Returns**: 
  - `str`: LaTeX string for the radical.

### `do_eqarr(self, elm)`
- **Parameters**: 
  - `elm`: An object representing an array element.
- **Returns**: 
  - `str`: LaTeX string for the array.

### `do_limlow(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a lower-limit element.
- **Returns**: 
  - `str`: LaTeX string for the lower limit.

### `do_limupp(self, elm)`
- **Parameters**: 
  - `elm`: An object representing an upper-limit element.
- **Returns**: 
  - `str`: LaTeX string for the upper limit.

### `do_lim(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a limit element.
- **Returns**: 
  - `str`: LaTeX string for the limit.

### `do_m(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a matrix element.
- **Returns**: 
  - `str`: LaTeX string for the matrix.

### `do_mr(self, elm)`
- **Parameters**: 
  - `elm`: An object representing a matrix row element.
- **Returns**: 
  - `str`: LaTeX string for the matrix row.

### `do_nary(self, elm)`
- **Parameters**: 
  - `elm`: An object representing an n-ary element.
- **Returns**: 
  - `str`: LaTeX string for the n-ary operation.

### `do_r(self, elm)`
- **Parameters**: 
  - `elm`: An object representing an 'r' element.
- **Returns**: 
  - `str`: LaTeX string for the text from the 'r' element.

## External Dependencies
- The class relies on external functions and constants such as `get_val`, `escape_latex`, and various dictionaries (e.g., `T`, `CHR_DEFAULT`, `POS_DEFAULT`, `D_DEFAULT`, `F_DEFAULT`, `FUNC`, `LIM_FUNC`, `LIM_UPP`, `M`, `BRK`, `ALN`, `CHR_BO`, `FUNC_PLACE`, and `LIM_TO`). These are not defined within the provided code and must be available in the broader context where this class is used.

## Usage Example
```python
element = ...  # An instance of an oMath element
converter = oMath2Latex(element)
latex_output = str(converter)
print(latex_output)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
