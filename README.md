# Edge Detection on checkerboard
The goal of this project is to detect the edges in a checkerboard and highlight them with a green line superimposed on the image.
# 1 Tool preparation
## 1.1 Used tools
The project has been developed using Python and open source libraries. In particular it's been used:
* Python 3.7.3
* OpenCV 
* Numpy 
* Argparse 
* Abstract Syntax Trees

## 1.2 Testing Data
The *Data* folder include five pictures of chessboard. Each of them has different degree of noise and rotation.
![Figure_1](https://user-images.githubusercontent.com/38732983/72232658-cf88d480-35c2-11ea-9857-ba8e749ada43.png)

# 2 Implementation 
## 2.1 Noise Reduction
Since the mathematics involved behind the edge detection are mainly based on derivatives, the results are highly sensitive to image noise. One way to remov the noise on the image, is by applying filter to smooth it. To do so, image convolution technique can be applied with different Kernel. 
There are four common filters for noise removal:
1. Averaging :  
It takes the average of all the pixels under the kernel area and replaces the central element. 
2. Gaussian :  
It is  generated by convolving an image with a kernel of Gaussian values and it is commonly used with edge detection. 
3. Median :  
The central element is always replaced by some pixel value in the image. It reduces the noise effectively. However, it reduced th corner of the chessboard too much.
4. Bilateral :  
Compared to the three filters above, it is more effective in smoothing while keeping edges sharp. The others filters tend to blur the edges.

Self-defined kernel can also be applied. The kernek should be stored in a tuple such as ([ 0.0625, 0.125, 0.0625 ],[ 0.125, 0.25, 0.125 ],[ 0.0625, 0.125, 0.0625]) . 

## 2.2 Threshold
Threshold is used to detect the edges more clearly when the checkerboard is not a black and white picture. 
![Figure_3](https://user-images.githubusercontent.com/38732983/72281338-9c822780-363a-11ea-839d-9afd91e1fdc3.png)
## 2.3 edge detection
Edge detection aims to find the boundaries of objects within images.
There are three common algorithm for edges detection:
1. Laplace : calculates second order derivatives in a single pass. 
2. Sobel : calculates the first derivatives of the image separately for the X and Y axes.
3. Canny : uses a multi-stage algorithm (five steps: 	1. Gaussian filter  2. Finding the intensity gradient of the image  3. Non-maximum suppression  4. Double threshold  5. Edge tracking by hysteresis)

# 3 Run the Project
## 3.1 Installation
In order to run the python file, the following packages must be installed.
```
# pip 
sudo easy_install pip
   
# OpenCV (cv2)
pip install opencv-python

# Numpy
pip install numpy

# Argparse 
pip install argparse
```
## 3.2 Run the Program
Launch the python edge_detector.py with the following parameters:
```
input 
--filter
--kernel
--detector
```
By default launching only python edge_detector.py with an input image, the script use the Bilateral filter for noise removal and Canny for the edge detection. Bilateral works better when we need to preserve the edges. Canny is considered to be a better algorithm because of the steps [Non Maximum Suppression] and [Hysteresis Process].  
With --filter you can choose which filter to use between Averaging, Gaussian, Median and Bilateral. With --kernel you can provide a kernel stored in a string such as '([0.06, 0.1, 0.06],[0.1, 0.36, 0.1],[0.06, 0.1, 0.06])'. With --detector you can choose which edge detection technique to use between Laplace, Sobel and Canny.
The output image will be stored in the *output* folder.

**Usage example**   
`cd {project_folder/src}`  
`python edge_detector.py '../data/Image_5.jpg' --filter 'Gaussian'`
`python edge_detector.py '../data/Image_3.png'`
`python edge_detector.py '../data/Image_2.png' --filter None --kernel '([0.06, 0.1, 0.06],[0.1, 0.36, 0.1],[0.06, 0.1, 0.06])'`

# Conclusion (possible improvements)
1. The improvement of noise reduction  
When there is noise around the edges of the squares in the checkerboard, it's sometimes doesn't get smoothed properly after the noise removal. We can try to figure out a kernel for noise reduction or an algorithm for sharpen the edges.
2. The straight edges  
The edges of a chessboard should ideally be straight lines. Hough Line transformation can be a way for detecting lines after edges detection. To do this properly, we might need to define the minimum line length. The method to measure the length is to find the corner of the square and calculate the distance between points. The accuracy of Hough Line transformation is also sensitive to noise reduction.






