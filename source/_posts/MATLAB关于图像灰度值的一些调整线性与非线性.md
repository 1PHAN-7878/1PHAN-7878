---
title: MATLAB关于图像灰度值的一些调整线性与非线性
date: 2023-11-08 20:33:50
tags: MATLAB
---

今天Q艮点名，还整的挺彳亍。晚上实验，先用ps的那个图像有个调整灰度分布的曲线，捏着就调整了，挺彳。

作业的话当然不是整理成ps那种的形式太难了。而是一个线性的映射，一个对数的映射。

代码与结果如下：

```matlab
img = imread('C:\Users\7878\Desktop\my_image.png');
img1 = imresize(img, 0.3);
img1 = rgb2gray(img1);
subplot(2, 2, 1);
imshow(img1);
 
[r,c] = size(img1);
 
output_image1 = zeros(size(img1));
 
% 
 
function1 = @(x) x * 1.5;
 
for i=1:r
    for j=1:c
        value = double(img1(i, j));
        output_image1(i, j) = function1(value);
    end
end
 
 
output_image1 = uint8(max(0, min(255, output_image1)));
 
subplot(2,2,2);
imshow(output_image1);
 
% 
% function2 = @(x) (255 / log(256)) * log(1 + x);
% 
% for i=1:r
%     for j=1:c
%         value = double(img1(i, j));
%         if(value == 0) 
%             continue;
%         end
%         output_image1(i, j) = function2(value);
%     end
% end
% 
% 
% output_image1 = uint8(max(0, min(255, output_image1)));
 
subplot(2,2,2);
imshow(output_image1);
 
 
subplot(2,2,3);
imhist(img1);
subplot(2,2,4);
imhist(output_image1);

```

![image-20231108204739001](../images/image-20231108204739001.png)

![image-20231108204744493](../images/image-20231108204744493.png)
