# Speech Data Synthesis Pipeline

## Overview
This Jupyter notebook implements a comprehensive speech synthesis pipeline using XTTS v2 (Cross-lingual Text-to-Speech) technology for voice cloning and multilingual speech generation. The pipeline processes JSON-formatted scripts and generates high-quality synthetic speech with custom voice characteristics.

## Key Features
- **Voice Cloning**: Clone any voice using a reference audio sample
- **Multilingual Support**: Generate speech in multiple languages
- **Batch Processing**: Process multiple scripts efficiently
- **Text Processing**: Advanced text cleaning and chunking for optimal synthesis
- **Audio Concatenation**: Seamless merging of audio chunks with smooth transitions
- **GPU Acceleration**: Optimized for CUDA-enabled devices

## Technical Components

### 1. Text Processing (`TextProcessor` class)
- **Text Cleaning**: Normalizes whitespace, handles abbreviations, converts numbers to words
- **Sentence Splitting**: Intelligent sentence boundary detection
- **Text Chunking**: Splits long texts into manageable chunks with configurable overlap
- **Preprocessing**: Prepares text for optimal TTS synthesis

### 2. XTTS Pipeline (`XTTSPipeline` class)
- **Model Loading**: Loads pre-trained XTTS v2 model
- **Speaker Conditioning**: Processes reference voice for cloning
- **Chunk Synthesis**: Generates speech for individual text segments
- **Audio Concatenation**: Combines chunks with silence padding for natural flow

### 3. Configuration (`SpeechConfig` class)
Configurable parameters include:
- **Audio Quality**: Sample rate (default: 22050 Hz)
- **Synthesis Parameters**: Temperature, length penalty, repetition penalty
- **Processing Settings**: Chunk size, overlap words, parallel workers
- **Output Settings**: Directory path, file naming

## Input Format
The pipeline expects a JSON file with the following structure:
```json
{
  "script_id": {
    "text": "Text content to synthesize",
    "file": "output_filename.wav",
    "speaker_wav": "path/to/reference/voice.wav"
  }
}
```

## Usage Instructions

### Prerequisites
```bash
pip install TTS transformers==4.36.2
```

### Configuration
```python
config = SpeechConfig(
    speaker_wav_path="path/to/reference/voice.wav",
    language="en",
    output_dir="generated_speech",
    chunk_size=150,
    temperature=0.75
)
```

### Pipeline Execution
1. **Initialize Pipeline**: Create XTTSPipeline instance with configuration
2. **Load Model**: Automatically downloads and loads XTTS v2 model
3. **Process Scripts**: Batch process JSON scripts to generate audio files
4. **Output**: Generated WAV files saved to specified directory

### Processing Workflow
1. **JSON Conversion**: Converts list-format JSON to dictionary format if needed
2. **Text Processing**: Cleans and chunks input text
3. **Voice Conditioning**: Extracts speaker characteristics from reference audio
4. **Speech Synthesis**: Generates audio chunks using XTTS model
5. **Audio Assembly**: Concatenates chunks with smooth transitions
6. **File Output**: Saves final audio as WAV files

## Performance Considerations
- **Memory Management**: Implements CUDA cache clearing for GPU optimization
- **Chunk Size**: Configurable text chunks prevent memory overflow
- **Parallel Processing**: Optional multi-worker support for batch operations
- **Error Handling**: Robust error recovery for individual script failures

## Output Quality
- **Sample Rate**: 22050 Hz (configurable)
- **Format**: 16-bit WAV files
- **Voice Fidelity**: High-quality voice cloning with speaker characteristics preserved
- **Naturalness**: Smooth audio transitions between synthesized chunks

## Use Cases
- **Content Creation**: Generate narration for videos, podcasts, audiobooks
- **Accessibility**: Convert text content to speech for visually impaired users
- **Localization**: Create multilingual content with consistent voice characteristics
- **Gaming**: Generate dialogue for interactive applications
- **Education**: Create educational content with custom voice personas

## Dependencies
- **TTS**: Coqui TTS library for XTTS v2 model
- **PyTorch**: Deep learning framework with CUDA support
- **torchaudio**: Audio processing and I/O operations
- **transformers**: Hugging Face transformers library
- **Standard Libraries**: json, os, pathlib, logging, typing, re, dataclasses

## Hardware Requirements
- **Recommended**: NVIDIA GPU with CUDA support (8GB+ VRAM)
- **Minimum**: CPU-only execution (significantly slower)
- **Storage**: Sufficient disk space for model files and generated audio
- **Memory**: 8GB+ RAM recommended for large batch processing

## Error Handling
- **Model Loading**: Graceful fallback and error reporting
- **Audio Processing**: Skip corrupted or missing reference files
- **Text Processing**: Handle malformed input gracefully
- **File I/O**: Robust file handling with proper error messages

## Output Management
- **Directory Structure**: Organized output in specified directory
- **File Naming**: Preserves original script identifiers
- **Batch Operations**: Processes multiple scripts sequentially
- **Progress Tracking**: Detailed logging of processing status

This pipeline provides a production-ready solution for high-quality speech synthesis with voice cloning capabilities, suitable for both research and commercial applications.
