---
title: Canvas对绘制的辅助
tags:
  - 自定义控件
  - Canvas
categories:
  - 自定义控件
date: 2017-10-02 12:18:15
---

### Canvas对绘制的辅助思维导图

![](https://ws1.sinaimg.cn/large/5cc1a78ely1fson1xokr8j222e0sg7bj.jpg)
<!-- more -->
### 范围裁切
1. clipRect
2. clipPath
### 几何变换
1. 使用 Canvas 来做常见的二维变换
    * translate 平移
    * rotate 旋转
    * scale 缩放
    * skew 错切
2. 使用 Matrix 来做变换
    * 使用 Matrix 来做常见变换
        * 创建 Matrix 对象
        * 调用 Matrix 的 pre/postTranslate/Rotate/Scale/Skew() 方法来设置几何变换
        * 使用 Canvas.setMatrix(matrix) 或 Canvas.concat(matrix) 来把几何变换应用到 Canvas
    * 使用 Matrix 来做自定义变换
        * Matrix.setPolyToPoly
3. 使用 Camera 来做三维变换
    * Camera.rotate*() 三维旋转
        * rotateX(deg) rotateY(deg) rotateZ(deg) rotate(x, y, z)
        * Camera 和 Canvas 一样也需要保存和恢复状态才能正常绘制
    * Camera.translate
    * Camera.setLocation(x, y, z) 设置虚拟相机的位置
        * 它的参数的单位不是像素，而是 inch，英寸