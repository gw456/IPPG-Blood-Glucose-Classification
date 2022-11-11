# IPPG-Blood-Glucose-Classification
In this project, I tried to classify blood glucose level (whether it is high or normal) using imaging photoplethysmography (IPPG) signal. This use this code, you should follow this steps:

Metode Penelitian -> Pixel Average -> IPPG Signal Extraction -> Signal Filtering -> Pemotongan Video -> Simpan Sinyal Potongan Video ke CSV -> Plot Sinyal dari CSV -> Ekstraksi Titik Puncak dan Lembah -> Segmentasi Sinyal -> Ekstraksi Fitur -> Seleksi Data -> Menjadikan Fitur Jadi 1 File -> Visualisasi Fitur 1 -> Visualisasi Fitur 2  -> Seleksi Fitur -> SVM

Those steps can be concluded into some representative step, namely data collection and data cleaning, signal processing, features extraction and SVM model development.

## Data Collection and Data Cleaning
In this step, I collect 62 subject data (37 subject with normal blood glucose level and 25 with high blood glucose level). The duration of recording is ranged around 2-3 minutes. I used additional light source to lighten the face of the subjects. The mistakes I made in data collection step are didn't measure optimal distance from camera (I used Samsung Galaxy A31 front camera) to subject's face; Didn't properly measure subject's PPG signal as comparison; and didn't properly adjust light source characteristic (whether it contain expected wave length and has enough intensity). After that, I cut parts of videos that contain subject's movement (it causes noise for the signal).

## Signal Processing
This step contain signal filtering that is done in 2 steps, namely baseline wander elimination and bandpass filter implementation. In the first step, I used DWT to eliminate lower frequency that cause baseline wander context. Then I use bandpass filter to obtain blood flow information and eliminate another infomation (considered as noise). The mistake I made in this step is not compare frequnce domain of signal before and aftar denoising to evaluate the process. After that, I extracted signal's peak and valley, to segment it and to help extracting its features.

## Features Extraction
After segment it into 1 periodic signal (2 valley and 1 peak), I performed features extraction. There are several features to extract. After extracting those features, I seperated signals that has reasonable features value and used them for further process. After this, I used pearson correlation coefficient to find colinear features and used boxplot to visualize features value distribution. Using these evaluation, I selected several relevant features to classify my data.

## SVM Model Development
Using selected features, I use SVM to classify it. I tried to changed gamma and c value to get better accuracy and f1-score.

Reference:
Rong, M. and Li, K. (2021) ‘A Blood Pressure Prediction Method Based on Imaging Photoplethysmography in combination with Machine Learning’, Biomedical Signal Processing and Control, 64(November 2020), p. 102328. doi: 10.1016/j.bspc.2020.102328.
