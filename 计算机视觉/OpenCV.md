# [OpenCV教程](https://www.runoob.com/opencv/opencv-tutorial.html)
## flask 
是一个用Python编写的Web应用框架，快速搭建网站或Web API


CSI（摄像头串行接口):基于MIPI协议
ISP（图像信号处理器）


模板匹配算法
图像梯度算法(明暗变化)
canny边缘检测
阈值算法(二值化)
形态学算法(腐蚀膨胀)

HTML:超文本标记语言
```html
<!DOCTYPE html>          <!-- 声明这是 HTML5 文档 -->
<html>                   <!-- HTML 开始 -->
<head>                   <!-- 头信息（配置、样式） -->
    <meta charset="utf-8">   <!-- 编码方式 -->
    <title>摄像头画面</title>  <!-- 浏览器标题 -->
    <style>              <!-- CSS 样式（控制外观） -->
        body { background: #111; }   <!-- 背景黑色 -->
        h1 { color: #ccc; }          <!-- 标题灰色 -->
    </style>
</head>
<body>                   <!-- 页面内容（用户看到的东西） -->
    <h1>摄像头实时画面</h1>   <!-- 标题 -->
    <img src="/video">        <!-- 图片/视频 -->
</body>
</html>                  <!-- HTML 结束 -->
```

## 矩形检测
### 图像预处理
1. 转为灰度图
2. 高斯滤波平滑噪点
3. canny边缘检测
### 提取特征
1. 获取轮廓contours,`findContours()` （把边缘图的白色像素连成封闭曲线）
2. 将轮廓简化为顶点更少的多边形`approxPolyDP()` 多边形逼近函数,找出只有四个顶点的多边形进行进一步筛选
3. 凸性检测（矩形必须是多边形！！)
4. 矩形度检查（轮廓面积 / 最小外接矩形面积）


## 相机参数
曝光（可以通过减少曝光时间来减轻运动模糊）

# [OpenCV教程](https://www.runoob.com/opencv/opencv-tutorial.html)
## flask 
是一个用Python编写的Web应用框架，快速搭建网站或Web API


CSI（摄像头串行接口):基于MIPI协议
ISP（图像信号处理器）


模板匹配算法
图像梯度算法(明暗变化)
canny边缘检测
阈值算法(二值化)
形态学算法(腐蚀膨胀)

HTML:超文本标记语言
```html
<!DOCTYPE html>          <!-- 声明这是 HTML5 文档 -->
<html>                   <!-- HTML 开始 -->
<head>                   <!-- 头信息（配置、样式） -->
    <meta charset="utf-8">   <!-- 编码方式 -->
    <title>摄像头画面</title>  <!-- 浏览器标题 -->
    <style>              <!-- CSS 样式（控制外观） -->
        body { background: #111; }   <!-- 背景黑色 -->
        h1 { color: #ccc; }          <!-- 标题灰色 -->
    </style>
</head>
<body>                   <!-- 页面内容（用户看到的东西） -->
    <h1>摄像头实时画面</h1>   <!-- 标题 -->
    <img src="/video">        <!-- 图片/视频 -->
</body>
</html>                  <!-- HTML 结束 -->
```

## 矩形检测
### 图像预处理
1. 转为灰度图
2. 高斯滤波平滑噪点
3. canny边缘检测
### 提取特征
1. 获取轮廓contours,`findContours()` （把边缘图的白色像素连成封闭曲线）
2. 将轮廓简化为顶点更少的多边形`approxPolyDP()` 多边形逼近函数,找出只有四个顶点的多边形进行进一步筛选
3. 凸性检测（矩形必须是多边形！！)
4. 矩形度检查（轮廓面积 / 最小外接矩形面积）


## 相机参数
曝光（可以通过减少曝光时间来减轻运动模糊）

