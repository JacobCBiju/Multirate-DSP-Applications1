# Multirate-DSP-Applications1

1.Multirate DSP Applications

Music Tempo Adjustment

**Aim**

The goal of this project is to develop and implement a digital signal processing (DSP) technique using Python in the Google Colab environment to achieve Time-Scale Modification (TSM) of audio signals. The primary objective is to adjust the playback tempo—either by stretching or compressing time—based on a user-defined factor, while maintaining the original pitch and avoiding noticeable artifacts. This is accomplished through sophisticated DSP methods such as the Phase Vocoder, applied via the Librosa library, which enables effective separation of the audio signal’s time and frequency components.


**Program**

# 1. INSTALL NECESSARY LIBRARIES
print("Installing libraries...")
!pip install librosa numpy soundfile IPython matplotlib

# ---------------------------------------------------------
# 2. IMPORT MODULES
import librosa
import librosa.display
import numpy as np
import soundfile as sf
import matplotlib.pyplot as plt
from IPython.display import Audio, display
import os

# ---------------------------------------------------------
# 3. DIRECT UPLOAD OPTION
# Instead of using files.upload(), this uses Colab’s file-explorer.

print("\n--- Direct Upload Option ---")
print("➡ You can upload your audio file directly through the Colab File Explorer (left panel):")
print("📁 Click the Folder icon → Click 'Upload' → Select your audio file.")
print("Then type the filename (with extension) below to load it.\n")

# Example filename once uploaded in /content/
file_name = input("Enter the audio filename (e.g., sample.wav): ").strip()

# ---------------------------------------------------------
# 4. DEFINE PARAMETER
STRETCH_RATE = 1.25  # Change to 0.5 for slower audio or 2.0 for faster
print(f"\nTarget Tempo Adjustment Rate: {STRETCH_RATE}")

# ---------------------------------------------------------
# 5. LOAD AND PROCESS AUDIO
print("\nLoading audio file...")
y, sr = librosa.load(file_name, sr=None, mono=True)
print(f"Original Audio Duration: {len(y)/sr:.2f} seconds")

# Apply time-stretch (tempo change without pitch shift)
y_stretched = librosa.effects.time_stretch(y, rate=STRETCH_RATE)
print(f"Stretched Audio Duration: {len(y_stretched)/sr:.2f} seconds")

# ---------------------------------------------------------
# 6. VISUALIZE RESULTS
plt.figure(figsize=(12, 6))
plt.subplot(2, 1, 1)
librosa.display.waveshow(y, sr=sr)
plt.title('Original Waveform (Tempo: 1.0x)')
plt.xlim(0, len(y)/sr)

plt.subplot(2, 1, 2)
librosa.display.waveshow(y_stretched, sr=sr)
plt.title(f'Stretched Waveform (Tempo: {STRETCH_RATE}x)')
plt.xlim(0, len(y_stretched)/sr)

plt.tight_layout()
plt.show()

# ---------------------------------------------------------
# 7. PLAY AND EXPORT AUDIO
output_file = f"tempo_adjusted_{STRETCH_RATE}x_{os.path.basename(file_name)}"
sf.write(output_file, y_stretched, sr)
print(f"\nProcessed audio saved as: {output_file}")

# Display players
print("\n--- Original Audio ---")
display(Audio(data=y, rate=sr))
print("\n--- Tempo Adjusted Audio ---")
display(Audio(data=y_stretched, rate=sr))

# Create download link
from google.colab import files
files.download(output_file)
print("\n✅ Download link generated successfully!")


**Original Audio**

[Elton_John_-_Im_Still_Standing_(getmp3.pro).mp3](https://github.com/user-attachments/files/22944005/Elton_John_-_Im_Still_Standing_.getmp3.pro.mp3)


**Tempo Adjusted Audio**

[tempo_adjusted_1.25x_Elton_John_-_Im_Still_Standing_(getmp3.pro) (1).mp3](https://github.com/user-attachments/files/22944168/tempo_adjusted_1.25x_Elton_John_-_Im_Still_Standing_.getmp3.pro.1.mp3)


**Waveform**

<img width="1189" height="590" alt="image" src="https://github.com/user-attachments/assets/05e1d781-8c94-4463-b8ce-e7ac636a5853" />


**Conclusion**

This project effectively developed a Music Tempo Adjustment system utilizing the Librosa library within Google Colab. By leveraging the Phase Vocoder algorithm, it successfully addressed the key challenge of altering tempo independently of pitch. The input audio’s duration was modified according to the desired stretch factor (e.g., sped up by 1.25× or slowed down by 0.5×), producing an output where the tempo was adjusted while preserving the original pitch and harmonic content. The implementation offers a reliable and practical example of Time-Scale Modification (TSM) methods, making it well-suited for applications in music production and audio analysis that demand tempo variation without the quality loss typical of basic resampling techniques..
