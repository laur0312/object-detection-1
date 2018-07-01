# Shape Recognition

![Example 1](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/example1.png  "Example 1")

![Example 2](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/example2.png  "Example 2")

![Example 3](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/example3.png  "Example 3")

![Example 4](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/example4.png  "Example 4")

![Example 5](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/example5.png  "Example 5")

A tool used for recognising and counting the number of occurrences
 of four different shapes (i.e. square, rectangle, circle, triangle) in a given image. 
 [Easily scalable in terms of new shapes]

The tool takes an image path as input, and returns three
 comma separated integers as output:
```
<int>,<int>,<int>
```
Where the first integer corresponds to the number of **squares**
 in the image, the second integer corresponds to the number of **circles**,
  and the third integer corresponds to the number of **triangles**.

## How to Run
Download the requirements:
```bash
pip3 install -r requirements.txt 
```
**To run the main tool**
```bash
python3 shapes_counter.py -i <image_path>
```
##### example
```bash
python3 shapes_counter.py -i training_data/001979900122A9-0017558-00101E4-001F3DE-00118C8001FC1B0016C37.jpg
```

and you can also run **the visualization tool** with any image to see the visual edits and effects happened in the picture
```bash
python3 evaluation/visualization.py  -i <image_path>
```
#### example
```bash
python3 evaluation/visualization.py  -i training_data/00170820010925-001146F-0011FF9-001E987-0019C5D001A322001AEF8.jpg
```

## Algorithm
I'm using simple image processing techniques using OpenCV-Python, the algorithm steps:
1. Do image preprocessing and reduce the noise.
2. Select the contours from the image.
3. Select the core approximate corners from each contour.
4. Determine the shape of the main contour; based on its number of vertices.
5. Draw the picture with its shapes tagged by their types.
6. Count the shapes occupancies and print the numbers, comma separated.

I tried to use a training dataset of a lot of labeled pictures, but I had two issues:
1. Te labeling technique seems to be not so useful for me; as if I know exactly the shapes in the picture but I don't know their places, then I can not use this info.
2. I didn't find a lot of papers discussing geometric shapes recognition using machine learning and advanced models, most of them are using contours detection and edge detection.
 
## Results
The results are not bad at all! a lot of test cases gonna be true, the algorithm can pass a lot of corner cases.

![Example 1](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/1.png  "Example 1") ![Example 2](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/2.png  "Example 2")
![Example 3](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/3.png  "Example 3") ![Example 4](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/4.png  "Example 4")
![Example 5](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/5.png  "Example 5") ![Example 6](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/6.png  "Example 6")
![Example 7](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/7.png  "Example 7") ![Example 8](https://github.com/AbdelrahmanRadwan/object-detection/blob/master/results/8.png  "Example 8")


**On the other side, the algorithm fails in some cases:**
1. With small shapes (very small).
2. With the unioned shapes.
3. With objects on the image boarders.

- Tried [image denoising](http://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_photo/py_non_local_means/py_non_local_means.html), but didn't work well:

- Tried [Canny edge detection](http://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_canny/py_canny.html), didn't work well:

- Tried the [Non-local Means Denoising](http://www.bogotobogo.com/python/OpenCV_Python/python_opencv3_Image_Non-local_Means_Denoising_Algorithm_Noise_Reduction.php), didn't work well:

- Tried the [Median Filter](https://code.tutsplus.com/tutorials/image-filtering-in-python--cms-29202), and it works well in preprocessing the image.

- Tried [contours detection](https://www.youtube.com/watch?v=hrwsHlKqBRw) and it works well.


## Furthur work
1. As a post processing step, we need to sharpen the shapes after the preprocessing phase, to avoid minimizing the shape which leads to unrecognizable shape with hard to detect edges.
2. As a post processing step, we need to separate the shapes from each others and from the boarders if they are hardly connected together.

