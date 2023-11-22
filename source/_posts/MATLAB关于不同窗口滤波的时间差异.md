---
title: MATLAB关于不同窗口滤波的时间差异
date: 2023-11-22 20:13:14
tags: MATLAB
---

# 任务要求

今日寒潮降温，Q粿讲了讲规格化的图像处理，留到下节课做，这节课就做一做MATLAB中对于不同的滑动卷积窗口比如说三乘三，五乘五，还有更大的窗口，看看运算时间的差异。

于是是学习了imfilter滤波函数以及tictok的计时方法

# 代码如下

```matlab
% 读取图像并调整大小和灰度
img = imread('C:\Users\7878\Desktop\my_image.png');
img1 = imresize(img, 0.4);
img1 = rgb2gray(img1);

% 创建子图
subplot(3,2,1);
set(gcf, 'Position', [0 0 1000 800])  % 设置窗口大小
imshow(img1);
set(gca, 'Position', [ 0 2/3 1/3 1/3]);  % 设置子图1位置和大小
[r,c] = size(img1);

% 定义不同的滤波器
filter3 = ones(3,3)/(3*3);
filter5 = ones(5,5)/(5*5);
filter15 = ones(15,15)/(15*15);
filter35 = ones(35,35)/(35*35);

% 对图像进行不同尺寸的均值滤波，并计算时间
tic
result1 = imfilter(img1, filter3, 'conv', 'replicate');  % 对图像进行3*3均值滤波
time1 = toc;
disp(' 3*3 时间' + time1);
subplot(3,2,2);
set(gca, 'Position', [ 1/2 2/3 1/3 1/3]);  % 设置子图2位置和大小
imshow(result1);

tic
result2 = imfilter(img1, filter5, 'conv', 'replicate');  % 对图像进行5*5均值滤波
time2 = toc;
disp(' 5*5 时间' + time2);
subplot(3,2,3);
imshow(result2);
set(gca, 'Position', [ 0 1/3 1/3 1/3]);  % 设置子图3位置和大小

tic
result3 = imfilter(img1, filter15, 'conv', 'replicate');  % 对图像进行15*15均值滤波
time3 = toc;
disp(' 15*15 时间' + time3);
subplot(3,2,4);
imshow(result3);
set(gca, 'Position', [ 1/2 1/3 1/3 1/3]);  % 设置子图4位置和大小

tic
result4 = imfilter(img1, filter35, 'conv', 'replicate');  % 对图像进行35*35均值滤波
time4 = toc;
disp(' 35*35 时间' + time4);
subplot(3,2,5);
imshow(result4);
set(gca, 'Position', [ 0 0 1/3 1/3]);  % 设置子图5位置和大小
```

# 效果如下

![image-20231122202258741](../images/image-20231122202258741.png)
