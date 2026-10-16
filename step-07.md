# Step: OpenCV Knowledge Check

## Description

A five-question multiple-choice quiz covering pixels, color spaces, NumPy array shapes, blurring, and edge detection.

## Type

quiz

## Duration

15m

:::quiz

question: "What does a single pixel in a grayscale image represent?"

options:
  - "A three-channel color value"
  - "A single brightness value, typically between 0 and 255"
  - "The width and height of the image"
  - "A coordinate on the x-axis only"

answer: "A single brightness value, typically between 0 and 255"

explanation: "In a grayscale image, each pixel stores one intensity value ranging from 0 (black) to 255 (white), with no separate color channels."

:::

:::quiz

question: "By default, in what color channel order does OpenCV read images?"

options:
  - "RGB"
  - "BGR"
  - "HSV"
  - "CMYK"

answer: "BGR"

explanation: "OpenCV historically reads and stores color images in BGR (Blue, Green, Red) order rather than the more common RGB order."

:::

:::quiz

question: "What is the correct NumPy array shape for a color image in OpenCV?"

options:
  - "(channels, height, width)"
  - "(width, height, channels)"
  - "(height, width, channels)"
  - "(height, channels, width)"

answer: "(height, width, channels)"

explanation: "OpenCV represents color images as NumPy arrays with the shape (height, width, channels), with height listed before width."

:::

:::quiz

question: "Why is Gaussian blur commonly applied before running Canny edge detection?"

options:
  - "To increase the image's resolution"
  - "To convert the image to a binary format"
  - "To reduce noise that could create false edges"
  - "To change the image's color space to HSV"

answer: "To reduce noise that could create false edges"

explanation: "Noise can produce sharp, misleading intensity changes. Blurring smooths the image first so that Canny detects genuine object boundaries rather than noise artifacts."

:::

:::quiz

question: "Which OpenCV function converts a grayscale image into a black-and-white binary image using a cutoff value?"

options:
  - "cv2.cvtColor()"
  - "cv2.GaussianBlur()"
  - "cv2.threshold()"
  - "cv2.resize()"

answer: "cv2.threshold()"

explanation: "cv2.threshold() compares each pixel's intensity to a specified cutoff value and assigns it fully black or fully white accordingly, producing a binary image."

:::

---
