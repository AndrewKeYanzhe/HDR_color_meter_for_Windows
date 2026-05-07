
# HDR Color Meter for Windows

This app can read native HDR pixel values under the user's mouse.

It shows the native pixel values from the HDR framebuffer (scRGB float16), and also shows the pixel values in Linear BT709 and BT2020 (100.0 = 100 nits)

<img width="2030" height="732" alt="Screenshot 2026-05-07 02-04-43_cropped" src="https://github.com/user-attachments/assets/f3ecee17-20e2-4181-bb1a-b619d91d5445" />

<img width="2123" height="739" alt="Screenshot 2026-05-07 02-09-07_cropped" src="https://github.com/user-attachments/assets/da4a8e52-f8f4-4c6b-962f-42cc4b11eec5" />

### Regarding precision

This app reads the native scRGB FP16 values from the Windows HDR frame buffer, so we are limited by FP16's precision.

https://learn.microsoft.com/en-us/windows/win32/direct3darticles/high-dynamic-range documents the color space:

> - scRGB color space (BT.709/sRGB primaries with linear gamma)
> - IEEE half precision (FP16 bit depth)
> - 1.0f is 80 nits

At 100 nits (scRGB 1.25), FP16's quantisation step is 2^-10 * 1.0 = 0.000977 in scRGB or ≈ 0.1 nits.

PQ HDR videos are typically encoded with 10 bit limited range, and this has a larger quantisation step of 0.98 nits at a signal of 100 nits.

- Limited range PQ code value 509 is 100.23 nits
- Limited range PQ code value 510 is 101.21 nits (so 0.98 nits higher)
