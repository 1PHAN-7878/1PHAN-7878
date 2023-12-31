---
title: MATLABQ关于灰度直方图以及一些线性非线性变换？
date: 2023-11-01 20:02:29
tags: MATLAB
---

风和日丽，Q艮又来点任务，这次是让看一看图片（灰度图）的直方分布，加上来然后让这个灰度图像进行一些变换，反正今天讲的叫什么前映射后映射变换是迷迷糊糊的。

这个是编写的康可：

```matlab
img = imread('C:\Users\7878\Desktop\my_image.png');
img1 = imresize(img, 0.3);
img1 = rgb2gray(img1);
subplot(2, 2, 1);
imshow(img1);
subplot(2, 2, 2);
imhist(img1);

img2 = imadjust(img1,[0.5, 0.6], [0, 1]);
subplot(2, 2, 3);
imshow(img2);

subplot(2, 2, 4);
imhist(img2);
```

当使用 `imadjust` 函数时，你可以指定输入图像中要拉伸到特定亮度范围的百分比，并且你可以指定输出图像中的目标亮度范围。这允许你控制亮度值的映射方式，以改变图像的对比度和亮度。

具体来说，这些参数的含义如下：

1. `low_in`：这是输入图像中要拉伸到的亮度范围的下限。它表示输入图像中亮度较低的像素值的百分比。例如，如果 `low_in` 设置为 0.2，表示将输入图像中最暗的 20% 像素值拉伸到目标范围。
2. `high_in`：这是输入图像中要拉伸到的亮度范围的上限。它表示输入图像中亮度较高的像素值的百分比。例如，如果 `high_in` 设置为 0.8，表示将输入图像中最亮的 80% 像素值拉伸到目标范围。
3. `low_out`：这是输出图像中的目标亮度范围的下限。它表示输出图像中最暗的像素值应该对应的亮度值。通常，它是 0，表示黑色。
4. `high_out`：这是输出图像中的目标亮度范围的上限。它表示输出图像中最亮的像素值应该对应的亮度值。通常，它是 1，表示白色。

通过调整这些参数，你可以控制输入图像中不同亮度级别的像素如何映射到输出图像中的亮度范围，从而增强或调整图像的对比度和亮度。这些参数的选择取决于你希望达到的图像效果。



![](../images/qg-1699076069906-1.jpg)
