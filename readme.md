
# HDR Color Meter for Windows

[![Get it from Microsoft](https://get.microsoft.com/images/en-us%20dark.svg)](https://apps.microsoft.com/detail/9NFTNFF5SDNT)


HDR Color Meter can read the native HDR pixel values under the user's cursor, as well as SDR RGB values.

It shows the native pixel values from the HDR framebuffer (scRGB float16), and also shows the pixel values in Linear BT709 and BT2020 (100.0 = 100 nits)

### Screenshots

**Reading SDR RGB values**



https://github.com/user-attachments/assets/66ec66eb-d9fe-4b43-8851-35810501485b



**Reading HDR RGB values**

<img width="650"  alt="Screenshot 2026-05-22 06-13-22_cropped" src="https://github.com/user-attachments/assets/a0bcf6ca-1cd9-46fc-99c5-93817518ec55" />

<img width="700"  alt="Screenshot 2026-05-22 06-15-17_cropped" src="https://github.com/user-attachments/assets/ed904f76-3044-41ab-bafc-e96b685750d6" />




&nbsp;


The HDR screenshots are taken as JXR on a Windows PC with SDR at 100 nits, and luminance is scaled 2.03x before saving as PNG. The screenshots appears identical to the original image when Chrome is used at OS SDR = 100 nits (Chrome scales 203 nits in HDR images to SDR white).

### Regarding precision

This app reads the native scRGB FP16 values from the Windows HDR frame buffer, so we are limited by FP16's precision.

https://learn.microsoft.com/en-us/windows/win32/direct3darticles/high-dynamic-range documents the color space:

> - scRGB color space (BT.709/sRGB primaries with linear gamma)
> - IEEE half precision (FP16 bit depth)
> - 1.0f is 80 nits

At 100 nits (scRGB 1.25), FP16's quantisation step is 2^-10 * 1.0 = 0.000977 in scRGB or ≈ 0.08 nits.

PQ HDR videos are typically encoded with 10 bit limited range, and this has a larger quantisation step of 0.98 nits at a signal of 100 nits.

- Limited range PQ code value 509 is 100.23 nits
- Limited range PQ code value 510 is 101.21 nits (so 0.98 nits higher)
