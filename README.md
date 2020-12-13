# Image Processing Practice 101 By Sajid ( Image To Sketch Conversion )

# Step 1: Importing Libraries Of Numpy and OpenCV


```python
import numpy as np
import cv2
```

# Step 2: Reading Image File


```python
photo = "image.jpg"
photo_obj = cv2.imread(photo)
```

# Step 3: Checking Shape Of The Image


```python
photo_obj.shape
```




    (818, 620, 3)



# Step 4: Shrinking The Image


```python
scale_percent = 0.60
width = int(photo_obj.shape[1]*scale_percent)
height = int(photo_obj.shape[0]*scale_percent)
```


```python
dim = (width, height)
```


```python
resized = cv2.resize(photo_obj, dim, interpolation = cv2.INTER_AREA)
```

# Step 5: Checking After Resizing To Compare With Previous One


```python
cv2.imshow('original image', photo_obj)
cv2.imshow('resized image', resized)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

# Step 6: Sharpening Of The Image


```python
kernel_sharpening = np.array ([[-1,-1,-1],
                               [-1, 9,-1],
                               [-1,-1,-1]])
sharpened = cv2.filter2D(resized,-1,kernel_sharpening)
```


```python
cv2.imshow('sharp', sharpened)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

# Step 7: Changing Color Of The Image


```python
gray = cv2.cvtColor(sharpened, cv2.COLOR_BGR2GRAY)
object_detection = cv2.cvtColor(sharpened, cv2.COLOR_BGR2HSV)
```


```python
cv2.imshow('gray', gray)
cv2.imshow('object_detection', object_detection)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

# Step 8: Inversing & Blurring The Image


```python
inv = 255-gray
gauss = cv2.GaussianBlur(inv, ksize=(15,15), sigmaX=0, sigmaY=0)
```

# Step 9: Making It Into Pencil Sketch


```python
pencil = cv2.divide(gray,255-gauss,scale=256)
cv2.imshow('pencil', pencil)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

# Step 10: Showing All The Versions Of The Image Together


```python
cv2.imshow('resized image', resized)
cv2.imshow('sharp', sharpened)
cv2.imshow('gray', gray)
cv2.imshow('pencil', pencil)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
