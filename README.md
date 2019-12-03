# MY-repository

2019/10/08
今天结合之前代码看了opencv--SVM部分知识，晚上看了cmake部分知识（https://www.cnblogs.com/52php/p/5681755.html）

2019/10/9------2019/10/15
完成一个小项目，实现练手的目的，识别身份证号码区域，并截取号码图片，使用SVM识别数字并显示出来


2019/10/15------2019/10/17
完成对Ubuntu系统重新安装，解决了home空间不够用的问题，包含大华相机驱动问题、opencv和扩展库，tensorflow,eigen等

2019/10/18------2019/10/24
仿照上交代码实现读取识别，圈出候选装甲板区域。


2019/10/25------2019/10/25
读和看去年的代码，使用简单的训练集训练出来的模型，对装甲板候选区域图片进行识别。


2019/10/26
学会对大华相机的使用，将去年的相机驱动移植到，自己的工程文件，经测试可以使用。


2019/10/27
将大华相机与之前做的自瞄结合在一起使用，实现识别作用，
效果：1，可以圈出正面装甲板，但是当出现倾斜界面时候，无法圈出装甲板
     2，利用之前识别身份证数字训练出来的模型，无法准确识别出装甲板数字
     
待做：重新制作训练集来提高准确率

2019/10/28
1，采集了6000张图片，采集的图片圈出了两个灯条，0、1、2、3、4、5六个数字，每个数字包含了1000张图片
2，效果：（1） 经测试，效果依然不是很理想，但是相比较27号的准确率得到了一定的提高。
        （2）对于倾斜的图片依然识别不出
3，看了去年的代码，发现存在将图片矫正的代码，可以采用此方法。
待做：在看去年代码和上交的开源代码，进行对比。


2019/10/29
1，对比了去年的代码和上交的代码，发现去年的命名空间部分写的很好，可以直接通过xml文件将需要经常改的参数进行修改，比较直接快速。
   于是自己将仿照此方法写了代码。
2，发现上交的代码写了很多小函数，可观性比较强
3，晚上看了已经注释的去年代码，对于 灯条内部目标颜色百分比 部分存在疑问，有待深入理解，测试这段代码发现加和不加区别很大。
4，自己重写代码时候，发现point2f不能进行赋值，留待明天解决。

2019/10/30（准备数学方法考试）
1,对于前一天的point2f问题，发现去年航哥进行赋值是为了方便计算装甲板的四个坐标点，而我是用定义灯条类和装甲板类，不需要进行这步操作。
2，完成匹配灯条类的筛选工作的代码部分。

2019/10/31（准备数学方法考试）
1，看了透射变换的原理，学习了API接口函数（warpPerspective，getPerspectiveTransform,可以成功在自己代码里面使用。
2，整体代码已经完成到可以正面和倾斜面检索到装甲板，并将装甲板矫正。
3，下一步要完成对去年的SVM的训练集整理和使用

2019/11/01
1,看了一下去年的SVM训练和测试代码，并且进行整理测试；
2，整理了一下训练集，一共6类，每类一共有3731张图片；
3，对代码进行注释，但是对于为什么打乱矩阵训练集尚且存在疑问，留待解决。


2019/11/02
1，完成对整体代码的注释工作。
2，完整的跑完所有代码，测试集合使用6类图片，每类有12张图片准确率达到100%，但是使用其他的测试图片会出现识别错误情况
3，完成对代码的文档整理工作。

2019/11/03
1，将SVM部分代码加入自己的代码中>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>


2019/11/04
1，再加入SVM部分时候，感觉自己的整体代码很混乱，重新进行梳理代码结构思路

2019/11/05
1，寻找装甲板的中心点，在使用去年的代码中，发现很多问题，不能很好的找到装甲板的中心点，重新进行谢了此代码，
利用两条对角线得到交点，即是中心点。
2，对装甲板进行优先级排序

