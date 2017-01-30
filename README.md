# Creating playlists with timbrically similar segments
Pablo Alonso and Daniel Balcells

Audio and Music Processing Lab - SMC 2017

The goal of this project is to process a small music dataset in order to create several playlists, each of them containing short fragments of timbrically similar music. 

## Instructions
Use jupyter-notebook to open the main file `music-segments-playlist.ipynb`.
Dependencies:
- [Essentia](https://github.com/mtg/essentia)
- Scipy
- Numpy
- Matplotlib
- SKLearn

## Algorithm overview
The steps we follow are:

### 1. Feature Extraction
This first stage aims at splitting the dataset into short segments and describing their timbre. The main steps are:
1. Load audio files (see dataset list below).
2. Estimate beat positions using Essentia's Degara beat tracking algorithm.
3. Split songs into segments that are 8 beats in length.
4. For each segment, obtain MFCC spectrogram using 12 coefficients and omitting the 0-th order coefficient.
5. Summarize the MFCC spectrogram of each segment by taking mean, variance, minimum, maximum and median values for each of the 12 coefficients.

### 2. Clustering
In this stage, we use a standard K-Means clustering algorithm to label each of the previously extracted segments as belonging to one of eight possible clusters. The algorithm is trained on the entire collection of segments. It is expected that segments that are timbrically similar, although belonging to different songs, are clustered together.

### 3. Example playlist generation
Finally, we use the cluster labels provided by the clustering stage to generate a short playlist for each cluster. This is done by randomly choosing and concatenating ten different segments from each cluster. Since the segments are obtained by splitting songs at estimated beat positions, the transitions between fragments are relatively smooth in terms of rhythm.

## Dataset
We chose 18 songs from our personal music collections, with genres including Reggae, Hip-Hop, Electronic, Classical, Metal, World, Rock and Ambient. Audio formats included WAV, MP3 and M4A. The full list is the following:
- **Reggae**: *The Dreamer* and *Daniel* by Groundation.
- **Hip-Hop**: *Big Poppa* by The Notorious B.I.G.
- **Electronic**: *The Game of Love* by Daft Punk; and *Apathy* by Shlohmo.
- **Classical**: *Die Forelle*, composed by Franz Schubert and played by Fischer-Dieskau and Moore.
- **Metal**: *Bullet In The Head* by Rage Against The Machine; *Exile*, *Seven Names* and *Cages* by Tesseract; *Master's Apprentices* by Opeth; and *Ragnarok* by Periphery.
- **World**: *World Turning* by Leo Kottke; and *Pedro Navaja* by Rubén Blades.
- **Rock**: *Hey Joe* and *Voodoo Child (Slight Return)* by The Jimi Hendrix Experience.
- **Ambient**: *Seven Names (Reimagined)* and *Cages (Reimagined)* by Tesseract.
