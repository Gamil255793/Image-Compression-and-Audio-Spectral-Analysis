# Image-Compression-and-Audio-Spectral-Analysis
Project Overview
This project involves two main tasks:

Image Compression using DCT

Audio Spectral Analysis and Filtering

The image compression part includes reading an image, decomposing it into its color components, applying block-based DCT for compression, and then reconstructing the image using inverse DCT.
The audio part involves performing spectral analysis on an audio signal, applying a Butterworth filter, and visualizing the results.

Sections:
Image Compression

Audio Spectral Analysis and Filtering

1. Image Compression
Objective:
Compress an image by applying the Discrete Cosine Transform (DCT) to its color components, retaining the top-left mxm block, and then decompressing it using Inverse DCT.

Steps:
a) Decompose the Image:
The image is read into a matrix, then decomposed into Red, Green, and Blue components. Each component is saved as a separate image file.

A = imread('image1.bmp');
RA = A(:,:,1);  % Red Component
GA = A(:,:,2);  % Green Component
BA = A(:,:,3);  % Blue Component
imwrite(RA,'imageredcomponent.bmp');
imwrite(GA,'imagegreencomponent.bmp');
imwrite(BA,'imagebluecomponent.bmp');
b) Compression (DCT and Block Processing):
Apply DCT on 8x8 blocks of each color component and retain the top-left mxm part for compression.

A = imread('image1.bmp');
RA = A(:,:,1);
GA = A(:,:,2);
BA = A(:,:,3);
m = 3;  % Compression level (can vary from 1 to 4)
fun1 = @(block_struct) dct2(block_struct.data);
fun2 = @(block_struct) block_struct.data(1:m,1:m);  % Take the top-left mxm block
RA_dct = blockproc(RA,[8 8],fun1);
GA_dct = blockproc(GA,[8 8],fun1);
BA_dct = blockproc(BA,[8 8],fun1);
RA_compressed = blockproc(RA_dct,[8 8],fun2);
GA_compressed = blockproc(GA_dct,[8 8],fun2);
BA_compressed = blockproc(BA_dct,[8 8],fun2);
imwrite(cat(3,RA_compressed,GA_compressed,BA_compressed),'compressed3.bmp');
c) Decompression and Inverse DCT:
Decompress the image by padding the top-left mxm block, applying the inverse DCT, and reconstructing the original image.

A = imread('image1.bmp');
RA = A(:,:,1);
GA = A(:,:,2);
BA = A(:,:,3);
m = 3;
fun1 = @(block_struct) dct2(block_struct.data);
fun3 = @(block_struct) padarray(block_struct.data(1:m,1:m),[8-m 8-m],'post');
fun4 = @(block_struct) idct2(block_struct.data);  % Inverse DCT
RA_dct = blockproc(RA,[8 8],fun1);
GA_dct = blockproc(GA,[8 8],fun1);
BA_dct = blockproc(BA,[8 8],fun1);
RA_padded = blockproc(RA_dct,[8 8],fun3);
GA_padded = blockproc(GA_dct,[8 8],fun3);
BA_padded = blockproc(BA_dct,[8 8],fun3);
RA_decomp = blockproc(RA_padded,[8 8],fun4);
GA_decomp = blockproc(GA_padded,[8 8],fun4);
BA_decomp = blockproc(BA_padded,[8 8],fun4);
RA_decomp3 = cat(3,RA_decomp,RA_decomp,RA_decomp);
RA_uint8 = uint8(RA_decomp3);
RA_NewImage = RA_uint8(:,:,1);
GA_decomp3 = cat(3,GA_decomp,GA_decomp,GA_decomp);
GA_uint8 = uint8(GA_decomp3);
GA_NewImage = GA_uint8(:,:,1);
BA_decomp3 = cat(3,BA_decomp,BA_decomp,BA_decomp);
BA_uint8 = uint8(BA_decomp3);
BA_NewImage = BA_uint8(:,:,1);
NewImage = cat(3,RA_NewImage,GA_NewImage,BA_NewImage);
imwrite(NewImage,'m3.bmp');
d) PSNR Calculation:
Calculate the Peak Signal-to-Noise Ratio (PSNR) of the decompressed image.

psnr(NewImage, A);
e) PSNR vs m Plot:
Plot the relationship between compression level m and PSNR.

matlab
Copy
Edit
x_discrete = [1 2 3 4];
y_discrete = [19.8635 21.9069 23.7734 25.9427];
plot(x_discrete, y_discrete);
xlabel('Compression level (m)');
ylabel('PSNR');
title('PSNR vs Compression level');
2. Audio Spectral Analysis and Filtering
Objective:
Perform spectral analysis on an audio signal, apply a Butterworth filter, and visualize the frequency response, magnitude spectrum, and impulse response.

Steps:
a) Original Audio Spectrum:
Plot the unshifted magnitude spectrum of the audio signal.

[x, fs] = audioread('audio.wav');
N = length(x);
k = 0:N-1;
X = fft(x, N);
plot(k, abs(X));
title('Unshifted Spectrum');
xlabel('Frequency (Hz)');
ylabel('Magnitude');
b) Shifted Spectrum:
Shift the frequency spectrum for visualization.

f = (-N/2:N/2-1) * fs / N;
plot(f, abs(fftshift(X)) / N);
title('Shifted Spectrum');
xlabel('Frequency (Hz)');
ylabel('Magnitude');
c) Filter the Audio:
Apply a Butterworth filter to the audio signal.

FD = designfilt('lowpass', 'FilterOrder', 10, 'CutoffFrequency', 2500, 'SampleRate', fs);
xFiltered = filter(FD, x);
sound(xFiltered, fs);
d) Filtered Spectrum:
Plot the spectrum of the filtered audio signal.

plot(f, abs(fftshift(fft(xFiltered))) / N);
title('Filtered Shifted Spectrum');
xlabel('Frequency (Hz)');
ylabel('Magnitude');
e) Frequency Response of Filter:
Visualize the frequency response of the Butterworth filter.

matlab
Copy
Edit
freqz(FD);
title('Frequency Response of Butterworth Filter');
f) Impulse Response:
Visualize the impulse response of the filter.

impz(FD);
title('Impulse Response');
g) Speed Up the Audio:
Stretch the audio and plot the new spectrum.

xFast = stretchAudio(xFiltered, 2);
sound(xFast, fs);
Nfast = length(xFast);
ffast = (-Nfast/2:Nfast/2-1) * 2 * fs / Nfast;
plot(ffast, abs(fftshift(fft(xFast, Nfast))) / Nfast);
title('Magnitude Spectrum of Speeded-Up Audio');
xlabel('Frequency (Hz)');
ylabel('Magnitude');
Project Files:
Image Compression Files: image1.bmp, compressed3.bmp, m3.bmp

Audio Files: audio.wav

Installation and Requirements:
To run the code, you will need the following:

MATLAB or Octave

Signal Processing Toolbox (for dct2, idct2, freqz, impz, etc.)
