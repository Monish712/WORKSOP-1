# WORKSOP-1
# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

## Program & Output :
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceImage = cv2.imread('pic.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```

<img width="317" height="426" alt="image" src="https://github.com/user-attachments/assets/d5c88b75-4034-4cf2-93c9-41d64b845bb5" />

```
glassPNG = cv2.imread('glass.png', cv2.IMREAD_UNCHANGED)
print(glassPNG.shape)
plt.imshow(glassPNG[:, :, ::-1])
plt.title("Sunglasses PNG")
plt.axis("off")
plt.show()
glassBGR = glassPNG[:, :, 0:3]
glassMask1 = glassPNG[:, :, 3]
```
<img width="386" height="372" alt="image" src="https://github.com/user-attachments/assets/7d5981f9-1062-4728-8939-d6b79588fbe7" />

```
plt.figure(figsize=[15,15])
plt.subplot(121)
plt.imshow(glassPNG[:, :, :3][:, :, ::-1])  # BGR → RGB
plt.title('Sunglass Color channels')
glassBGR = glassPNG[:, :, :3]
glassGray = cv2.cvtColor(glassBGR, cv2.COLOR_BGR2GRAY)
_, glassMask1 = cv2.threshold(glassGray, 240, 255, cv2.THRESH_BINARY_INV)
plt.subplot(122)
plt.imshow(glassMask1, cmap='gray')
plt.title('Sunglass Mask (generated)')
plt.show()
```

<img width="1190" height="535" alt="image" src="https://github.com/user-attachments/assets/cbfc5b00-c08e-4615-a04b-a60c7109dc38" />

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceImage = cv2.imread("pic.jpeg")
glassPNG = cv2.imread("glass.png", cv2.IMREAD_UNCHANGED)
new_w = int(faceImage.shape[1] * 0.42)
new_h = int(new_w * glassPNG.shape[0] / glassPNG.shape[1])
glass_resized = cv2.resize(glassPNG, (new_w, new_h))
if glass_resized.shape[2] == 4:
    glassBGR = glass_resized[:, :, 0:3]
else:
    glassBGR = glass_resized
glassGray = cv2.cvtColor(glassBGR, cv2.COLOR_BGR2GRAY)
_, glassMask = cv2.threshold(glassGray, 240, 255, cv2.THRESH_BINARY_INV)
mask_inv = cv2.bitwise_not(glassMask)
x = int((faceImage.shape[1] - new_w) / 2)
y = int(faceImage.shape[0] * 0.15)
x = max(0, min(x, faceImage.shape[1] - new_w))
y = max(0, min(y, faceImage.shape[0] - new_h))
roi = faceImage[y:y+new_h, x:x+new_w]
bg = cv2.bitwise_and(roi, roi, mask=mask_inv)
fg = cv2.bitwise_and(glassBGR, glassBGR, mask=glassMask)
combined = cv2.add(bg, fg)
faceImage[y:y+new_h, x:x+new_w] = combined
plt.figure(figsize=(10, 10))
plt.imshow(cv2.cvtColor(faceImage, cv2.COLOR_BGR2RGB))
plt.title("Face with Sunglasses")
plt.axis("off")
plt.show()
```

<img width="592" height="757" alt="image" src="https://github.com/user-attachments/assets/bbed4c6a-9818-46a3-9968-6d6e15ffb31f" /> 

## Result :
Successfully added and adjusted sunglasses to a passport photo using OpenCV image processing techniques for a fun visual transformation.

