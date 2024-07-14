# Image Manipulation Lab

This repository contains the code and instructions for manipulating images using Python libraries such as NumPy and PIL (Pillow). The lab covers various tasks including copying images, flipping images, cropping images, changing specific image pixels, and overlaying images.

## Objectives
- Learn how to manipulate images as arrays and PIL image objects.
- Understand how to copy images to avoid aliasing.
- Perform image flipping and cropping.
- Change specific image pixels to draw shapes, write text, and overlay images.

## Table of Contents
1. [Setup](#setup)
2. [Copying Images](#copying-images)
3. [Flipping Images](#flipping-images)
4. [Cropping Images](#cropping-images)
5. [Changing Specific Image Pixels](#changing-specific-image-pixels)
6. [Overlaying Images](#overlaying-images)
7. [Examples](#examples)
8. [Authors](#authors)
9. [References](#references)

## Setup
1. Clone the repository:
    ```bash
    git clone https://github.com/your-username/image-manipulation-lab.git
    cd image-manipulation-lab
    ```

2. Install the required libraries:
    ```bash
    pip install matplotlib Pillow numpy
    ```

3. Download the images used in the lab:
    ```bash
    !wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-CV0101EN-SkillsNetwork/images%20/images_part_1/cat.png -O cat.png
    !wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-CV0101EN-SkillsNetwork/images%20/images_part_1/lenna.png -O lenna.png
    !wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-CV0101EN-SkillsNetwork/images%20/images_part_1/baboon.png -O baboon.png
    ```

## Copying Images
Copying images to avoid aliasing ensures that changes to one image do not affect the other.

```python
import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

baboon = np.array(Image.open('baboon.png'))
A = baboon
B = baboon.copy()

print("Memory address of A:", id(A))
print("Memory address of baboon:", id(baboon))
print("Memory address of B:", id(B))

Flipping Images
Flipping images involves reordering the indices of the pixels to change the orientation of the image.
from PIL import ImageOps

image = Image.open("lenna.png")
im_flip = ImageOps.flip(image)
im_mirror = ImageOps.mirror(image)

plt.figure(figsize=(5, 5))
plt.imshow(im_flip)
plt.title("Flipped Image")
plt.show()

plt.figure(figsize=(5, 5))
plt.imshow(im_mirror)
plt.title("Mirrored Image")
plt.show()


Cropping Images
Cropping is the act of cutting out a part of an image.
array = np.array(image)
upper, lower = 150, 400
left, right = 150, 400

crop_top = array[upper:lower, :, :]
crop_horizontal = crop_top[:, left:right, :]
crop_image = image.crop((left, upper, right, lower))

plt.figure(figsize=(5, 5))
plt.imshow(crop_image)
plt.title("Cropped Image")
plt.show()

Changing Specific Image Pixels
Change specific image pixels using array indexing to draw shapes or overlay text.
array_sq = np.copy(array)
array_sq[upper:lower, left:right, 1:2] = 0

plt.figure(figsize=(10, 10))
plt.subplot(1, 2, 1)
plt.imshow(array)
plt.title("Original Image")
plt.subplot(1, 2, 2)
plt.imshow(array_sq)
plt.title("Altered Image")
plt.show()


Overlaying Images
Overlay or paste one image over another by reassigning pixel values.
image_lenna = Image.open("lenna.png")
array_lenna = np.array(image_lenna)
array_lenna[upper:lower, left:right, :] = array[upper:lower, left:right, :]

plt.imshow(array_lenna)
plt.title("Overlayed Image")
plt.show()

