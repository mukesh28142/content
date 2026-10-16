# Step: Document Scanner Example

## Description

A realistic mini case study walking through how to build a smartphone document-scanning application, from raw photo input to a flattened, cleaned-up output image.

## Type

use_case

## Duration

15m

## Scenario

A student wants to build a simple app that lets a user photograph a paper document with their smartphone camera and automatically turns it into a clean, flat, top-down scan — similar to popular document-scanning apps.

## Pipeline Overview

```text
[ Smartphone Photo ]
        ↓
[ Grayscale Conversion ]
        ↓
[ Gaussian Blur (noise reduction) ]
        ↓
[ Edge Detection (Canny) ]
        ↓
[ Contour Detection ]
        ↓
[ Perspective Transformation ]
        ↓
[ Flattened Document Output ]
```

### Input

The raw input is a photo taken at an angle, often with uneven lighting, some background clutter (a desk, a table edge), and perspective distortion.

### Image Preprocessing

The image is resized to a manageable size and converted to grayscale, since color information is not needed to find the document's edges.

### Grayscale Conversion

```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
blurred = cv2.GaussianBlur(gray, (5, 5), 0)
```

Blurring reduces small text and texture details on the page that might otherwise be mistaken for edges.

### Edge Detection

```python
edges = cv2.Canny(blurred, 75, 200)
```

The Canny algorithm highlights the strong, straight edges of the document against its background.

### Contour Detection

```python
contours, _ = cv2.findContours(edges, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
contours = sorted(contours, key=cv2.contourArea, reverse=True)
document_contour = contours[0]
```

`cv2.findContours()` locates continuous boundary curves in the edge map. Sorting by area and taking the largest contour is a simple, effective way to isolate the document from smaller background shapes.

### Perspective Transformation

Once the four corners of the document are identified from its contour, `cv2.getPerspectiveTransform()` and `cv2.warpPerspective()` are used to "unwarp" the document into a flat, rectangular, top-down view — correcting for the angle the photo was taken at.

### Output

The final output is a clean, flat, rectangular image of just the document, ready for further processing such as OCR (optical character recognition) or saving as a PDF.

### Possible Improvements

- Applying **adaptive thresholding** to improve text contrast in uneven lighting.
- Using a more robust corner-detection approach for documents with rounded or damaged edges.
- Adding automatic **rotation correction** so scanned text is always upright.
- Combining with an OCR engine (such as Tesseract) to extract machine-readable text from the final scan.

![Document Scanner Pipeline](./5 images/Document Scanner Pipeline.png)

---