2019/11/06
1，完成装甲板优先级程序的任务
2，使用PNP得到相机到装甲板的距离
3，下一步要做的是添加串口部分，正在学习BOOST。


2019/11/07
1,测试了串口通信代码，经测试可以通信，一开始没有注意到是１６进制导致出现乱码。
２，下一步开始看坐标变换部分。


2019/11/0８～2019/11/１０
１，学习了解了像素坐标系、图像坐标系、世界坐标系、相机坐标系之间的关系和数学推导。
２，学习了解了相机畸变原因以及畸变矫正。

2019/11/0９
１，在对自瞄大体流程清楚情况下，李凯安排了我去搞雷达部分，所以开始学习了解雷达部分。
２，对雷达的目前思路是，通过帧间差法找到运动的物体，并将运动物体圈出来，通过与第一帧图像对比，可以知道物体运动的距离。
３，学习了一下上车调代码的步骤。
４，将大华相机架高拍了一下车辆运动视频。

2019/11/10～2019/11/1１
１，做雷达当时第一想到的是检测运动物体，所以在ＣＳＤＮ上检索了相关的方法，找到了几个方法，帧间差分法、背景减弱法、光流法
２，采用了背景减弱法（ＭＯＧ２）测试了效果，感觉挺不错

2019/11/1２～2019/11/1４
１，感觉之前的拍照的视频效果不够好，重新录了红蓝车运动视频。
２，使用新拍照的视频，按照识别装甲板的思路继续编写代码识别运动车辆
３，可以识别到运动车辆，但存在误检和漏检，依靠自己的手举着摄像头存在抖动现象。

2019/11/15
1,完善之前写的代码，实现在不纠缠在一起情况下可以识别敌我车辆，并在视频里面显示
２，与４０５师兄讨论整体方案的可行性，最终得到一个建议，使用鱼眼镜头，增加广角，验证能否识别装甲板的数字
３，晚上验证的效果不是很理想，等待天亮再次验证。

2019/11/1６
１，在白天继续验证用长镜头是否可以识别装甲板的数字，发现在大厅的两个对角处用１６ｍｍ镜头可以实现识别，但是视野范围太小。
２，对比了不同的镜头的视野范围
３，测量了大厅的距离是１２＊９ｍ,大创那边是１０＊５ｍ.
４，陈玮泽请机械的帮忙打印了一个固定可动装置来录制视频。

2019/11/1７

１，研究了一天工业相机的基础知识，有焦距、物距、像距、靶面、１/1.8''和１/3等的意思、相机接口、相机上面有调焦环、调光圈环等、视角和视野计算方法等。

2019/11/18 ~2019/11/24
1,使用大约一周的时间去看共享内存、节点、互斥量、发布器、订阅器，目的是为了解决驱动两个相机问题。
２，在学长、兄弟帮助下，最终在２４号成功驱动两个相机。过程：
（１）一开始想法是，把链接相机函数、回调函数（订阅器名字）等统统重新创建一个，存在问题是永远只能驱动一个相机，哪个相机连接函数放在前面，就驱动哪个相机。
（２）最终发现问题原因在于存在一个线程（ｊｏｉｎ）的原因，所以导致永远无法执行第二个连接函数。
（３）为了解决第二个问题又想办法创建一个线程，但是出现了一开始可以读出两张图片，但是不到一分钟就崩溃了。
（４）最终选择在连接函数里面，每个都添加一个最终解决问题，成功读出图片。
　
 
 2019/11/2５　
１，发现现在出现一个新问题，连接两个相机后，大约１０分钟或者时间更少，出现一个相机崩溃问题。
2，尝试解决此问题。

2019/11/27
1,解决驱动相机问题。

2019/11/30~2019/12/1
1,测试场地。22×16m，同时测试双目相机效果（120度广角），可以做到监控全场
2，购买新的相机镜头，广角达到110度

2019/12/03
1，将颜色识别由RGB识别改成HSV识别。
2，取回新买的镜头测试了一下110度的效果图。


