# Histogram Equalization Using OpenCV (Grayscale & Color Images)

---

## Aim

To write a Python program using OpenCV to perform histogram equalization on both grayscale and color images to enhance image contrast and brightness.

The program performs the following operations:

- Read and display a grayscale image  
- Plot histogram of the grayscale image  
- Apply histogram equalization on grayscale image  
- Read and display a color image  
- Plot histogram of B, G, R channels  
- Convert image to HSV color space  
- Apply histogram equalization on the Value (V) channel  
- Convert the enhanced image back to BGR format  
- Display original and enhanced images with histograms  

---

## Software Used

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (`cv2`)  
- NumPy  
- Matplotlib  

---

## Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the image `parrot.jpg` in grayscale format.

### Step 3:
Display the grayscale image and plot its histogram.

### Step 4:
Apply histogram equalization using `cv2.equalizeHist()` to enhance contrast.

### Step 5:
Display original grayscale image, its histogram, enhanced image, and its histogram using a 2 × 2 grid.

### Step 6:
Read the same image in color format.

### Step 7:
Split the image into B, G, R channels and plot their histograms.

### Step 8:
Convert the image from BGR to HSV color space.

### Step 9:
Apply histogram equalization on the V (Value) channel.

### Step 10:
Merge the channels and convert the image back to BGR format.

### Step 11:
Display original color image, histogram, enhanced image, and enhanced histogram using a 2 × 2 grid.

---

## Program

### Developed By:
**Name:** EZHIL NEVEDHA K
### Register No:
212223230055
#### Grayscale Histogram Equalization
```
# Import required libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the image in grayscale format
img = cv2.imread('parrot.jpg', 0)

# Check if image is loaded
if img is None:
    print("Error: Image not found!")
    exit()

# Plot histogram of original image
plt.figure(figsize=(8,6))
plt.hist(img.ravel(), 256, [0,256])
plt.title("Histogram of Original Image")
plt.show()

# Perform histogram equalization
equalized_img = cv2.equalizeHist(img)

# Display using 2x2 layout
plt.figure(figsize=(10,8))

# Original Image
plt.subplot(2,2,1)
plt.imshow(img, cmap='gray')
plt.title("Original Grayscale Image")
plt.axis('off')

# Histogram of Original Image
plt.subplot(2,2,2)
plt.hist(img.ravel(), 256, [0,256])
plt.title("Original Histogram")

# Equalized Image
plt.subplot(2,2,3)
plt.imshow(equalized_img, cmap='gray')
plt.title("Enhanced Image")
plt.axis('off')

# Histogram of Equalized Image
plt.subplot(2,2,4)
plt.hist(equalized_img.ravel(), 256, [0,256])
plt.title("Enhanced Histogram")

plt.tight_layout()
plt.show()
```

#### Color Histogram Equalization (HSV Method)
```
# Import required libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the color image
img = cv2.imread('parrot.jpg')

# Check if image is loaded
if img is None:
    print("Error: Image not found!")
    exit()

# Convert BGR to RGB for display
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Plot histogram for B, G, R channels
colors = ('b','g','r')
plt.figure(figsize=(8,6))
for i, col in enumerate(colors):
    hist = cv2.calcHist([img],[i],None,[256],[0,256])
    plt.plot(hist, color=col)
plt.title("Histogram of Original Color Image")
plt.show()

# Convert to HSV
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# Split channels
h, s, v = cv2.split(hsv)

# Equalize only the V channel (brightness)
v_eq = cv2.equalizeHist(v)

# Merge channels
hsv_eq = cv2.merge([h, s, v_eq])

# Convert back to BGR
img_eq = cv2.cvtColor(hsv_eq, cv2.COLOR_HSV2BGR)

# Convert to RGB for display
img_eq_rgb = cv2.cvtColor(img_eq, cv2.COLOR_BGR2RGB)

# Display using 2x2 layout
plt.figure(figsize=(10,8))

# Original Image
plt.subplot(2,2,1)
plt.imshow(img_rgb)
plt.title("Original Color Image")
plt.axis('off')

# Original Histogram
plt.subplot(2,2,2)
for i, col in enumerate(colors):
    hist = cv2.calcHist([img],[i],None,[256],[0,256])
    plt.plot(hist, color=col)
plt.title("Original Histogram")

# Enhanced Image
plt.subplot(2,2,3)
plt.imshow(img_eq_rgb)
plt.title("Enhanced Color Image")
plt.axis('off')

# Enhanced Histogram
plt.subplot(2,2,4)
for i, col in enumerate(colors):
    hist = cv2.calcHist([img_eq],[i],None,[256],[0,256])
    plt.plot(hist, color=col)
plt.title("Enhanced Histogram")

plt.tight_layout()
plt.show()
```
---

##  Output

### Grayscale Histogram Equalization

- Original grayscale image is displayed  
- Histogram of original grayscale image is plotted  
- Enhanced image after histogram equalization is displayed  
- Histogram of enhanced grayscale image shows improved contrast  

### Color Image Histogram Equalization

- Original color image is displayed  
- Histogram of B, G, R channels is plotted  
- Enhanced image after HSV-based equalization is displayed  
- Histogram of enhanced image shows better intensity distribution  

---

## Result

Thus, histogram equalization is successfully performed on both grayscale and color images using OpenCV. The contrast and brightness of the images are significantly improved, enhancing visual quality and feature visibility.
