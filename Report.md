# 数字图像处理Final    
**学生姓名：曾泽源  
班级：自动化65  
学号：2160504116  
提交日期：2019/3/30**  
**摘要：**  本报告主要记录最后一次作业的各项任务的完成情况。本次实验基于MATLAB2018a，对六幅测试图像分别进行了Canny algorithm处理，并在此基础上进行了Hough直线检测，进行了结果分析。同时，对test1进行了三种边缘检测方式：Canny algorithm、Sobel edge detection、Gaussian highpass filter，并基于这三种边缘检测方式分别进行了不同极值点的Hough直线检测，进行横向和纵向对比。  
**关键词：Canny algorithm;Hough直线检测;Sobel edge detection;Gaussian highpass filter;横向和纵向对比**   

Final：   
----------------------------------------  
直线检测  
  
作业要求：  
1. 首先对测试图像（文件名为：test1~test6）进行边缘检测，可采用书上介绍的Sobel等模板或者cann算子方法；  
2. 在边缘检测的基础上，用hough变换检测图中直线；  
3. 比较不同边缘检测算法（2种以上）、不同hough变换参数对直线检测的影响；  
4. 可以采用Matlab、OpenCV等自带函数。  
  
按标准格式在考试前提交报告。  
  
结果讨论    
----------------------------------------  
## 1.  
####  Canny algorithm  
**结果展示：**  
![](https://github.com/cengzeyuan/final/blob/master/picture/1.1.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/1.2.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/1.3.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/1.4.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/1.5.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/1.6.jpg)  
**结果分析：**  
 Canny algorithm较好的将图像边缘分割出来，同时能很好地抑制噪声。但是也可以看出，由于采用高斯滤波，Canny algorithm得到的图像边缘大多不是连续的，即对边缘的保存并不是很好。  
**注：** 由于test1有两个图层，第二个图层是空白的，所以我直接选取第一个图层作为测试图像去处理。处理后的结果与之前第四次作业相同图（第四次作业也是这个图，但当时是test4）的Canny algorithm效果一致。    
 ## 2.
 ####   基于Canny边缘检测的Hough直线检测  
 **结果展示：**    
![](https://github.com/cengzeyuan/final/blob/master/picture/2.1.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/2.2.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/2.3.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/2.4.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/2.5.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/2.6.jpg)  
**结果分析：**   
可以看出，由于 Canny algorithm较好的将图像边缘分割出来，Hough直线检测的效果是比较理想的，特别是对于细节较少的测试图片test2、test3、test4。反观对于细节较多的图片，如test1、test5、test6，特别是test6，Hough直线检测虽然还是能检测出较多的直线，但对比不难看出它也检测出了不少错误的、原图和Canny algorithm处理后的图像都不存在的直线。 
  
## 3.
 ####   比较不同边缘检测算法（2种以上）、不同hough变换参数对直线检测的影响  
我在原先使用的Canny algorithm的情况下，加入了 Sobel edge detection和
Gaussian highpass filter，并改变了Hough直线检测的极值点数。
 **结果展示：**    
![](https://github.com/cengzeyuan/final/blob/master/picture/3.1.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/3.2.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/picture/3.3.jpg)  
**结果分析：**   
可以看出，相较而言，基于Canny algorithm的Hough直线检测效果最佳的。随着极值点的增多，检测出的直线更多，同时直线的角度和长度也更丰富。  
Sobel edge detection能检测出图像的边缘，但是它并非基于图像灰度进行处理，并没有将图像的主体与背景严格地区分开来，同时对比Canny algorithm可以看出，它对于图像内部的细节的保护基本没有，这导致基于此的Hough直线检测效果很差，不管是基于Sobel edge detection处理后的图像的基础上观察，还是对比原图观察，这些检测出的直线明显都是有问题的，并且都出现边缘内侧白色区域，即原本的房子区域，可以大致分为两组平行线，并且随着极值点的增多，错误直线更加密集。  
Gaussian highpass filter处理后的图像明显不是单纯地0,1灰度图像，除了黑白色调以外，还有较明显的灰色。与Sobel edge detection的问题类似，基于此的Hough直线检测效果不佳，但是更多的错误直线出现在房子边缘的外侧。同时，这些直线大致也能分为两组平行线，并且随着极值点的增多，错误直线更加密集。  

## 4  
#### 关于作业第三题的一些问题  
可以看出，作业第三题中，我使用Matlab自带函数的canny algorithm的效果是没问题的，但是使用自己编的Sobel edge detection和Gaussian highpass filter包括显示以及之后的Hough直线检测的结果都出现了很大的问题，之后我发现，显示出现问题（即3的第二张图和第三张图的右上角的图片）是因为我在显示的时候漏带了索引map，加入了索引map以后显示是正常的。    
因为自己编的边缘检测算法我不知道如何让输出的图像和索引map直接合并然后进行Hough直线检测，之后进行Hough直线检测的依旧是没有索引map的tese1_main（由于test1有两个图层，第二个图层是空白的，所以我直接选取第一个图层作为测试图像去处理），所以左下角和右下角的图片显示的问题以及边缘检测的问题我不知道如何处理。  
最后，我考虑直接使用Matlab自带的函数进行处理，选用了Canny algorithm,Prewitt edge detection和Sobel edge detection。  
同时补充了对参数变化的叙述。  
 **结果展示：**    
![](https://github.com/cengzeyuan/final/blob/master/4.1.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/4.2.jpg)  
![](https://github.com/cengzeyuan/final/blob/master/4.3.jpg)  
**结果分析：**   
Prewitt算子是一种边缘样板算子，利用像素点上下左右邻点灰度差，在边缘处达到极值检测边缘，对噪声具有平滑的作用。由于边缘点像素的灰度值与其邻域点的灰度值显著不同，在实际应用中通常采用微分算子和模板匹配的方法检测图像的边缘。Prewitt算子不仅能检测边缘点，而且能抑制噪声的影响，因此对灰度和噪声较多的图像处理得比较好。  
观察可以发现，Prewitt edge detection和Sobel edge detection的结果和Hough直线检测的结果几乎一样（肉眼上观察），这可能是因为两者使用的卷积核相近。
与Canny algorithm相比，Prewitt edge detection和Sobel edge detection图内的细节保留的非常少，也较为破碎，但是也可能是这个原因，Hough直线检测的结果反而较好，与我们肉眼所观察的直线更为贴近并且准确。经Canny algorithm后的Hough直线检测因为图像内部大量破碎边缘的影响，出现了部分直线的误判。  
随着极值点的增多，三种边缘检测后的Hough直线检测检测出的直线更多，同时直线的角度和长度也更丰富。不难看出，当极值点较少时（为5），Matlab算法的Hough直线检测倾向于寻找倾斜角较小的直线（0-pi/2），当极值点较多时（为10），Matlab算法的Hough直线检测才开始出现pi/2-pi倾斜角的直线。  
