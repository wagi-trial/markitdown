# packages/markitdown/src/markitdown/converters/_youtube_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_youtube_converter.py",
  "file_hash": "e58680df90de1dc04e3b92881ac9773b260b50a76f8f522dbc8e9c7a44cef478",
  "last_updated": "2025-12-23T15:53:03.107808+00:00",
  "functions": {
    "YouTubeConverter": {
      "hash": "5bb54bdc7cdb020f2fbf456c41834e8b4a210bb63ac14fd883d4e4a35bb34f3c",
      "lines": "37-239",
      "last_updated": "2025-12-23T15:53:03.107733+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_youtube_converter.py` implements the `YouTubeConverter` class, which is responsible for converting YouTube video HTML content into a structured Markdown format. The class focuses on extracting key metadata such as the video title, description, and transcript, if available. It utilizes the BeautifulSoup library to parse HTML content and extract relevant information from meta tags and scripts.

The main functions within the `YouTubeConverter` class include `accepts`, which checks if the input stream is a valid YouTube HTML document based on its URL, MIME type, and file extension; and `convert`, which processes the HTML content to extract metadata and format it into Markdown. The class also includes a private method `_get`, which retrieves specific metadata attributes from a dictionary. The converter optionally supports YouTube video transcripts through the `youtube_transcript_api`, which is conditionally imported based on its availability.

The file explicitly imports several modules, including `json`, `time`, `re`, `bs4` (BeautifulSoup), and `urllib.parse`. It also relies on the `DocumentConverter` and `DocumentConverterResult` classes from a parent module, as well as the `StreamInfo` class for handling stream metadata. The data structures manipulated within the file include dictionaries for metadata storage and lists for handling transcript languages, as well as the use of `BinaryIO` for file streams. The class defines the types of input parameters and return values using type hints, ensuring clarity in the expected data types throughout its methods.

## Functions and Classes

## `YouTubeConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_youtube_converter.py:37`](/packages/markitdown/src/markitdown/converters/_youtube_converter.py#L37-L239)

# YouTubeConverter Documentation

## Overview
`YouTubeConverter` is a subclass of `DocumentConverter` designed to handle YouTube video content specifically. It focuses on extracting the video title, description, and transcript from HTML content sourced from YouTube.

## Method: `accepts`

### Description
The `accepts` method determines whether the provided file stream and stream information correspond to a valid YouTube video URL and content type.

### Parameters
- `file_stream` (BinaryIO): A binary stream of the file content. This parameter is used to read the content type.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `url` (str): The URL of the YouTube video.
  - `mimetype` (str): The MIME type of the content.
  - `extension` (str): The file extension of the content.
- `**kwargs` (Any): Additional options to pass to the converter.

### Returns
- `bool`: Returns `True` if the URL is a valid YouTube video URL and the content type is acceptable; otherwise, returns `False`.

## Method: `convert`

### Description
The `convert` method processes the file stream to extract metadata and generate a formatted markdown representation of the YouTube video, including the title, metadata, description, and transcript.

### Parameters
- `file_stream` (BinaryIO): A binary stream of the file content, used for parsing the HTML.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `url` (str): The URL of the YouTube video.
  - `charset` (str, optional): The character set of the content.
- `**kwargs` (Any): Additional options to pass to the converter, including `youtube_transcript_languages`.

### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): A markdown formatted string representing the YouTube video details.
  - `title` (str): The title of the YouTube video.

## Dependencies
- `bs4`: Used for parsing HTML content.
- `json`: Used for handling JSON data.
- `re`: Used for regular expression operations.
- `time`: Used for implementing delays in retry operations.
- `YouTubeTranscriptApi`: An external API for fetching YouTube video transcripts.
- `StreamInfo`: An external class that provides metadata about the stream.

## Usage Example
```python
converter = YouTubeConverter()
file_stream = open("youtube_video.html", "rb")
stream_info = StreamInfo(url="https://www.youtube.com/watch?v=example_video_id", mimetype="text/html", extension="html")

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info, youtube_transcript_languages=["en"])
    print(result.markdown)
```

This example demonstrates how to create an instance of `YouTubeConverter`, check if a file stream corresponds to a YouTube video, and convert it to a markdown format.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
