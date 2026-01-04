# packages/markitdown/src/markitdown/converters/_audio_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_audio_converter.py",
  "file_hash": "02f266e6fb689bcdcb261f9314e2b15cd5f74a735accc93ff69b64ad8c99e975",
  "last_updated": "2026-01-04T17:19:03.541888+00:00",
  "functions": {
    "AudioConverter": {
      "hash": "5f06a6d29b1348aef94a061e1fb1fa5b9eff97376e6199247033161778400911",
      "lines": "23-102",
      "last_updated": "2026-01-04T17:19:03.541823+00:00"
    }
  }
}
```

</details>



The Python file `_audio_converter.py` implements an `AudioConverter` class that is responsible for converting audio files into markdown format. This conversion involves extracting metadata from the audio files and transcribing the audio content into text. The class checks for accepted audio file types based on their MIME types and file extensions before processing them.

The `AudioConverter` class contains two primary methods: `accepts` and `convert`. The `accepts` method verifies if a given file stream and its associated stream information (MIME type and file extension) are supported by checking against predefined lists of accepted MIME type prefixes and file extensions. The `convert` method performs the actual conversion, which includes extracting metadata using the `exiftool_metadata` function and transcribing the audio content using the `transcribe_audio` function. If the `exiftool` or `speech_recognition` dependencies are not available, the conversion will proceed without their respective functionalities.

The file explicitly imports several modules and functions, including `exiftool_metadata` from `_exiftool`, `transcribe_audio` from `_transcribe_audio`, and classes such as `DocumentConverter` and `DocumentConverterResult` from `_base_converter`. It also imports `StreamInfo` from `_stream_info` and `MissingDependencyException` from `_exceptions`. The data structures manipulated in this file include `BinaryIO` for file streams and `StreamInfo` for metadata about the audio files. The output of the conversion process is encapsulated in a `DocumentConverterResult` object, which contains the generated markdown content.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `AudioConverter`

**Nested Functions:**
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (12 unique functions)</summary>

- `AudioConverter`
- `DocumentConverterResult`
- `accepts`
- `convert`
- `exiftool_metadata`
- `get`
- `lower`
- `metadata`
- `startswith`
- `strip`
- `transcribe_audio`
- `transcription`

</details>

</details>



## Functions and Classes

## `AudioConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_audio_converter.py:23`](/packages/markitdown/src/markitdown/converters/_audio_converter.py#L23-L102)

**Nested Functions:** `accepts`, `convert`  
**Dependencies:** `AudioConverter`, `DocumentConverterResult`, `accepts`, `convert`, `exiftool_metadata`, `get`, `lower`, `metadata`, `startswith`, `strip`, `transcribe_audio`, `transcription`  


# AudioConverter Documentation

## Overview
`AudioConverter` is a subclass of `DocumentConverter` that converts audio files into markdown format. It extracts metadata from the audio files using `exiftool` (if installed) and performs speech transcription using the `speech_recognition` library (if installed).

## Method: accepts

### Description
The `accepts` method checks if the provided audio file stream and its associated stream information are acceptable for conversion based on file extension and MIME type.

### Parameters
- `file_stream` (BinaryIO): The binary stream of the audio file to be checked.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `mimetype` (str): The MIME type of the audio file.
  - `extension` (str): The file extension of the audio file.
- `**kwargs` (Any): Additional options that may be passed to the converter.

### Returns
- `bool`: Returns `True` if the file extension or MIME type is accepted based on predefined lists; otherwise, returns `False`.

## Method: convert

### Description
The `convert` method processes the audio file stream to extract metadata and transcribe audio content into markdown format.

### Parameters
- `file_stream` (BinaryIO): The binary stream of the audio file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `mimetype` (str): The MIME type of the audio file.
  - `extension` (str): The file extension of the audio file.
- `**kwargs` (Any): Additional options that may be passed to the converter, including:
  - `exiftool_path` (str): The file path to the `exiftool` executable.

### Returns
- `DocumentConverterResult`: An object containing the converted markdown content as follows:
  - `markdown` (str): A string containing the extracted metadata and audio transcript, formatted in markdown.

## Dependencies
- `exiftool`: Used for extracting metadata from audio files. The functionality is contingent on `exiftool` being installed.
- `speech_recognition`: Used for transcribing audio files. The functionality is contingent on this library being installed.
- `MissingDependencyException`: An exception that is caught if the transcription library is not available.

## Usage Example
```python
from io import BytesIO

# Create an instance of AudioConverter
audio_converter = AudioConverter()

# Prepare a binary stream and stream info
file_stream = BytesIO(b"audio data here")  # Replace with actual audio data
stream_info = StreamInfo(mimetype="audio/mpeg", extension=".mp3")

# Check if the converter accepts the file
if audio_converter.accepts(file_stream, stream_info):
    result = audio_converter.convert(file_stream, stream_info, exiftool_path="/path/to/exiftool")
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
