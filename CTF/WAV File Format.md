Source: [WaveFormat](http://soundfile.sapp.org/doc/WaveFormat/)

![[../Resources/Saved Pages/Microsoft WAVE soundfile format.pdf|Microsoft WAVE soundfile format]]

---
# WAV File Format
> **The default byte ordering assumed for WAVE data files is `little-endian`.**
## Overview
- **Extension:** .wav
- **MIME Type:** audio/wav
- **Encoding:** PCM (Pulse Code Modulation) or other formats
- **File Type:** Binary
## Structure
A WAV file consists of several chunks, each serving a specific purpose. The basic structure includes:
1. **RIFF Header:**
    - 4 bytes: "RIFF" (Resource Interchange File Format) identifier. **\[Big Endian\]**
    - 4 bytes: Total size of the file excluding this 8-byte header.
    - 4 bytes: "WAVE" identifier. **\[Big Endian\]**
2. **Format Chunk (fmt):**
    - 4 bytes: "fmt " (format) identifier.  **\[Big Endian\]**
    - 4 bytes: Size of the format chunk (usually 16 for PCM).
    - 2 bytes: Audio format (1 for PCM).
    - 2 bytes: Number of channels (1 for mono, 2 for stereo, etc.).
    - 4 bytes: Sample rate (number of samples per second).
    - 4 bytes: Byte rate (number of bytes per second).
    - 2 bytes: Block align (number of bytes for one sample).
    - 2 bytes: Bits per sample.
3. **Data Chunk (data):**
    - 4 bytes: "data" identifier. **\[Big Endian\]**
    - 4 bytes: Size of the data (number of bytes in the data chunk).
4. **Audio Data:**
    - Actual audio samples in PCM or other specified format.

## Sample Rate and Bit Depth
- **Sample Rate:** The number of samples of audio carried per second, measured in Hertz (Hz).
- **Bit Depth:** The number of bits of information in each sample, representing the amplitude of the audio signal.

## Compression
While PCM is the most common encoding for WAV files, other compression formats may be used, such as ADPCM (Adaptive Differential Pulse Code Modulation) or MP3. In such cases, additional chunks and information may be present.