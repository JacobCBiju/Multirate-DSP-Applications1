# Multirate-DSP-Applications1
1.Multirate DSP Applications
Music Tempo Adjustment
Aim
The aim of this project is to design and implement a digital signal processing (DSP) solution in a Python environment (Google Colab)
to perform Time-Scale Modification (TSM) on an audio signal. Specifically, the objective is to change the playback speed or tempo of a
music file (time-stretching or time-compressing) by a user-defined factor without altering the original pitch or introducing significant
artifacts. This is achieved by employing advanced DSP algorithms like the Phase Vocoder via the librosa library, which effectively
decouples the time and frequency domains of the audio signal.
program
# =========================================================
# MUSIC TEMPO ADJUSTMENT (TIME-STRETCHING) IN GOOGLE COLAB
# =========================================================
# 1. INSTALL NECESSARY LIBRARIES
# librosa is the core library for audio processing and time-stretching.
# soundfile is used for saving the processed audio file.
print("Installing libraries...")
!pip install librosa numpy soundfile IPython
# ---------------------------------------------------------
# 2. IMPORT MODULES
import librosa
import librosa.display
import numpy as np
import soundfile as sf
import matplotlib.pyplot as plt
from google.colab import files
from IPython.display import Audio
# ---------------------------------------------------------
# 3. UPLOAD AUDIO FILE
# This uses a Colab specific function to prompt you to upload a file.
print("\n--- Upload Audio File ---")
uploaded = files.upload()
file_name = next(iter(uploaded)) # Get the name of the uploaded file
print(f"Successfully uploaded: {file_name}")
# ---------------------------------------------------------
# 4. DEFINE PARAMETER
# Change this value to adjust the tempo.
# Rate > 1.0 speeds up the audio.
# Rate < 1.0 slows down the audio.
# Example: rate = 2.0 (Twice as fast), rate = 0.5 (Half as fast)
STRETCH_RATE = 1.25 # Speed up by 25% (Faster Tempo)
print(f"\nTarget Tempo Adjustment Rate: {STRETCH_RATE}")
# ---------------------------------------------------------
# 5. LOAD AND PROCESS AUDIO
# Load the audio file (y) and its sampling rate (sr)
y, sr = librosa.load(file_name, sr=None, mono=True)
print(f"Original Audio Duration: {len(y)/sr:.2f} seconds")
# Apply Time-Stretching using librosa.effects.time_stretch
# This function uses the Phase Vocoder algorithm to adjust tempo without changing pitch.
y_stretched = librosa.effects.time_stretch(y, rate=STRETCH_RATE)
print(f"Stretched Audio Duration: {len(y_stretched)/sr:.2f} seconds")
# ---------------------------------------------------------
# 6. VISUALIZE RESULTS (Optional)
plt.figure(figsize=(12, 6))
# Plot Original Waveform
plt.subplot(2, 1, 1)
librosa.display.waveshow(y, sr=sr)
plt.title('Original Waveform (Tempo: 1.0x)')
plt.xlim(0, len(y)/sr)
# Plot Stretched Waveform
plt.subplot(2, 1, 2)
librosa.display.waveshow(y_stretched, sr=sr)
plt.title(f'Stretched Waveform (Tempo: {STRETCH_RATE}x)')
plt.xlim(0, len(y_stretched)/sr)
plt.tight_layout()
plt.show()
# ---------------------------------------------------------
# 7. PLAY AND EXPORT AUDIO
output_file = f"tempo_adjusted_{STRETCH_RATE}x_{file_name}"
# Save the processed audio to a new file
sf.write(output_file, y_stretched, sr)
print(f"\nProcessed audio saved as: {output_file}")
# Display audio players for comparison
print("\n--- Original Audio ---")
display(Audio(data=y, rate=sr))
print("\n--- Tempo Adjusted Audio (Pitch Preserved) ---")
display(Audio(data=y_stretched, rate=sr))
# Offer the user a link to download the new file
files.download(output_file)
print("\nDownload link generated.")
# =========================================================


Original Audio
yuvan_oru_naalil.mp3
Tempo Adjusted Audio (Pitch Preserved)
[tempo_adjusted_1.25x_yuvan_oru_naalil.mp3](https://github.com/user-attachments/files/22943392/tempo_adjusted_1.25x_yuvan_oru_naalil.mp3)

Waveform
<img width="946" height="425" alt="image" src="https://github.com/user-attachments/assets/d8c53eb1-f3b6-4ce6-b7d1-1076532531de" />

Conclusion
ConclusionThe project successfully implemented an efficient Music Tempo Adjustment system using the librosa library in Google
Colab. By applying the Phase Vocoder algorithm, the core challenge of decoupling tempo and pitch was overcome. The duration of the
input audio was successfully scaled by the specified stretch rate (e.g., 1.25𝑥 faster or 0.5𝑥 slower), resulting in a processed output file
where the tempo was changed, but the fundamental frequencies and perceived pitch remained unchanged. The code provides a
verifiable, practical demonstration of TSM techniques, yielding an output suitable for use in audio production or music analysis where
tempo flexibility is required without the degradation associated with simple resampling.
