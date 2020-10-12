# **Finding Lane Lines on the Road** 

## Writeup Template


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---



### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...


## Helper Function Study: '20.10/12

### 1. def grayscale(img)
* convert to gray using cv2 member function

### 2. def canny(img, low_th, high_th)
* using cv2 member function .Canny
* It is useful to find edge using gradient

### 3. def gaussian_blur(img, kernel_size)
* using cv2 member function .GaussianBlur

### 4. def region_of_interest(img, vertices)
* mask = np.zeros_like(img) works that make the zero padding image size as img
--- 
if len(img.shape) > 2:
        channel_count = img.shape[2]  # i.e. 3 or 4 depending on your image
        ignore_mask_color = (255,) * channel_count
    else:
        ignore_mask_color = 255
cv2.fillPoly(mask, vertices, ignore_mask_color)
masked_image= cv2.bitwise_and(img,mask)
return masked_image
---
is for making the white (true) image mask. It is used as mask region selection with bitwise_and(img,mask)

### 5. def draw_lines(img, lines, color=[255, 0, 0] , thickness=2)
* draw the line on image

### 6. def hough_lines(img, rho, theta, threshold, min_line_len, max_line_gap)
* Returns an image with hough line drawn
---
lines = cv2.HoughLinesP(img, rho, theta, threshold, np.array([]), minLineLength=min_line_len, maxLineGap=max_line_gap)
    line_img = np.zeros((img.shape[0], img.shape[1], 3), dtype=np.uint8)
    draw_lines(line_img, lines)
    return line_img
---
* hough can find the line 'a' and 'b' domain in 'y=ax+b', not x and y domain

### 7. deg weighted_img(img, initial_img, alpha, beta, gamma) 
---
 """
    `img` is the output of the hough_lines(), An image with lines drawn on it.
    Should be a blank image (all black) with lines drawn on it.
    
    `initial_img` should be the image before any processing.
    
    The result image is computed as follows:
    
    initial_img * α + img * β + γ
    NOTE: initial_img and img must be the same shape!
    """
    return cv2.addWeighted(initial_img, α, img, β, γ)
---
* blend the two image with weighting parameter



## Project Rubric: Finding Lane Lines on the Road: '20.10/12

###Required Files

- Have all project files been included with the submission?

The project submission includes all required files:
* Ipython notebook with code
* A writeup report (either pdf or markdown)


### Lane Finding Pipeline

- Does the pipeline for line identification take road images from a video as input and return an annotated video stream as output?
* The output video is an annotated version of the input video.

- Has a pipeline been implemented that uses the helper functions and / or other code to roughly identify the left and right lane lines with either line segments or solid lines? (example solution included in the repository output: raw-lines-example.mp4)
* In a rough sense, the left and right lane lines are accurately annotated throughout almost all of the video. Annotations can be segmented or solid lines

- Have detected line segments been filtered / averaged / extrapolated to map out the full extent of the left and right lane boundaries? (example solution included in the repository: P1_example.mp4)
* Visually, the left and right lane lines are accurately annotated by solid lines throughout most of the video.

### Reflection

- Has a thoughtful reflection on the project been provided in the notebook?
* Reflection describes the current pipeline, identifies its potential shortcomings and suggests possible improvements. There is no minimum length. Writing in English is preferred but you may use any language.



