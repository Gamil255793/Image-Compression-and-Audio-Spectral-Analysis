Project Overview
This project consists of two main tasks: Image Compression and Audio Spectral Analysis and Filtering. Each task is implemented in MATLAB, and the project demonstrates techniques such as Discrete Cosine Transform (DCT), Inverse DCT (IDCT), Butterworth filtering, and frequency domain analysis.

Task 1: Image Compression
Description:
The image compression task demonstrates how to apply the Discrete Cosine Transform (DCT) and Inverse DCT to compress an image and then decompress it. The image is decomposed into three color components (Red, Green, and Blue), and various compression levels (m=1 to m=4) are applied to each color component. The compression is done by retaining only the top-left mxm block of the DCT of each 8x8 block of the image, followed by padding and inverse DCT for decompression.

Steps:
Decompose the image into its Red, Green, and Blue components.

Apply DCT to the 8x8 blocks of each color component.

Compress the image by retaining the top-left mxm block from the DCT of each block.

Decompress the image by applying padding and inverse DCT to reconstruct the image.

Calculate PSNR (Peak Signal-to-Noise Ratio) for each compression level (m=1, m=2, m=3, m=4) to assess the quality of the compressed image.

Plot the PSNR vs Compression Level to visualize the relationship between compression and image quality.

Results:
The compressed images show a significant decrease in file size compared to the original image, with varying quality depending on the compression level (m).

The PSNR value increases as the compression level (m) increases, indicating better image quality with less compression.

Example Image Sizes:
Original Image Size: 5.93MB

Compressed Image Sizes:

m=1: 94.9 KB

m=2: 379 KB

m=3: 854 KB

m=4: 1.48MB

Task 2: Audio Spectral Analysis and Filtering
Description:
In this task, audio spectral analysis and filtering are performed using a Butterworth filter. The audio file is analyzed in the frequency domain using the Fast Fourier Transform (FFT), and a low-pass Butterworth filter is applied to remove specific frequencies. The task includes the following steps:

Read the audio file and plot its unshifted and shifted magnitude spectrum.

Apply a Butterworth filter to the audio signal to remove noise and unwanted frequencies.

Visualize the filtered signal in the frequency domain and the frequency response of the filter.

Generate and visualize the impulse response of the filter.

Stretch the audio by a factor of 2 and analyze its frequency spectrum.

Filter Specifications:
Passband Frequency (Fpass): 2500 Hz

Stopband Frequency (Fstop): 2800 Hz

Steps:
Perform FFT on the original audio signal and plot its magnitude spectrum.

Shift the spectrum to center around zero frequency for better visualization.

Apply a low-pass Butterworth filter with a cutoff frequency of 2500 Hz.

Plot the filtered magnitude spectrum and the frequency response of the filter.

Generate the impulse response of the filter using the inverse Fourier transform of the frequency response.

Stretch the audio (increase playback speed) and analyze its new spectrum.

Results:
The shifted magnitude spectrum clearly shows the frequency components of the audio signal.

The filtered spectrum shows how unwanted frequencies are removed, improving the quality of the audio.

The impulse response and frequency response of the Butterworth filter demonstrate the behavior of the filter in both time and frequency domains.

After speeding up the audio, its frequency spectrum is stretched, indicating a shift in the frequency components due to the increased playback speed.

Files Included:
image1.bmp: The original image for compression.

audio.wav: The original audio file for spectral analysis and filtering.

compressed3.bmp: The compressed image using m=3.

m3.bmp: The decompressed image after applying inverse DCT and padding.

How to Run:
Install MATLAB: Ensure you have MATLAB installed with the necessary toolboxes (Signal Processing Toolbox).

Prepare the Files:

Place the image file (image1.bmp) and audio file (audio.wav) in the working directory.

Run the Scripts: Open MATLAB and run the provided scripts for both Image Compression and Audio Spectral Analysis and Filtering. The scripts will process the files and generate the required output images and plots.
