# Boundary Detection

## Repository Description
[Study Repo] Used to learn and understand boundary detection using traditional computer vision and deep learning

## Traditional Computer Vision Method

### Theory

Boundary detection is the fundamental process of any computer vision algorithm. One od the most primitive and basic feature of any object in an image is the boundary.
Although it sounds like a simple task, boundary detection from a single image becaomes very difficult unless we have the description of the object. The most basic method
to do boundary detection is to observe the intensity variation in the image but this is susceptible to change in brighness, color, texture and camera view point.
Although we cannot solve all the problems using just one image, we can make use of all the 3 channels (R-G-B) to maximize the probabilty to find all the boundaries in the image.

Classical methods include Canny and Sobel detectors to find the boundaries

### Sobel edge detection

It is a method of kernel convolution to find the edges in the image. It uses two kernels Gx and Gy which calculates the gradient in intensity gradient in x direction and intensity gradient in y direction of the image.

- Convert the image into gray scale (Single channel 0-255)
- Apply gaussian filter to smooth the image
- Convolution operation using Gx filter 
- Convolution operation using Gy filter
- Find the magnitude of gradient for every pixel by using `sqrt(pow(Gx, 2) + pow(Gy, 2))`
- Find the direction of gradient for every pixel by using `atan(Gy/Gx)`

Sobel Kernels

|    | Gx |    |
|----|----|----|
| -1 | -2 | -1 |
| 0  | 0  | 0  |
| 1  | 2  | 1  |

|    | Gy |    |
|----|----|----|
| -1 | 0  | 1  |
| -2 | 0  | 2  |
| -1 | 0  | 1  |

### Canny edge detection

Canny edge detection is a multi stage algorithm which uses gaussian based filter to find the edges in the image. The output if Sobel Filtering is the input to canny esge 
detection.

- Convert the image into gray scale (Single channel 0-255)
- Apply gaussian filter to smooth the image
- Find the oriented intensity gradients just like we did in Sobel
- Use non-max suppression to remove the unnecessary edges determining the same boundary
  - Use the orientation of the gradient for the pixel to select the neighbour pixels in that orientation (We need to thin the edge in the direction of whcih the egde is running)
  - Check if the magnitude of the gradient of the current pixel is greater than the magnitude of gradient of the selected neighbour pixels
  - If greater then we suppress the neighbour pixel and remove them from edge (thinning the edge)
- Apply hysterisis thresholding to find strong edges and get rid of the weaker edges
  - Select the value of upper and lower threshold for the gradient of the edge
  - If the value of gradient at a pixel is greater than the upper threshold then we select that pixel for the edge
  - If the value of gradient at a pixel is lower than the lower thereshold then we rejet that pixel for the edge (Weak edges)
  - If the value of gradient at a pixes is between the upper and lower threshold and the pixel is connected to the strong edge then we select that pixel for the edge
  - Thus, we get rid of the weaker edges









