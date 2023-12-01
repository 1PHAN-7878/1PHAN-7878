---
title: MATLABQ艮课堂任务之两张给定的图像数据规定化
date: 2023-12-01 10:19:53
tags: MATLAB
---

# 任务描述

天气很冷，Q艮又是作为最后一节课，没想到是布置了上课的作业（其实是课上交给他的话会有一扣扣的加分啊）。任务呢，是给定了图像像素的分布，为了简化，只有八像素的灰度。将原本图像，按照给定的分布，重新排布，称之为规定化。

![image-20231201102436343](../images/image-20231201102436343.png)![image-20231201102442272](../images/image-20231201102442272.png)![image-20231201102452193](../images/image-20231201102452193.png)![image-20231201102459198](../images/image-20231201102459198.png)![image-20231201102516264](../images/image-20231201102516264.png)

代码如下：

```matlab
% 给定数组 A、B 和 C
A = [790, 1023, 850, 656, 329, 245, 122, 81];
B = [0, 1, 2, 3, 4, 5, 6, 7];
C = [0, 0, 0, 15, 20, 30, 20, 15];

% 初始化结果数组
result = zeros(1, 8);
resultadd = zeros(1, 8);

% 计算数组 A 和 C 的累积和
A_sum = cumsum(A);
A_p = A / max(A_sum); % 对 A 进行归一化

C_sum = cumsum(C);

% 对 A_sum 和 C_sum 进行归一化
A_normalized = A_sum / max(A_sum);
C_normalized = C_sum / max(C_sum);

% 显示归一化后的数组
disp('A 经过归一化');
disp(A_normalized);
disp('C 经过归一化');
disp(C_normalized);

% 循环遍历归一化后的 A，并在归一化后的 C 中找到最接近的值
for i = 1:length(A_normalized)
    targetNumber = A_normalized(i);
    [closestValue, index] = min(abs(C_normalized - targetNumber));
    result(i) = index;
end

% 显示归一化后 A 与 C 之间的相似性结果
disp('归一化后的相似性结果');
disp(result);

% 计算并显示添加近似值后的概率结果
for i = 1:length(result)
    resultadd(result(i)) = A_p(i) + resultadd(result(i));
end

% 显示最终的概率结果
disp('添加所有近似值后的概率和');
disp(resultadd);

% 绘制归一化分布的条形图
bar(resultadd);
title('数值分布的归一化');
xlabel('像素值');
ylabel('概率');

```

