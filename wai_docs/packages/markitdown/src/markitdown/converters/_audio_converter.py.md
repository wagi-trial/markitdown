# packages/markitdown/src/markitdown/converters/_audio_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_audio_converter.py",
  "file_hash": "02f266e6fb689bcdcb261f9314e2b15cd5f74a735accc93ff69b64ad8c99e975",
  "last_updated": "2025-12-23T15:48:38.972150+00:00",
  "functions": {
    "AudioConverter": {
      "hash": "5f06a6d29b1348aef94a061e1fb1fa5b9eff97376e6199247033161778400911",
      "lines": "23-102",
      "last_updated": "2025-12-23T15:48:38.972077+00:00"
    }
  }
}
```

</details>



The Python file `_audio_converter.py` implements the `AudioConverter` class, which is responsible for converting audio files into markdown format. This conversion includes the extraction of metadata from audio files, provided that the `exiftool` dependency is installed, and the transcription of audio content, contingent on the availability of the `speech_recognition` library. The class defines methods to check if a given audio file is accepted based on its MIME type or file extension and to perform the conversion operation itself.

The main class defined in this file is `AudioConverter`, which inherits from `DocumentConverter`. It includes two primary methods: `accepts` and `convert`. The `accepts` method verifies if the audio file's MIME type or extension matches predefined accepted formats, while the `convert` method extracts metadata using the `exiftool_metadata` function and transcribes audio using the `transcribe_audio` function. The resulting markdown content is structured to include both metadata and the audio transcript, if available.

The file explicitly imports several modules, including `exiftool_metadata` from `_exiftool`, `transcribe_audio` from `_transcribe_audio`, and various components from the parent module, such as `DocumentConverter`, `DocumentConverterResult`, `StreamInfo`, and `MissingDependencyException`. The code manipulates types such as `BinaryIO` for file streams and `Any` for additional options, and it utilizes the `DocumentConverterResult` data structure to return the final markdown output. The accepted MIME types and file extensions are defined as lists, which are used to validate input files.

## Functions and Classes

## `AudioConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_audio_converter.py:23`](/packages/markitdown/src/markitdown/converters/_audio_converter.py#L23-L102)

# AudioConverter Class Documentation

## Overview
The `AudioConverter` class is a subclass of `DocumentConverter` that converts audio files into markdown format. It extracts metadata from audio files using `exiftool` if it is installed and performs speech transcription using the `speech_recognition` library if available.

## Method: accepts

### Description
The `accepts` method checks whether the provided audio file can be processed by the converter based on its MIME type and file extension.

### Parameters
- `file_stream` (BinaryIO): A binary stream of the audio file to be checked.
- `stream_info` (StreamInfo): An object containing information about the audio stream, including:
  - `mimetype` (str): The MIME type of the audio file.
  - `extension` (str): The file extension of the audio file.
- `**kwargs` (Any): Additional options that can be passed to the converter.

### Returns
- `bool`: Returns `True` if the file extension or MIME type is accepted; otherwise, returns `False`.

## Method: convert

### Description
The `convert` method processes the audio file, extracting metadata and transcribing the audio content into markdown format.

### Parameters
- `file_stream` (BinaryIO): A binary stream of the audio file to be converted.
- `stream_info` (StreamInfo): An object containing information about the audio stream, including:
  - `mimetype` (str): The MIME type of the audio file.
  - `extension` (str): The file extension of the audio file.
- `**kwargs` (Any): Additional options that can be passed to the converter, specifically for the `exiftool_path`.

### Returns
- `DocumentConverterResult`: An object containing the converted markdown content. The `markdown` attribute of this object holds the generated markdown string.

## Dependencies
- `exiftool`: Required for extracting metadata from audio files.
- `speech_recognition`: Required for transcribing audio content.
- `DocumentConverterResult`: A class that encapsulates the result of the conversion process.

## Usage Example
```python
audio_converter = AudioConverter()
file_stream = open('example.mp3', 'rb')
stream_info = StreamInfo(mimetype='audio/mpeg', extension='.mp3')

if audio_converter.accepts(file_stream, stream_info):
    result = audio_converter.convert(file_stream, stream_info, exiftool_path='/path/to/exiftool')
    print(result.markdown)
```

This example demonstrates how to create an instance of `AudioConverter`, check if a given audio file can be accepted, and convert it to markdown format, printing the resulting markdown content.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
