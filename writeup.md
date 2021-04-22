# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.


My pipeline consisted of 6 steps:
>
    gray = grayscale(image)
    blur = gaussian_blur(gray, kernel_size)
    cannyedge = canny(blur, canny_low_threshold, canny_high_threshold)
    roi = region_of_interest(cannyedge, region)
    hough = hough_lines_new(roi, rho, theta, threshold, min_line_length, max_line_gap, thickness)
    layed = weighted_img(hough, image,)

I particualarly developed draw_lines function, as renamed to draw_lines_new in my code.
draw_lines_new's algorithm is as following:
- divide lines to left group and right group
- for each group, sort the lines, find average k and b value and build a new full length line.

![alt text][test_images_output/solidWhiteCurve.jpg]


### 2. Identify potential shortcomings with your current pipeline

Shortcoming 1:
if the first bottom line segment has bad position, it will affect left/right seperation quality badly.

Shortcoming 2:
It can't handle curving lines, typically at far end of the lane


### 3. Suggest possible improvements to your pipeline

A possible improvement for shortcoming 1 would be, use statistic algorithms to identify good line segments, instead of hard rules.
For shortcoming 2, solution should include handling curving segments specifically.
