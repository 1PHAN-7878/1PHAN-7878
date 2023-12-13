---
title: MATLAB关于图像傅里叶变换以及滤波的初探
date: 2023-12-13 20:02:21
tags: MATLAB
---

# 任务要求

今天雪下的巨大，学的傅里叶变换（单独的还是明白了，但是怎么让他们跟图像放在一起）形成了低频和高频（我理解低频和高频是像素值变化的剧烈程度），对图像做了傅里叶变换，把低频的拿到了中间，应该叫移动，再用掩膜给他盖起来。比如我盖住了高频的，那么只有低频的进行复原，也就是说是个低通滤波器，反之就是个高通滤波器。

如此说来，高通滤波器下，变化剧烈的像素被保留，就能够获得轮廓。

# 代码

```matlab
img = imread('C:\Users\7878\Desktop\my_image.png');
img1 = imresize(img, 0.3);
img1 = rgb2gray(img1);
img1 = im2double(img1);



subplot(2, 3, 1);
imshow(img1);
fftimg1 = fft2(img1);
sfftimg1 = fftshift(fftimg1);
RR = real(sfftimg1);
II = imag(sfftimg1);

A=sqrt(RR.^2+II.^2);%计算频谱幅值
A=(A-min(min(A)))/(max(max(A))-min(min(A)))*225; %归一化
subplot(2,3,2);
imshow(A);

% 计算填充图像大小
[M,N] = size(img1);
M2 = 2*M;
N2 = 2*N;

% 傅里叶变换
F = fftshift(fft2(img1,M2,N2));
subplot(2,3,3);imshow(mat2gray(log(1+abs(F))));title('傅里叶频谱');


% 设计滤波器
D0=40;      
h=zeros(M2,N2); 
for i=1:M2 
    for j=1:N2 
       if((abs(M2/2-i)<D0)&&(abs(N2/2-j)<D0)) 
           h(i,j)=0; 
       else
           h(i,j)=1;
        end 
    end 
end    
H = mat2gray(h);% 理想滤波器
subplot(2,3,4);imshow(H);title('理想高通滤波器');


G = F.*H;
subplot(2,3,5);imshow(mat2gray(log(1+abs(G))));title('频域滤波');


g0 = ifft2(fftshift(G));
g = g0(1:M,1:N);
g = real(g);
subplot(2,3,6);imshow(g);title('滤波后的图像');
% 
% % 创建高通滤波器
% high_pass_filter = ones(size(A));
% radius = 30; % 调整这个半径以控制高频通道的大小
% 
% % 在频谱中心创建一个圆形掩模，将半径外的部分设为0
% [rows, cols] = size(A);
% center = [rows/2, cols/2];
% [x, y] = meshgrid(1:cols, 1:rows);
% mask = (x - center(1)).^2 + (y - center(2)).^2 > radius * radius;
% % mask = (abs(x - center(1)) > radius) | (abs(y - center(2)) > radius);
% % mask1(200:250, 200:300) = 0;
% mask = ~mask;
% high_pass_filter(mask) = 0;
% 
% % 应用高通滤波器
% filtered_A = A .* high_pass_filter;
% 
% subplot(2,3,3);
% imshow(filtered_A, []);
% 
% % 反傅里叶变换
% filtered_img = ifft2(ifftshift(filtered_A));
% 
% % 取实部
% filtered_img = real(filtered_img);
% 
% subplot(2,3,4);
% imshow(uint8(filtered_img),[]);



```

# 结果

![image-20231213201827054](../images/image-20231213201827054.png)
