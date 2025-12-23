# packages/markitdown/src/markitdown/converters/_markdownify.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_markdownify.py",
  "file_hash": "52a5a560169fab0ca1781e2a21443e81c430367f1f1de4077a401ac45c8defac",
  "last_updated": "2025-12-23T15:51:09.644024+00:00",
  "functions": {
    "_CustomMarkdownify": {
      "hash": "afd3e2b6cd239cd6e0d7ef4d610ba8c62f4732d55ef50739432ac5cc28b4eef1",
      "lines": "8-127",
      "last_updated": "2025-12-23T15:51:09.643910+00:00"
    }
  }
}
```

</details>



The file `packages/markitdown/src/markitdown/converters/_markdownify.py` implements a custom Markdown converter class named `_CustomMarkdownify`, which extends the `MarkdownConverter` from the `markdownify` library. This class modifies the behavior of the standard Markdown conversion process by altering heading styles, removing JavaScript hyperlinks, truncating large data URIs in images, and ensuring that URIs are properly escaped to avoid conflicts with Markdown syntax.

The main class in this file is `_CustomMarkdownify`, which includes several methods with specific responsibilities: 
- `__init__`: Initializes the converter with options for heading style and data URI handling.
- `convert_hn`: Converts heading elements while ensuring they start on a new line.
- `convert_a`: Converts anchor elements, removing JavaScript links and escaping URIs.
- `convert_img`: Converts image elements, removing data URIs unless specified to keep them.
- `convert_input`: Converts checkbox input elements to Markdown syntax.
- `convert_soup`: Converts a BeautifulSoup object to Markdown using the parent class's method.

The code explicitly imports modules such as `re`, `markdownify`, and `urllib.parse`, which are used for regular expression operations, Markdown conversion, and URL parsing and manipulation, respectively. The file interacts with data structures such as HTML elements represented by the `el` parameter in the conversion methods, which are expected to have attributes like `href`, `src`, `alt`, and `title`. The methods also handle strings for text content and Markdown formatting. The types used in the methods include `Any` and `Optional`, indicating flexibility in the types of arguments that can be passed.

## Functions and Classes

## `_CustomMarkdownify`

**Location:** [`packages/markitdown/src/markitdown/converters/_markdownify.py:8`](/packages/markitdown/src/markitdown/converters/_markdownify.py#L8-L127)

# Documentation for `_CustomMarkdownify`

## Class Overview
`_CustomMarkdownify` is a subclass of `markdownify.MarkdownConverter`. It customizes the behavior of the Markdown conversion process by altering heading styles, removing JavaScript hyperlinks, truncating images with large data URIs, and ensuring that URIs are properly escaped to avoid conflicts with Markdown syntax.

## Constructor
### `__init__(self, **options: Any)`
Initializes the `_CustomMarkdownify` instance with specific options.

#### Parameters
- `**options`: A variable-length argument dictionary that can contain the following keys:
  - `heading_style` (optional): Specifies the style of headings. Defaults to `markdownify.ATX` if not provided.
  - `keep_data_uris` (optional): A boolean that determines whether to keep data URIs. Defaults to `False`.

#### Return Value
None.

## Methods

### `convert_hn(self, n: int, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`
Converts heading elements to Markdown format.

#### Parameters
- `n`: An integer representing the heading level (e.g., 1 for H1, 2 for H2).
- `el`: An element object representing the heading element.
- `text`: A string containing the text of the heading.
- `convert_as_inline`: An optional boolean indicating whether to convert the heading as an inline element. Defaults to `False`.
- `**kwargs`: Additional keyword arguments.

#### Return Value
A string representing the Markdown formatted heading. If `convert_as_inline` is `False` and the text does not start with a newline, a newline is prepended.

### `convert_a(self, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`
Converts anchor (`<a>`) elements to Markdown format.

#### Parameters
- `el`: An element object representing the anchor element.
- `text`: A string containing the text of the link.
- `convert_as_inline`: An optional boolean indicating whether to convert the link as an inline element. Defaults to `False`.
- `**kwargs`: Additional keyword arguments.

#### Return Value
A string representing the Markdown formatted link. JavaScript links are removed, and URIs are escaped. If the link is not valid, the original text is returned.

### `convert_img(self, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`
Converts image (`<img>`) elements to Markdown format.

#### Parameters
- `el`: An element object representing the image element.
- `text`: A string containing the text associated with the image.
- `convert_as_inline`: An optional boolean indicating whether to convert the image as an inline element. Defaults to `False`.
- `**kwargs`: Additional keyword arguments.

#### Return Value
A string representing the Markdown formatted image. Data URIs are truncated if `keep_data_uris` is `False`.

### `convert_input(self, el: Any, text: str, convert_as_inline: Optional[bool] = False, **kwargs) -> str`
Converts input elements, specifically checkboxes, to Markdown format.

#### Parameters
- `el`: An element object representing the input element.
- `text`: A string containing the text associated with the input.
- `convert_as_inline`: An optional boolean indicating whether to convert the input as an inline element. Defaults to `False`.
- `**kwargs`: Additional keyword arguments.

#### Return Value
A string representing the Markdown formatted checkbox. Returns `[x]` if the checkbox is checked, otherwise returns `[ ]`.

### `convert_soup(self, soup: Any) -> str`
Converts a BeautifulSoup object to Markdown format.

#### Parameters
- `soup`: A BeautifulSoup object representing the HTML content to be converted.

#### Return Value
A string representing the Markdown formatted content.

## Dependencies
- `markdownify`: The base class `MarkdownConverter` is imported from this module.
- `re`: Used for regular expression operations.
- `urlparse`, `urlunparse`, `quote`, `unquote`: Functions from the `urllib.parse` module to handle URL parsing and manipulation.

## Usage Example
```python
custom_markdown = _CustomMarkdownify(heading_style='ATX', keep_data_uris=False)
markdown_output = custom_markdown.convert_hn(1, heading_element, "Sample Heading")
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
