# packages/markitdown/src/markitdown/converters/_youtube_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_youtube_converter.py",
  "file_hash": "e58680df90de1dc04e3b92881ac9773b260b50a76f8f522dbc8e9c7a44cef478",
  "last_updated": "2026-01-04T17:23:00.401462+00:00",
  "functions": {
    "YouTubeConverter": {
      "hash": "5bb54bdc7cdb020f2fbf456c41834e8b4a210bb63ac14fd883d4e4a35bb34f3c",
      "lines": "37-239",
      "last_updated": "2026-01-04T17:23:00.401401+00:00"
    }
  }
}
```

</details>



The Python file `_youtube_converter.py` implements the `YouTubeConverter` class, which is responsible for converting YouTube video information into a structured markdown format. The class focuses on extracting the video title, description, and transcript from HTML content sourced from YouTube. It includes methods to validate the input stream and to perform the conversion process, which involves parsing HTML, extracting metadata, and optionally fetching video transcripts.

The `YouTubeConverter` class contains the following key methods: 
- `accepts`: Validates whether the input stream is from a YouTube URL and checks if the MIME type and file extension are acceptable. 
- `convert`: Parses the HTML content, extracts relevant metadata (such as title, description, and statistics), and constructs a markdown representation of the video information. It also attempts to fetch the video transcript using the `YouTubeTranscriptApi` if available.
- `_get`: A utility method used to retrieve specific metadata keys from the extracted metadata dictionary.

The file imports several modules, including `json`, `time`, `re`, `bs4` (BeautifulSoup), and `urllib.parse`. It also conditionally imports the `YouTubeTranscriptApi` from the `youtube_transcript_api` package, which is used for fetching video transcripts. The code defines and manipulates data structures such as dictionaries for metadata and employs types like `BinaryIO`, `Dict`, and `Any` from the `typing` module. The class also utilizes the `DocumentConverter` and `DocumentConverterResult` types from the parent module, indicating its role within a larger document conversion framework.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `YouTubeConverter`

**Nested Functions:**
- `accepts`
- `convert`
- `_get`
- `_findKey`
- `_retry_operation`

<details>
<summary><strong>Calls/Dependencies</strong> (35 unique functions)</summary>

- `BeautifulSoup`
- `DocumentConverterResult`
- `Exception`
- `YouTubeConverter`
- `YouTubeTranscriptApi`
- `_findKey`
- `_get`
- `_retry_operation`
- `accepts`
- `append`
- `convert`
- `else`
- `fetch`
- `find_transcript`
- `get`
- `group`
- `isinstance`
- `items`
- `join`
- `len`
- `list`
- `loads`
- `lower`
- `operation`
- `parse_qs`
- `print`
- `replace`
- `search`
- `sleep`
- `soup`
- `startswith`
- `str`
- `translate`
- `unquote`
- `urlparse`

</details>

</details>



## Functions and Classes

## `YouTubeConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_youtube_converter.py:37`](/packages/markitdown/src/markitdown/converters/_youtube_converter.py#L37-L239)

**Nested Functions:** `accepts`, `convert`, `_get`, `_findKey`, `_retry_operation`  
**Dependencies:** `BeautifulSoup`, `DocumentConverterResult`, `Exception`, `YouTubeConverter`, `YouTubeTranscriptApi`, `_findKey`, `_get`, `_retry_operation`, `accepts`, `append`, `convert`, `else`, `fetch`, `find_transcript`, `get` *(+20 more)*  


# YouTubeConverter Documentation

## Class Overview
`YouTubeConverter` is a subclass of `DocumentConverter` designed to handle YouTube video content specifically. It focuses on extracting the video title, description, and transcript from HTML content sourced from YouTube.

## Method: accepts

### Description
The `accepts` method determines whether the provided file stream and stream information correspond to valid YouTube HTML content.

### Parameters
- `file_stream` (BinaryIO): A binary input stream representing the content to be processed.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `url` (str): The URL of the YouTube video.
  - `mimetype` (str): The MIME type of the content.
  - `extension` (str): The file extension of the content.
- `**kwargs` (Any): Additional options to pass to the converter.

### Returns
- `bool`: Returns `True` if the content is from YouTube and is of an accepted MIME type or file extension; otherwise, returns `False`.

## Method: convert

### Description
The `convert` method processes the provided file stream to extract relevant metadata and generate a formatted markdown representation of the YouTube video.

### Parameters
- `file_stream` (BinaryIO): A binary input stream containing the HTML content of the YouTube video.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `url` (str): The URL of the YouTube video.
  - `charset` (str): The character set of the content (optional).
- `**kwargs` (Any): Additional options to pass to the converter, including:
  - `youtube_transcript_languages` (List[str]): A list of languages for fetching the transcript.

### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): A markdown formatted string with the video title, metadata, description, and transcript.
  - `title` (str): The title of the YouTube video.

## Dependencies
- `bs4`: Used for parsing HTML content.
- `json`: Used for handling JSON data.
- `re`: Used for regular expression operations.
- `time`: Used for implementing delays during retry operations.
- `YouTubeTranscriptApi`: An external API used to fetch video transcripts.
- `StreamInfo`: A class that provides metadata about the stream.

## Usage Example
```python
converter = YouTubeConverter()
file_stream = open('youtube_video.html', 'rb')  # Example HTML file stream
stream_info = StreamInfo(url='https://www.youtube.com/watch?v=example_video_id', mimetype='text/html', extension='html')

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info, youtube_transcript_languages=['en'])
    print(result.markdown)
```

This example demonstrates how to instantiate the `YouTubeConverter`, check if it accepts a given HTML file stream, and convert it to markdown format if accepted.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
