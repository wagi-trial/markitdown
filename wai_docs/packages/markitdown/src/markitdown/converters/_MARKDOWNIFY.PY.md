# packages/markitdown/src/markitdown/converters/_markdownify.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_markdownify.py",
  "file_hash": "52a5a560169fab0ca1781e2a21443e81c430367f1f1de4077a401ac45c8defac",
  "last_updated": "2026-01-04T17:21:18.842277+00:00",
  "functions": {
    "_CustomMarkdownify": {
      "hash": "afd3e2b6cd239cd6e0d7ef4d610ba8c62f4732d55ef50739432ac5cc28b4eef1",
      "lines": "8-127",
      "last_updated": "2026-01-04T17:21:18.842221+00:00"
    }
  }
}
```

</details>



The file `packages/markitdown/src/markitdown/converters/_markdownify.py` implements a custom Markdown converter class named `_CustomMarkdownify`, which extends the functionality of the `markdownify.MarkdownConverter`. This class modifies the default behavior of the Markdown conversion process by altering heading styles, removing JavaScript hyperlinks, truncating images with large data URIs, and ensuring that URIs are properly escaped to avoid conflicts with Markdown syntax.

The `_CustomMarkdownify` class includes several methods, each with specific responsibilities:
- `__init__(self, **options: Any)`: Initializes the converter with options for heading style and data URI handling.
- `convert_hn(self, n: int, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`: Converts heading elements, ensuring that they start on a new line if not inline.
- `convert_a(self, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs)`: Converts anchor elements, removing JavaScript links and escaping URIs.
- `convert_img(self, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`: Converts image elements, removing data URIs unless specified to keep them.
- `convert_input(self, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`: Converts input elements, specifically checkboxes, to Markdown syntax.
- `convert_soup(self, soup: Any) -> str`: Calls the parent class's method to convert a BeautifulSoup object.

The code imports several modules, including `re`, `markdownify`, `Any`, `Optional` from `typing`, and functions from `urllib.parse` such as `quote`, `unquote`, `urlparse`, and `urlunparse`. These dependencies facilitate regular expression operations, Markdown conversion, and URL handling. The file manipulates data structures such as HTML elements represented by `el` and utilizes attributes like `href`, `src`, and `alt` to perform conversions. The methods also handle string data types for text and titles, ensuring proper formatting in the resulting Markdown output.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `_CustomMarkdownify`

**Nested Functions:**
- `__init__`
- `convert_hn`
- `convert_a`
- `convert_img`
- `convert_input`
- `convert_soup`

<details>
<summary><strong>Calls/Dependencies</strong> (22 unique functions)</summary>

- `_CustomMarkdownify`
- `__init__`
- `_replace`
- `chomp`
- `convert_a`
- `convert_hn`
- `convert_img`
- `convert_input`
- `convert_soup`
- `find_parent`
- `get`
- `has_attr`
- `lower`
- `quote`
- `replace`
- `search`
- `split`
- `startswith`
- `super`
- `unquote`
- `urlparse`
- `urlunparse`

</details>

</details>



## Functions and Classes

## `_CustomMarkdownify`

**Location:** [`packages/markitdown/src/markitdown/converters/_markdownify.py:8`](/packages/markitdown/src/markitdown/converters/_markdownify.py#L8-L127)

**Nested Functions:** `__init__`, `convert_hn`, `convert_a`, `convert_img`, `convert_input`, `convert_soup`  
**Dependencies:** `_CustomMarkdownify`, `__init__`, `_replace`, `chomp`, `convert_a`, `convert_hn`, `convert_img`, `convert_input`, `convert_soup`, `find_parent`, `get`, `has_attr`, `lower`, `quote`, `replace` *(+7 more)*  


# Documentation for _CustomMarkdownify Class

## Overview
The `_CustomMarkdownify` class is a custom implementation of the `MarkdownConverter` from the `markdownify` library. It modifies the behavior of the markdown conversion process with specific alterations to handle headings, hyperlinks, images, and input elements.

## Dependencies
- `markdownify`: The base class `MarkdownConverter` is inherited from this library.
- `re`: Used for regular expression operations.
- `urlparse` and `urlunparse`: Used for parsing and constructing URLs.
- `quote` and `unquote`: Used for URL encoding and decoding.

## Constructor
### `__init__(self, **options: Any)`
Initializes the `_CustomMarkdownify` instance.

#### Parameters
- `**options`: A variable-length keyword argument dictionary.
  - `heading_style`: Optional; specifies the style of headings. Defaults to `markdownify.ATX`.
  - `keep_data_uris`: Optional; a boolean that determines whether to keep data URIs. Defaults to `False`.

## Methods

### `convert_hn(self, n: int, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`
Converts heading elements into Markdown format.

#### Parameters
- `n` (int): The level of the heading (e.g., 1 for `#`, 2 for `##`).
- `el` (Any): The element being converted.
- `text` (str): The text content of the heading.
- `convert_as_inline` (Optional[bool]): If `True`, converts the heading inline. Defaults to `False`.
- `**kwargs`: Additional keyword arguments.

#### Returns
- `str`: The Markdown representation of the heading, prefixed with a newline if `convert_as_inline` is `False`.

### `convert_a(self, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`
Converts anchor (`<a>`) elements into Markdown format, removing JavaScript links and escaping URIs.

#### Parameters
- `el` (Any): The anchor element being converted.
- `text` (str): The text content of the anchor.
- `convert_as_inline` (Optional[bool]): If `True`, converts the anchor inline. Defaults to `False`.
- `**kwargs`: Additional keyword arguments.

#### Returns
- `str`: The Markdown representation of the anchor. If the link is a JavaScript link or has an unsupported scheme, it returns the text without a link.

### `convert_img(self, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`
Converts image (`<img>`) elements into Markdown format, removing data URIs.

#### Parameters
- `el` (Any): The image element being converted.
- `text` (str): The text content associated with the image.
- `convert_as_inline` (Optional[bool]): If `True`, converts the image inline. Defaults to `False`.
- `**kwargs`: Additional keyword arguments.

#### Returns
- `str`: The Markdown representation of the image. If the source is a data URI and `keep_data_uris` is `False`, it truncates the URI.

### `convert_input(self, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`
Converts input elements, specifically checkboxes, into Markdown format.

#### Parameters
- `el` (Any): The input element being converted.
- `text` (str): The text content associated with the input.
- `convert_as_inline` (Optional[bool]): If `True`, converts the input inline. Defaults to `False`.
- `**kwargs`: Additional keyword arguments.

#### Returns
- `str`: The Markdown representation of the checkbox. Returns `[x]` if checked, `[ ]` if not.

### `convert_soup(self, soup: Any) -> str`
Converts a BeautifulSoup object into Markdown format.

#### Parameters
- `soup` (Any): The BeautifulSoup object to be converted.

#### Returns
- `str`: The Markdown representation of the BeautifulSoup object.

## Usage Example
```python
custom_markdown = _CustomMarkdownify(heading_style='ATX', keep_data_uris=False)
markdown_output = custom_markdown.convert_hn(1, el, "Heading Text")
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
