# My_YOLO

代码源自： [YOLOv3-Object-Detection-with-OpenCV](https://github.com/iArunava/YOLOv3-Object-Detection-with-OpenCV.git)

参考：
[近距离观察YOLOv3](https://zhuanlan.zhihu.com/p/40332004)
[What’s new in YOLO v3?](https://towardsdatascience.com/yolo-v3-object-detection-53fb7d3bfe6b)

另：Youtube 上 Andrew的CNN课程非常详细

推荐[Convolutional Neural Networks (Course 4 of the Deep Learning Specialization)](https://www.youtube.com/watch?v=ArPaAX_PhIs&list=PLkDaE6sCZn6Gl29AoE31iwdVwSG-KnDzF)。

----

## Strided Convolutions

As for basic NN, the number of inputs should be the same. This restriction is quite inconvenient in our real life because we will often meet pictures in different sizes.

The strided convolutions includes two idea.

* Instead of doing concolutions through the whole picture as one time we actually use a smaller filter to convolute each part of the picture. This is the main idea how we deal with figure with different sizes

* As for calculations, instead of dividing the picuture into several pieces and convolute them seperately, we basically convolute the whole picture altogether. Then what we end up getting is not a 1x1 matrix but a mxm matrix and each cell of the matrix denotes the result for the convolution of a certain piece of  the original picture. This method makes the calculation much faster.

## Object Locolization

Object locolization problem is more complex than object classification problem.

In object classification, we mainly focus on the quesiton "what is the object". In object locolization, our goal becomes "Is there an obeject in the picture? If so, where is it and what is it." Clearly, this task is much more difficult.

For each result it will contain several parts:

* Is there an object, denoted by p.

* The probability of there exist an object in a certain class in this part of the picuture, denoted by ci.
* the size of it, i.e. w(width), h(height), x(the x coordinate of the centroid), y(the y coordinate of the centroid).

## Intersection over union

In practice, chances are that since some parts of the picture share the same area of the picture, those  results might be very similar and actually, they are locolizing the same object. But of course, what we want is for each object there should be only one frame on it. Then we need to pick one result with the greatest probability among those results focusing on one same object.

The idea of intesection over union is calculated with respect to the label. it is simply the ratio of the intersection between predicted frame and the label area over the union of them.

## Nonmax Suppression

This is an algorithm using IOU to omit redundancy results.

## YOLO

YOLO stands for **You Only Look Once**, it basically use those method introduced above to achieve a faster and more accurate object detection.