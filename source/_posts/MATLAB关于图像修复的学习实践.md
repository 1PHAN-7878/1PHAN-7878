---
title: MATLAB关于图像修复的学习实践
date: 2023-12-06 20:03:04
tags: MATLAB
---

# 任务需求

天气怎么又有点暖和了，今天学了图像修复，以及图像的恢复。这两个貌似很相似，不过一个是对于噪声的，一个是直接把图片的一部分给扣走。晚上的任务是，能否自己实现一个图像补全，图像修复？

# 查询资料

图像补全，即是将图片中缺失的像素补充上, 目的是使得没有看过这原图像的观察者无法察觉出这其实是补全的图像。 有时为了移除图像中的一些物体, 会手动地将这些物体遮挡起来进行补全。 一般来说, 按照补全的难易程度可以将该问题分成两类: (1) 补全较小的区域 —— 细缝, 文字等; (2)补全较大的区域 —— 整块的缺失图片。

![image-20231206200659347](../images/image-20231206200659347.png)

![image-20231206200706653](../images/image-20231206200706653.png)不过的话，这样看起来简单，其实是不太好做，这上面两张图是中科院研究所做的。我的话，想的是看看MATLAB中是否有类似的函数等可以使用。

方法大致如下：

![image-20231206201027274](../images/image-20231206201027274.png)

# 实现

```matlab
img = imread('C:\Users\7878\Desktop\my_image.png');
img1 = imresize(img, 0.3);
img1 = rgb2gray(img1);

% 定义缺失块的位置和大小
missingBlockPosition = [400, 250];
missingBlockSize = [50, 50];

% 制作掩码，将缺失块区域置零
mask = ones(size(img1));
mask(missingBlockPosition(1):missingBlockPosition(1)+missingBlockSize(1)-1, ...
     missingBlockPosition(2):missingBlockPosition(2)+missingBlockSize(2)-1) = 0;
 
img1 = img1 .* uint8(mask);
inversemask = ~mask;
% reconstructedImage = inpaint_nans(img1, mask);
% reconstructedImage = fillmissing(img1, 'linear');
reconstructedImage = regionfill(img1, inversemask);
% 显示结果
figure;
subplot(1, 2, 1), imshow(img1), title('Original Image');
subplot(1, 2, 2), imshow(reconstructedImage), title('Reconstructed Image'); 
```

效果：

![image-20231206200844084](../images/image-20231206200844084.png)

对于这种与周围区别不大的图像，确实能够有一定的效果，也是补全了黑色的区域。
