# shuffle and buffle

**Description:**  
A web-based tool for applying **buffer shuffle** effects to audio files.  
Provides real-time visualization of the resulting audio and options to download the processed track.  

---

## Features

- Shuffle audio **at byte-level blocks** (buffer shuffle)  
- Adjustable **block size** and **shuffle intensity**  
- Optional **start and end offsets** to shuffle only part of the track  
- Real-time **audio visualizer**  
- Custom **play/pause controls**  
- Download the processed WAV file  

---

## User Interface

### Inputs
- **File Upload** – Select an audio file.  
- **Block Size (bytes)** – Range slider (256–8192). Sets the size of each block used in shuffling.  
- **Shuffle Intensity (%)** – Range slider (1–100). Controls how many blocks will be randomly swapped.  
- **Start Offset (%)** – Range slider (0–50). Sets the start point of shuffling relative to the track length.  
- **End Offset (%)** – Range slider (50–100). Sets the end point of shuffling relative to the track length.  

### Buttons
- **Shuffle Buffer** – Generates the shuffled audio buffer based on current settings.  
- **Play** – Plays the shuffled audio.  
- **Pause** – Stops the current playback.  
- **Download** – Download the shuffled audio as a WAV file.  

### Visualizer
- **Canvas** – Displays the waveform of the audio in real-time during playback.  

---

## How It Works

1. **File Loading**  
   - WAV file is read using `FileReader` and decoded with `AudioContext.decodeAudioData()`.  

2. **Buffer Shuffle Algorithm**  
   - The selected range (startOffset → endOffset) is divided into blocks of the chosen size.  
   - Random swaps are applied according to the shuffle intensity.  
   - The shuffled blocks are merged into a new audio buffer.  

3. **Playback**  
   - The shuffled buffer is played using an `AudioBufferSourceNode`.  
   - Playback can be started/stopped using **Play/Pause** buttons.  

4. **Download**  
   - The buffer is converted to WAV format using `DataView` and `Blob`.  
   - The download link points to the generated WAV file.  

5. **Visualization**  
   - An `AnalyserNode` provides time-domain data for drawing the waveform on the canvas.  
   - The waveform updates in real-time during playback.  

---

## Code Overview

**Variables**
- `audioCtx` – Web Audio API `AudioContext`  
- `analyser` – `AnalyserNode` for waveform visualization  
- `sourceNode` – Current `AudioBufferSourceNode`  
- `shuffledBuffer` – Processed `AudioBuffer` with buffer shuffle applied  
- `dataArray` – `Uint8Array` holding waveform data for visualization  

**Functions**
- `initAudioContext()` – Initializes AudioContext and AnalyserNode.  
- `updateVisualization()` – Draws waveform continuously on canvas.  
- `bufferToWav(buffer)` – Converts an AudioBuffer to a WAV Blob.  
- Event listeners handle **shuffle**, **play**, and **pause** functionality.  

---

## Usage

1. Select an audio file using the file input.  
2. Adjust **block size**, **shuffle intensity**, **start offset**, and **end offset**.  
3. Click **Shuffle Buffer** to generate the shuffled track.  
4. Use **Play / Pause** buttons to listen.  
5. Click **Download** to save the shuffled WAV file.  

---

## License

MIT License
