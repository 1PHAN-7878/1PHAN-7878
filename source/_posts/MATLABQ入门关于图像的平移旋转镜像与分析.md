---
title: MATLABQ入门关于图像的平移旋转镜像与分析
date: 2023-10-25 20:09:35
tags: MATLAB
---

# MATLAB Q根作业

今天Q根说要我完成一些作业，他还会检查其中一部分。这让我感到非常紧张和着急，我开始焦虑地写作业。

在心慌意乱的状态下，我努力扩写了每个问题，并尽量给出详细的答案。我不断提醒自己要保持专注和冷静，尽力完成作业。

时间一分一秒地过去，我试图将注意力集中在任务上，忽略掉内心的不安和压力。我意识到，即使紧张也无法改变现实，唯一的解决办法就是面对并尽力去完成作业。

逐渐地，我发现自己进入了一种工作的节奏。通过不断努力，我开始逐渐克服恐惧和焦虑，专注于解决问题和完成任务。

最终，我完成了作业，并在一半检查时交给了Q根。我深呼吸一口气，希望我的努力能够得到认可。无论结果如何，我知道我已经尽力了，并从中学到了如何应对压力和困难。

这次经历让我明白，当面临紧张和压力时，保持冷静和专注非常重要。虽然一开始感到慌乱，但通过努力和积极思考，我能够克服困难，完成任务并成长。



# 内容

编程：图像的平移，水平，垂直，镜像（对比你自己的和自带的），验证：旋转（调用），imageresize实现图像缩放（很多算法不同），对比两幅图像是否相同的标准psnr

# 结果

```matlab


img = imread('C:\Users\7878\Desktop\my_image.png');
img1 = imresize(img, 0.2);
% 旋转
angle = 45;
img_rotate = imrotate(img1, angle);

subplot(2,3,1);
imshow(img1);
% title('before rotate');

subplot(2,3,2);
imshow(img_rotate);
% title('旋转后');


img_gray = rgb2gray(img1);

subplot(2,3,3);
imshow(img_gray);
% title('灰色');

[r,c] = size(img_gray);
img_dst = zeros(r,c);

dx = 50;
dy = 50;
tras=[1 0 dx;0 1 dy;0 0 1];
for i=1:r
    for j=1:c
        %         temp = [i;j;1];
        %         temp = tras*temp;
        %         x=temp(1,1);
        %         y=temp(2,1);
        x = i + dx;
        y = j + dy;
        if(x>=1 && x<=r) && (y>=1 && y<=c)
            img_dst(x,y) = img_gray(i,j);
        end
    end
end


img_mirror = zeros(r,c);
for i=1:r
    for j=1:c
        x = abs(r - i);
        y = j;
        if(x>=1 && x<=r) && (y>=1 && y<=c)
            img_mirror(x,y) = img_gray(i,j);
        end
    end
end

subplot(2,3,4);
imshow(uint8(img_mirror));
% title('镜像的');


subplot(2,3,5);
imshow(uint8(img_dst));
% title('平移后');


% 水平镜像
horizontal_flip = flip(img_gray, 2);

% 垂直镜像
vertical_flip = flip(img_gray, 1);

subplot(2,3,6);
imshow(vertical_flip);
% 峰值信噪比
% mse = sum((double(img_mirror) - double(vertical_flip)).^2, [], 'all') / numel(img_mirror);
% psnr = 10 * log10((255^2) / mse);
% disp(psnr);
% result = psnr(img_mirror, vertical_flip);
[peaksnr, snr] = psnr(uint8(img_mirror), uint8(vertical_flip));
  
fprintf('\n The Peak-SNR value is %0.4f', peaksnr);


```

