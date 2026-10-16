# Step: Building a Simple Edge Detection Program

## Description

A complete hands-on Python program that reads an image, converts it to grayscale, blurs it, applies Canny edge detection, and saves the result — with a troubleshooting section for common errors.

## Type

hands_on

## Duration

30m

## Complete Edge Detection Program

```python
import cv2
import sys

def detect_edges(input_path: str, output_path: str) -> None:
    # Read the image
    image = cv2.imread(input_path)

    if image is None:
        raise FileNotFoundError(
            f"Could not read image at '{input_path}'. "
            "Check that the file exists and the path is correct."
        )

    # Convert to grayscale
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    # Reduce noise with Gaussian blur
    blurred = cv2.GaussianBlur(gray, (5, 5), 0)

    # Apply Canny edge detection
    edges = cv2.Canny(blurred, threshold1=50, threshold2=150)

    # Save the result
    cv2.imwrite(output_path, edges)
    print(f"Edge-detected image saved to '{output_path}'.")


if __name__ == "__main__":
    detect_edges("sample.jpg", "sample_edges.jpg")
```

### Line-by-Line Explanation

- `cv2.imread(input_path)` attempts to load the image; if the path is wrong or the file is unreadable, it returns `None` rather than raising an error, which is why we check for `None` explicitly.
- `cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)` reduces the image to a single brightness channel, which is all the Canny algorithm needs.
- `cv2.GaussianBlur(gray, (5, 5), 0)` smooths the grayscale image to reduce noise-driven false edges.
- `cv2.Canny(blurred, 50, 150)` performs the full multi-stage Canny algorithm described in the previous step.
- `cv2.imwrite(output_path, edges)` writes the final single-channel edge map to disk.

### Troubleshooting Common Problems

| Problem | Likely Cause | Suggested Fix |
|---|---|---|
| Image not found | `cv2.imread()` returned `None` | Check `if image is None:` and confirm the file exists at that path |
| Incorrect path | Relative path resolved from the wrong working directory | Use an absolute path, or verify the script's current working directory |
| Unsupported image format | Proprietary or unusual file format | Re-export the image to a standard format such as `.jpg` or `.png` |
| Unexpected dimensions | Wrong file loaded (e.g., a thumbnail or cropped copy) | Print `image.shape` early and confirm it matches expectations |

---
