# Step: Understanding Images in OpenCV

## Description

An introduction to OpenCV and computer vision, covering how digital images are represented as pixels and NumPy arrays, the difference between grayscale and color images, and core OpenCV terminology.

## Type

static_content

## Duration

25m

## What is OpenCV?

**OpenCV** (Open Source Computer Vision Library) is a free, open-source library used to build applications that can *see* and interpret images and video. It was originally developed by Intel and has since become the most widely used computer vision library in both industry and research.

> "Computer vision is the science of enabling computers to interpret and understand visual information from the world, much the same way human vision does."

OpenCV provides ready-made tools for tasks such as:

- Reading and writing images and video
- Filtering and transforming images
- Detecting edges, shapes, and objects
- Tracking motion across video frames
- Working with 3D vision and camera calibration

It has bindings for several languages, but this lesson focuses on **Python**, since it is the most common entry point for beginners.

## What is Computer Vision?

*Computer vision* is a field of artificial intelligence that trains computers to extract meaningful information from digital images and videos, and then to take actions or make decisions based on that information. A self-driving car recognizing a stop sign, a phone unlocking via face recognition, and a factory camera spotting a defective part are all examples of computer vision in action.

## How Digital Images Are Represented

A digital image is not a continuous picture the way a painting is — it is a grid of small squares called **pixels** (short for "picture elements"). Each pixel holds a numeric value that represents color or brightness at that point in the image.

### Pixels and Image Dimensions

An image's dimensions are usually described as `width x height`, measured in pixels. For example, an image that is 1920 pixels wide and 1080 pixels tall is described as a `1920x1080` image.

The total number of pixels in an image can be expressed mathematically as:

$$
\text{Total Pixels} = \text{width} \times \text{height}
$$

So a `1920x1080` image contains:

$$
1920 \times 1080 = 2{,}073{,}600 \text{ pixels}
$$

This total pixel count is closely related to an image's **resolution** — higher resolution generally means more pixels, and therefore more detail, at the cost of a larger file size.

### Grayscale Images

A **grayscale image** stores only brightness information for each pixel — no color. Each pixel is typically represented by a single number ranging from `0` (black) to `255` (white), with values in between representing shades of gray.

### RGB and BGR Representation

A **color image** typically stores three numeric values per pixel, one for each of the *Red*, *Green*, and *Blue* channels. Combining different intensities of these three channels can produce millions of distinct colors.

One important quirk to remember: while most image libraries and web standards use the **RGB** channel order, OpenCV uses **BGR** (Blue, Green, Red) by default when reading images. This is a historical convention from OpenCV's early development and frequently trips up beginners who forget to account for it when combining OpenCV with other libraries.

### Image Channels

The term **channel** refers to one layer of an image's color information:

- A grayscale image has **1 channel**.
- A standard color image has **3 channels** (Blue, Green, Red in OpenCV).
- Some images include a 4th **alpha channel**, which controls transparency.

### Images as NumPy Arrays

Internally, OpenCV represents every image as a **NumPy array** — a multi-dimensional grid of numbers provided by the `numpy` library. Understanding this is essential, because almost everything you do with an image in OpenCV is really an array operation.

A color image is represented as an array with the shape:

```python
(height, width, channels)
```

For example, a `1920x1080` color image would have the shape `(1080, 1920, 3)`. Note that **height comes before width** in this shape — another common source of confusion for beginners.

You can inspect an image's shape directly with `image.shape`, and its data type (usually `uint8`, meaning unsigned 8-bit integers from 0–255) with `image.dtype`.

![OpenCV Image Representation](../images/opencv-image-representation.png)

### Basic OpenCV Terminology

A short glossary of terms you will see throughout this lesson:

1. **Pixel** — the smallest unit of a digital image, holding one or more numeric values.
2. **Channel** — one layer of color/brightness data (e.g., Blue, Green, or Red).
3. **Resolution** — the number of pixels in an image, usually given as width × height.
4. **Array** — the NumPy data structure OpenCV uses to store image data.
5. **Kernel** — a small matrix used in filtering operations such as blurring.
6. **Contour** — a curve that follows the boundary of shapes in an image.

Key points to remember before moving on:

- Images are grids of pixels stored as NumPy arrays.
- OpenCV uses `BGR`, not `RGB`, by default.
- Grayscale images have 1 channel; color images typically have 3.
- Array shape is `(height, width, channels)`.

---
