# EXP - 3 HISTOGRAM EQUILIZATION USING OPEN CV (GRAYSCALE AND COLOR IMAGES)

---

## Aim:

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

## Software Used:

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (`cv2`)  
- NumPy  
- Matplotlib  

---

## Algorithm:

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

## Program:

### Developed By:
**Name:** R P Loshini
**Register No:** 212225230155

#### Grayscale Histogram Equilisation
```
import cv2
import numpy as np
import matplotlib.pyplot as plt

image_path = r"C:\Users\acer\DIPT\parrot.jpg"

# Step 2: Read the image parrot.jpg in grayscale format
gray_img = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)

# Step 3: Display the grayscale image and plot its histogram (Intermediate visualization)
# Step 4: Apply histogram equalization using cv2.equalizeHist() to enhance contrast
equalized_gray = cv2.equalizeHist(gray_img)

# Step 5: Display original grayscale image, its histogram, enhanced image, and its histogram using a 2 x 2 grid
fig, axes = plt.subplots(2, 2, figsize=(12, 8))

# 1. Original Grayscale Image
axes[0, 0].imshow(gray_img, cmap='gray')
axes[0, 0].set_title("Original Grayscale Image")
axes[0, 0].axis('off')

# 2. Histogram of Original Grayscale Image
axes[0, 1].hist(gray_img.ravel(), bins=256, range=[0, 256], color='black')
axes[0, 1].set_title("Original Grayscale Histogram")
axes[0, 1].set_xlim([0, 256])

# 3. Enhanced Grayscale Image
axes[1, 0].imshow(equalized_gray, cmap='gray')
axes[1, 0].set_title("Enhanced Grayscale Image")
axes[1, 0].axis('off')

# 4. Histogram of Enhanced Grayscale Image
axes[1, 1].hist(equalized_gray.ravel(), bins=256, range=[0, 256], color='black')
axes[1, 1].set_title("Equalized Grayscale Histogram")
axes[1, 1].set_xlim([0, 256])

plt.tight_layout()
plt.show()
```

#### BGR Channel Histograms
```
# Step 6: Read the same image in color format
color_img = cv2.imread(image_path)

# Step 7: Split the image into B, G, R channels and plot their histograms
b, g, r = cv2.split(color_img)

plt.figure(figsize=(10, 5))
plt.title("RGB Channel Histograms")
plt.xlabel("Pixel Intensity Value (0 - 255)")
plt.ylabel("Pixel Count")

colors = ('b', 'g', 'r')
channel_labels = ('Blue Channel', 'Green Channel', 'Red Channel')

for i, col in enumerate(colors):
    hist = cv2.calcHist([color_img], [i], None, [256], [0, 256])
    plt.plot(hist, color=col, label=channel_labels[i])

plt.xlim([0, 256])
plt.legend()
plt.show()
```

#### Color Image HSV Histogram Equilisation
```
# Step 8: Convert the image from BGR to HSV color space
hsv_img = cv2.cvtColor(color_img, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv_img)

# Step 9: Apply histogram equalization on the V (Value) channel
v_equalized = cv2.equalizeHist(v)

# Step 10: Merge the channels and convert the image back to BGR format
hsv_equalized = cv2.merge((h, s, v_equalized))
enhanced_color_bgr = cv2.cvtColor(hsv_equalized, cv2.COLOR_HSV2BGR)

# Convert BGR images to RGB format for Matplotlib rendering
color_img_rgb = cv2.cvtColor(color_img, cv2.COLOR_BGR2RGB)
enhanced_color_rgb = cv2.cvtColor(enhanced_color_bgr, cv2.COLOR_BGR2RGB)

# Step 11: Display original color image, histogram, enhanced image, and enhanced histogram using a 2 x 2 grid
fig, axes = plt.subplots(2, 2, figsize=(12, 8))

# 1. Original Color Image
axes[0, 0].imshow(color_img_rgb)
axes[0, 0].set_title("Original Color Image")
axes[0, 0].axis('off')

# 2. Histogram of Original V-Channel
axes[0, 1].hist(v.ravel(), bins=256, range=[0, 256], color='gray')
axes[0, 1].set_title("Original V-Channel Histogram")
axes[0, 1].set_xlim([0, 256])

# 3. Enhanced Color Image
axes[1, 0].imshow(enhanced_color_rgb)
axes[1, 0].set_title("Enhanced Color Image (HSV Equalized)")
axes[1, 0].axis('off')

# 4. Histogram of Equalized V-Channel
axes[1, 1].hist(v_equalized.ravel(), bins=256, range=[0, 256], color='gray')
axes[1, 1].set_title("Equalized V-Channel Histogram")
axes[1, 1].set_xlim([0, 256])

plt.tight_layout()
plt.show()
```

---

##  Output:

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

<img width="1078" height="722" alt="image" src="https://github.com/user-attachments/assets/ae4aa4de-1455-42f8-9dae-2faf6ec21fe9" />
<img width="875" height="450" alt="image" src="https://github.com/user-attachments/assets/ef0b238d-7c21-4f98-91be-3193dd91fd76" />
<img width="1078" height="726" alt="image" src="https://github.com/user-attachments/assets/59f9b3b8-ab14-4b43-8f17-f29e699b425a" />


---

## Result:

Thus, histogram equalization is successfully performed on both grayscale and color images using OpenCV. The contrast and brightness of the images are significantly improved, enhancing visual quality and feature visibility.
