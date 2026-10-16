# Step: Hands-on Image Processing with OpenCV

## Description

A guided, hands-on coding walkthrough where the learner loads an image, inspects its dimensions, converts it to grayscale, resizes it, applies Gaussian blur, and saves the processed result.

## Type

hands_on

## Duration

30m

## Walkthrough: Basic Image Processing Pipeline

In this hands-on exercise, you will build a small pipeline that performs several common preprocessing steps in sequence.

### Step-by-Step Instructions

1. **Load an image** using `cv2.imread()`.
2. **Check its dimensions** using `.shape`.
3. **Convert it to grayscale** using `cv2.cvtColor()`.
4. **Resize it** using `cv2.resize()`.
5. **Apply Gaussian blur** using `cv2.GaussianBlur()`.
6. **Save the processed image** using `cv2.imwrite()`.

### Complete Code

```python
import cv2

# 1. Load an image
image = cv2.imread("sample.jpg")

if image is None:
    raise FileNotFoundError("Could not load 'sample.jpg'. Check the file path.")

# 2. Check its dimensions
height, width, channels = image.shape
print(f"Width: {width}, Height: {height}, Channels: {channels}")

# 3. Convert it to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# 4. Resize it (to half its original size)
resized_image = cv2.resize(gray_image, (width // 2, height // 2))

# 5. Apply Gaussian blur to reduce noise
blurred_image = cv2.GaussianBlur(resized_image, (5, 5), 0)

# 6. Save the processed image
cv2.imwrite("processed_sample.jpg", blurred_image)

print("Processing complete. Saved as 'processed_sample.jpg'.")
```

### Code Explanation

- `cv2.imread("sample.jpg")` loads the image into memory as a NumPy array. Checking for `None` guards against a missing or unreadable file.
- `image.shape` unpacks into `height`, `width`, and `channels`, confirming the image was loaded correctly.
- `cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)` converts the 3-channel BGR image into a single-channel grayscale image.
- `cv2.resize(gray_image, (width // 2, height // 2))` halves the image dimensions, which is useful for reducing processing time.
- `cv2.GaussianBlur(resized_image, (5, 5), 0)` smooths the image using a `5x5` kernel, which helps reduce noise before further processing such as edge detection.
- `cv2.imwrite(...)` writes the final result to disk.

### Expected Output

```text
Width: 1920, Height: 1080, Channels: 3
Processing complete. Saved as 'processed_sample.jpg'.
```

A new file, `processed_sample.jpg`, will appear in your working directory: a smaller, blurred, grayscale version of the original image.

### Practical Exercise

Using the code above as a starting point, modify the script so that it:

- Resizes the image to exactly `400x400` pixels instead of half its original size, and
- Applies a stronger blur using a `9x9` kernel instead of `5x5`.

Save your modified image as `exercise_output.jpg` and compare it visually to `processed_sample.jpg`.

![Image Processing Pipeline](./5 images/Image Processing Pipeline.png)

---
