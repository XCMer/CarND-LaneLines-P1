# **Finding Lane Lines on the Road** 

## Reflection

### 1. Pipeline

The pipeline consists of the following steps:

1. Convert image to grayscale, since canny edge works on the intensity.
1. Apply gaussian blur to the image in preparation of canny edge detection.
1. Apply canny edge detection.
1. Bitmask the region of interest. We do this step before hough transform so that we only get relevant lines from the hough transform.
1. Get lines from the hough transform.
1. Assuming that all the lines from the hough transform are relevant, divide them into left lane and right lane lines. For each lane, get the mean slope and mean offset from the origin for the line. Then, draw just this one line on the screen.
1. Overlay the found lanes on top of the original image.

## 2. Identify potential shortcomings with your current pipeline

### Changing lighting with yellow solid lane

The yellow lane marker sometimes is not visibly distinct in intensity in the grayscale image, under specific lighting conditions. There is a chance that it doesn't get detected at all.

### Cannot deal with a lot of traffic

Due to the amount of edges detected on cars, under high traffic condition, the amount of lane visible might not be enough to confidentally mark and extrapolate lanes.

## 3. Suggest possible improvements to your pipeline

### Do canny edge detection on all the channels in the HSV space

And then, somehow combine them and have them vote on the significant lines.

### Remove outliers on the hough transform output

Since we take a mean of all the lines contributing to a lane, we should remove outliers. Going a bit further, we have check how many lines have similar slope or offset (within a threshold), and use them as votes to decide which one of the "parallel" lines to keep.

### Do RGB normalization

Under different lighting conditions, it's important to somehow normalize the intensity of the things we're looking for.
