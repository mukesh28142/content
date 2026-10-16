# Step: Edge Detection and Image Segmentation

## Description

An explanation of image gradients, edge detection, the Canny algorithm, thresholding, and binary images, including why preprocessing is essential before segmentation.

## Type

static_content

## Duration

25m

## Image Gradients

An **image gradient** measures how quickly pixel intensity changes between neighboring pixels. A large gradient usually indicates a sharp change in brightness — which is often the boundary, or **edge**, of an object.

## Edge Detection

*Edge detection* is the process of identifying the boundaries of objects within an image by locating points where brightness changes sharply. Edges are useful because they often correspond to meaningful structure in a scene — the outline of a face, the border of a document, or the shape of a road sign.

### The Canny Edge Detector

The **Canny edge detector**, developed by John F. Canny in 1986, is one of the most widely used edge detection algorithms. Conceptually, it works in several stages:

1. **Noise reduction** — the image is smoothed (typically with Gaussian blur) to reduce false edges caused by noise.
2. **Gradient calculation** — the algorithm computes the intensity gradient at every pixel, capturing both its strength and direction.
3. **Non-maximum suppression** — thin, sharp edges are kept by suppressing pixels that are not local maxima along the gradient direction.
4. **Double thresholding** — pixels are classified as *strong*, *weak*, or *non-edges* based on two threshold values.
5. **Edge tracking by hysteresis** — weak edges connected to strong edges are kept; isolated weak edges are discarded.

```python
import cv2

image = cv2.imread("sample.jpg")
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
blurred = cv2.GaussianBlur(gray, (5, 5), 0)

# Apply Canny edge detection
edges = cv2.Canny(blurred, threshold1=50, threshold2=150)

cv2.imwrite("edges.jpg", edges)
```

The `threshold1` and `threshold2` parameters control the double-thresholding step: pixels above `threshold2` are considered strong edges, pixels below `threshold1` are discarded, and pixels in between are kept only if connected to a strong edge.

## Thresholding and Binary Images

**Thresholding** converts a grayscale image into a **binary image** — one where every pixel is either fully black (`0`) or fully white (`255`) — based on whether its intensity is above or below a chosen cutoff value.

```python
import cv2

gray = cv2.cvtColor(cv2.imread("sample.jpg"), cv2.COLOR_BGR2GRAY)

# Simple binary thresholding
_, binary_image = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)

cv2.imwrite("binary.jpg", binary_image)
```

Binary images are extremely useful in **image segmentation** — the process of separating an image into regions of interest, such as isolating a document from its background.

### Why Preprocessing Matters Here

Noise in an image can create false gradients, which the Canny algorithm may misinterpret as edges. This is why blurring is almost always applied **before** edge detection — clean input leads to clean, meaningful edges rather than a noisy, cluttered result.

| Technique | Purpose | Example |
|---|---|---|
| Gaussian Blur | Reduce noise before edge detection | `cv2.GaussianBlur()` |
| Canny Edge Detection | Identify object boundaries | `cv2.Canny()` |
| Binary Thresholding | Separate foreground from background | `cv2.threshold()` |

![Canny Edge Detection Pipeline](./5 images/Canny Edge Detection Pipeline.png)

---
