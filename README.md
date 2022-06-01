# About

MotionCam is a camera application for Android that replaces the entire camera pipeline. It consumes RAW images and uses computational photography to combine multiple images to reduce noise.

Download the latest free release:

<a href='https://play.google.com/store/apps/details?id=com.motioncam&pcampaignid=pcampaignidMKT-Other-global-all-co-prtnr-py-PartBadge-Mar2515-1'><img alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png' width="25%"/></a>

Download the latest PRO release:

<a href='https://play.google.com/store/apps/details?id=com.motioncam.pro&pcampaignid=pcampaignidMKT-Other-global-all-co-prtnr-py-PartBadge-Mar2515-1'><img alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png' width="25%"/></a>

## Get Help / Join a discussion about the app

For bug reports, discussions and feature requests/ideas join us on Discord:

[Discord Invite](https://discord.gg/Vy4gQNEdNS)

# RAW video capture

Capture RAW video up to 60 FPS on supported devices.

### Convert to DNG on your PC

Download tools to convert the recorded videos to DNG on your PC:

![Windows](https://github.com/mirsadm/motioncam/releases/download/v0.22/motioncam-tools-0.22-win-x64.zip)

![Mac M1](https://github.com/mirsadm/motioncam/releases/download/v0.22/motioncam-tools-0.2.2-macos-m1.zip)

### Tutorials

https://youtu.be/-i_TvErm3C0

https://youtu.be/DX1FEtEnt5Y

## Other features

#### Dual exposure

Dual exposure is similar to the feature found in the Google Camera. The two sliders control the exposure compensation and tonemapping.

![Dual Exposure](https://user-images.githubusercontent.com/508688/118869074-d4f3de80-b8dc-11eb-8ca6-6261e3e1ea4d.gif)

#### Zero shutter lag burst capture

![Burst Capture](https://user-images.githubusercontent.com/508688/118869720-a7f3fb80-b8dd-11eb-8292-5e7a6ae899cc.gif)

#### Photo Mode

Photo mode captures RAW images in the background. It captures a single underexposed image when the shutter button is pressed which is used to recover highlights and increase dynamic range.

#### Night Mode

Night mode increases the shutter speed of the camera up to 1/3 of a second and captures more RAW images to further reduce noise.

## Overview

### Noise Reduction

The denoising algorithm uses bayer RAW images as input. Motion Cam treats the RAW data as four colour channels (red, blue and two green channels). It starts by creating an optical flow map between a set of images and the reference image utilising [Fast Optical Flow using Dense Inverse Search](https://arxiv.org/abs/1603.03590). Then, each colour channel is fused using a simplified Gaussian pyramid.

### Camera Preview

Motion Cam uses the GPU to generate a real time preview of the camera from its RAW data. It uses a simplified pipeline to produce an accurate representation of what the final image will look like. This means it is possible to adjust the tonemapping, contrast and colour settings in real time.

### Demosaicing

Most modern cameras use a bayer filter. This means the RAW image is subsampled and consists of 25% red, 25% blue and 50% green pixels. There are more green pixels because human vision is most sensitive to green light. The output from the denoising algorithm is demosaiced and colour corrected into an sRGB image. Motion Cam uses the algorithm [Color filter array demosaicking: New method and performance measures by Lu and Tan](https://pdfs.semanticscholar.org/37d2/87334f29698e451282f162cb4bc4f1f352d9.pdf).

### Tonemapping

Motion Cam uses the algorithm [exposure fusion](https://mericam.github.io/exposure_fusion/index.html) for tonemapping. The algorithm blends multiple different exposures to produce an HDR image. Instead of capturing multiple exposures, it artificially generates the overexposed image and uses the original exposure as inputs to the algorithm. The shadows slider in the app controls the overexposed image.

### Sharpening and Detail Enhancement

The details of the image are enhanced and sharpened using an unsharp mask with a threshold to avoid increasing the noise.
