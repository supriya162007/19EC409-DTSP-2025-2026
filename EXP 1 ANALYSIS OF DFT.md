# EXP 1 :  ANALYSIS OF DFT WITH AUDIO SIGNAL

# AIM: 

  To analyze audio signal by removing unwanted frequency. 

# APPARATUS REQUIRED: 
   
   PC installed with SCILAB/Python. 

# PROGRAM: 
```
# ================================
# DFT (FFT) ANALYSIS OF AUDIO SIGNAL
# ================================

# Step 1: Upload audio file
from google.colab import files
uploaded = files.upload()

# Get uploaded file name
filename = list(uploaded.keys())[0]

# ================================
# Step 2: Import libraries
# ================================
import numpy as np
import matplotlib.pyplot as plt
from scipy.io import wavfile
from scipy.signal import spectrogram
from IPython.display import Audio

# ================================
# Step 3: Read audio file
# ================================
fs, x = wavfile.read(filename)

# Convert to mono if stereo
if len(x.shape) == 2:
    x = x.mean(axis=1)

# Normalize signal
x = x / np.max(np.abs(x))

print("Sampling Frequency (Hz):", fs)
print("Total Samples:", len(x))
print("Duration (seconds):", len(x)/fs)

# ================================
# Step 4: Time Domain Plot
# ================================
t = np.arange(len(x)) / fs

plt.figure(figsize=(10,4))
plt.plot(t, x)
plt.title("Time Domain Signal")
plt.xlabel("Time (seconds)")
plt.ylabel("Amplitude")
plt.grid()
plt.show()

# ================================
# Step 5: Apply Window (Hamming)
# ================================
window = np.hamming(len(x))
x_windowed = x * window

# ================================
# Step 6: FFT (DFT)
# ================================
N = len(x_windowed)

X = np.fft.fft(x_windowed)
freqs = np.fft.fftfreq(N, 1/fs)

# Only positive half
half_N = N // 2

# ================================
# Step 7: Frequency Spectrum Plot
# ================================
plt.figure(figsize=(10,4))
plt.plot(freqs[:half_N], np.abs(X[:half_N]))
plt.title("Frequency Spectrum (DFT using FFT)")
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")
plt.grid()
plt.show()

# ================================
# Step 8: Spectrogram
# ================================
f, t_spec, Sxx = spectrogram(x, fs)

plt.figure(figsize=(10,5))
plt.pcolormesh(t_spec, f, 10 * np.log10(Sxx + 1e-10), shading='gouraud')
plt.title("Spectrogram")
plt.ylabel("Frequency (Hz)")
plt.xlabel("Time (seconds)")
plt.colorbar(label="Intensity (dB)")
plt.show()

# ================================
# Step 9: Play Audio
# ================================
print("Audio Playback:")
display(Audio(x, rate=fs))
```

# OUTPUT: 


<img width="875" height="393" alt="image" src="https://github.com/user-attachments/assets/44673d3a-f35d-4470-a266-c367c3fab91f" />
<img width="866" height="393" alt="image" src="https://github.com/user-attachments/assets/4b9c9ba1-3cd7-4d84-a254-171f15dbc3d5" />

<img width="838" height="470" alt="image" src="https://github.com/user-attachments/assets/c7f5008b-2ff8-44ab-91e4-fcb5fbe7ce0e" />


# RESULTS
 analyze audio signal by removing unwanted frequency is verified
