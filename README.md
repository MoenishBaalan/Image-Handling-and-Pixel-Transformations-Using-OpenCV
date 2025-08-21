# Image-Handling-and-Pixel-Transformations-Using-OpenCV 
### Name: Moenish Baalan G
### Reg no: 212223220057
### Date of submission: 21.08.2025
## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** Moenish Baalan G
- **Reg no:** 212223220057

 ```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### 1. Read grayscale image
```python
img_gray = cv2.imread('Eagle_in_Flight.jpg', cv2.IMREAD_GRAYSCALE)
```

### 2. Print width, height & channels
```python
h, w = img_gray.shape
print(f"Width: {w}, Height: {h}, Channels: 1")
```

### 3. Display grayscale
```python
plt.imshow(img_gray, cmap='gray')
plt.axis('off')
plt.show()
```

### 4. Save PNG
```python
cv2.imwrite('Eagle_gray.png', img_gray)
```

### 5. Read saved image as color
```python
img_color = cv2.imread('Eagle_gray.png')
```

### 6. Display color & print
```python
h, w, c = img_color.shape
print(f"Width: {w}, Height: {h}, Channels: {c}")
plt.imshow(cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB))
plt.axis('off')
plt.show()
```

### 7. Crop eagle (example coords)
```python
eagle_crop = img_color[50:420,200:570]
plt.imshow(eagle_crop)
plt.axis('off')
plt.show()
```

### 8. Resize 2x
```python
resized = cv2.resize(cropped, None, fx=2, fy=2)
plt.imshow(cv2.cvtColor(resized, cv2.COLOR_BGR2RGB))
plt.axis('off')
plt.show()
```

### 9. Flip horizontally
```python
flipped = cv2.flip(resized, 1)
plt.imshow(cv2.cvtColor(flipped, cv2.COLOR_BGR2RGB))
plt.axis('off')
plt.show()
```

### 10. Read Apollo image
```python
apollo = cv2.imread('Apollo-11-launch.jpg')
```

### 11. Add text
```python
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN
text_size = cv2.getTextSize(text, font_face, 2, 2)[0]
text_x = (apollo.shape[1] - text_size[0]) // 2
text_y = apollo.shape[0] - 20
cv2.putText(apollo, text, (text_x, text_y), font_face, 2, (255, 255, 255), 2)
```

### 12. Draw magenta rectangle
```python
cv2.rectangle(apollo, (100, 50), (300, 500), (255, 0, 255), 3)
```

### 13. Display Apollo
```python
plt.imshow(cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB))
plt.axis('off')
plt.show()
```

### 14. Read boy image
```python
boy = cv2.imread('boy.jpg')
```

### 15. Brightness matrix
```python
matrix_ones = np.ones(boy.shape, dtype=np.uint8) * 50
```

### 16. Brighter & darker
```python
img_brighter = cv2.add(boy, matrix_ones)
img_darker = cv2.subtract(boy, matrix_ones)
```

### 17. Show brightness
```python
plt.subplot(1,3,1); plt.imshow(cv2.cvtColor(boy, cv2.COLOR_BGR2RGB)); plt.axis('off'); plt.title('Original')
plt.subplot(1,3,2); plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB)); plt.axis('off'); plt.title('Darker')
plt.subplot(1,3,3); plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB)); plt.axis('off'); plt.title('Brighter')
plt.show()
```

### 18. Contrast images
```python
img_higher1 = cv2.convertScaleAbs(boy, alpha=1.1, beta=0)
img_higher2 = cv2.convertScaleAbs(boy, alpha=1.2, beta=0)
```

### 19. Show contrast
```python
plt.subplot(1,3,1); plt.imshow(cv2.cvtColor(boy, cv2.COLOR_BGR2RGB)); plt.axis('off'); plt.title('Original')
plt.subplot(1,3,2); plt.imshow(cv2.cvtColor(img_higher1, cv2.COLOR_BGR2RGB)); plt.axis('off'); plt.title('Contrast 1.1x')
plt.subplot(1,3,3); plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB)); plt.axis('off'); plt.title('Contrast 1.2x')
plt.show()
```

### 20. Split BGR
```python
b, g, r = cv2.split(boy)
plt.subplot(1,3,1); plt.imshow(b, cmap='gray'); plt.axis('off'); plt.title('Blue')
plt.subplot(1,3,2); plt.imshow(g, cmap='gray'); plt.axis('off'); plt.title('Green')
plt.subplot(1,3,3); plt.imshow(r, cmap='gray'); plt.axis('off'); plt.title('Red')
plt.show()
```

### 21. Merge BGR
```python
merged_bgr = cv2.merge((b, g, r))
plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB))
plt.axis('off')
plt.show()
```

### 22. Split HSV
```python
hsv_img = cv2.cvtColor(boy, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv_img)
plt.subplot(1,3,1); plt.imshow(h, cmap='gray'); plt.axis('off'); plt.title('Hue')
plt.subplot(1,3,2); plt.imshow(s, cmap='gray'); plt.axis('off'); plt.title('Saturation')
plt.subplot(1,3,3); plt.imshow(v, cmap='gray'); plt.axis('off'); plt.title('Value')
plt.show()
```

### 23. Merge HSV
```python
merged_hsv = cv2.merge((h, s, v))
hsv_to_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)
plt.imshow(cv2.cvtColor(hsv_to_bgr, cv2.COLOR_BGR2RGB))
plt.axis('off')
plt.show()
```

## Output:
- **i)** Read and Display an Image.  
- **ii)** Adjust Image Brightness.  
- **iii)** Modify Image Contrast.  
- **iv)** Generate Third Image Using Bitwise Operations.

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.
