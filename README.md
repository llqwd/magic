# 一、Linux
* ### 基础语句

  cd：进入目录  pwd：显示路径  ls：查看文件等

  cat file1：查看file1的文件内容

​	rm:删除文档  mkdir:创建目录   cp file1 dir1:复制file1到dir1   mv file2 dir2:移动file2到dir2

​	（/filecp）是重命名为filecp的意思

<img src="https://github.com/llqwd/magic/blob/main/Screenshots/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202026-01-29%20140909.png" alt="屏幕截图 2026-01-29 140909" style="zoom:80%;" />

​	rmdir:删除空目录   rm -r:删除非空目录

​	head/tail file:查看前/后10行（默认10行

​	head/tail -n 5 file:查看前/后5行

​	grep "l" file1 **其中-n显示行号   -i忽略大小写   -r在目录中递归查找**

<img src="https://github.com/llqwd/magic/blob/main/Screenshots/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202026-01-29%20150001.png" alt="屏幕截图 2026-01-29 150001" style="zoom:80%;" />

(^C是强制退出)

​	find -name "file3":（默认在当前目录）查找file3文件的地址

​	find -name “*3”：查找带有"3"的文件的地址

![屏幕截图 2026-01-29 152732](https://github.com/llqwd/magic/blob/main/Screenshots/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202026-01-29%20152732.png)

​	find -size +/- nM:查找大于/小于n兆的文件

​	find -maxdepth 2 -size +/- nM:层数区别

​	find -mtime -1:在一天内被**修改**的文件   find -mmin -1:在1分钟之内被**修改**的文件

​	fine -ctime -cmin:在一天 一分钟内被**创建**的文件

​	find -type f(查找文件) d(查找目录) l(查询符号)

​	<img src="https://github.com/llqwd/magic/blob/main/Screenshots/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202026-01-29%20160344.png" alt="屏幕截图 2026-01-29 160344" style="zoom:80%;" />

（还不会就看这个视频https://www.bilibili.com/video/BV1hw411z7Eh/?spm_id_from=333.337.search-card.all.click&vd_source=0f90f2fa90be4f490a6243549c4fbe7f

+ ### nano基本用法

​	-l：行号   -m：用鼠标点击或滚动   +n：跳转到第n行

1.保存文件：Ctrl+ O,然后按 Enter 键。

2.退出编辑器：Ctrl+ X

3.移动光标：

  + 箭头键（上、下、左、右）:移动光标。
  + Page Up / Page Down :滚动页面。
  + Ctrl+ A :光标移到行首。
  + Ctrl+ E :光标移到行尾。

4.剪切、复制和粘贴：

  + Ctrl+ K :剪切（删除）。
  + Ctrl+ U :复制文本。
  + Ctrl+ Shift + V :粘贴文本。

5.查找和替换：

  + Ctrl+ W :查找。
  + Ctrl+ \ :替换.

6.撤销和重做：

  + Ctrl+ Shift + Z :撤销。
  + Ctrl+ Shift + R :重做。

+ ### ssh

​	ping (ip地址) 判断是否联通

```Linux
ssh -p 22 user@host
ssh -l [user] hostname
ssh hostname
```

​    -p：指定端口号    user：登录的用户名    host：登录的主机。(22为默认端口号)

+ ### 挂载复制u盘

  1. 先查看新磁盘：
  sudo fdisk -l 从而找到新磁盘地址
  2. 新建挂载点：
  mkdir /mnt/data（可自定义路径
  <img src="https://github.com/llqwd/magic/blob/main/Screenshots/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20260206124844_225_2.jpg" alt="挂载u盘1" style="zoom:80%;" />
  <img src="https://github.com/llqwd/magic/blob/main/Screenshots/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20260206124843_224_2.jpg" alt="挂载u盘2" style="zoom:80%;" />
（挂载可参考b站视频https://www.bilibili.com/video/BV1534y1F7Uu/?spm_id_from=333.337.search-card.all.click&vd_source=0f90f2fa90be4f490a6243549c4fbe7f

# 二、opencv
## 1，python
### 基础语句

+ 读取图像

  ```python
  import cv2
  import matplotlib.pyplot as plt
  import numpy as np
  %matplotlib inline

  img=cv2.imread('cat.jpg')
  ```
  其中`cv2.IMREAD_COLOR`是彩色图像 `cv2.IMREAD_GRAYSCALE`是灰度图像

+ 读取数值
  `img.shape`会得到图像属性(h,w,c)

+ 图像保存
  ```python
  cv2.imwrite('mycat.png',img)
  ```
  
+ 在四角显示图片
  ```python
  #调整图片大小（例如到400*300
  def resize_image(img, width, height):
    return cv2.resize(img,(width,height),interpolation=cv2.INTER_AREA)

  resized_img = resize_image(img, 400, 300)
  #设定屏幕尺寸
  screen_width,screen_height=1920,1080
  img_w,img_h=resized_img.shape[1],resized_img.shape[0]
  #四个角坐标
  positions = {
       "左上角": (0, 0),
       "右上角": (screen_width - img_w, 0),
       "左下角": (0, screen_height - img_h),
       "右下角": (screen_width - img_w, screen_height - img_h)
   }
   #显示在四个角
   for name, (x, y) in positions.items():
       cv2.namedWindow(name, cv2.WINDOW_NORMAL)
       cv2.moveWindow(name, x, y)
       cv2.imshow(name, resized_img)
       cv2.waitKey(0)
       cv2.destroyAllWindows()
  ```
  `cv2.namedWindow(name, cv2.WINDOW_NORMAL)`:创建一个名为`name`的窗口
    + cv2.WINDOW_NORMAL：允许手动调整大小
    + cv2.WINDOW_AUTOSIZE：固定大小无法调整

  `cv2.moveWindow(name, x, y)`:将名为`name`窗口移动到(x,y)处

+ 处理像素与通道(彩色图变灰度图)
  ```python
  import cv2
  import numpy as np
  
  img = cv2.imread("test.jpg")
  h, w, c = img.shape
  
  # 遍历每个像素，计算三通道均值并替换
  for y in range(h):
      for x in range(w):
          b, g, r = img[y, x]
          average = int((b + g + r) / 3)
          img[y, x] = [average, average, average]
          # 三通道都设为均值
  
  cv2.imshow("Average Image", img)
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ```
+ 深拷贝与浅拷贝
  浅拷贝
  ```python
  import copy
  c=copy.copy(a)
  ```
  深拷贝
  ```python
  import copy
  d=copy.deepcopy(a)
  ```
  **区别：修改浅拷贝会影响原图 但是深拷贝不影响**
+ 通道分离
  ```python
  import cv2
  import numpy as np
  
  img = cv2.imread("test.jpg")
  
  # 分离 BGR 通道
  b, g, r = cv2.split(img)
  
  # 显示每个通道
  cv2.imshow("Blue Channel", b)
  cv2.imshow("Green Channel", g)
  cv2.imshow("Red Channel", r)
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ```
+ Gamma矫正
  + 为什么：屏幕并非线性输出所以显示器显示图像时，本身会变暗；人眼对暗部更敏感
  + 矫正公式：
    
    $$ O = \left( \frac{I}{255} \right)^{\gamma} \times 255 $$

    I: 原像素值（0-255）
    γ: 伽马系数（γ<1 图像变亮）
    O: 矫正后的像素
  + 代码实现
  ```python
  import cv2
  import numpy as np
  
  def gamma_correct(img, gamma=1.0):
      # 1. 构建 Gamma 映射表
      inv_gamma = 1.0 / gamma
      table = np.array([((i/255.0) ** inv_gamma) * 255 for i in np.arange(256)]).astype("uint8")
      #.astype("uint8"):将计算结果转化为0-255范围内数
  
      # 2. 应用查表
      return cv2.LUT(img, table)
  
  img = cv2.imread("test.jpg")
  img_gamma = gamma_correct(img, gamma=2.2)  # 标准gamma
  
  cv2.imshow("original", img)
  cv2.imshow("gamma", img_gamma)
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ```
+ HSV
  H：色相。红色为0°，蓝色约为240°
  S:饱和度。0为灰度，255为最亮
  V：明度。0为纯黑，255为最亮
  代码实现：
  ```python
  import cv2
  import numpy as np
  
  # 1. 读取图片并转换到HSV
  img = cv2.imread("dog.jpg")
  hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
  # 表明从RGB转化为HSV并返回hsv三维数组
  
  # 2. 定义颜色范围（OpenCV中H:0-179, S:0-255, V:0-255）
  # 红色（注意：红色在HSV中分布在0°和180°附近，需要两段范围）
  lower_red1 = np.array([0, 120, 70])
  upper_red1 = np.array([10, 255, 255])
  lower_red2 = np.array([170, 120, 70])
  upper_red2 = np.array([180, 255, 255])
  
  # 蓝色
  lower_blue = np.array([100, 120, 70])
  upper_blue = np.array([130, 255, 255])
  
  # 3. 使用inRange提取掩膜
  mask_red1 = cv2.inRange(hsv, lower_red1, upper_red1)
  mask_red2 = cv2.inRange(hsv, lower_red2, upper_red2)
  mask_red = cv2.bitwise_or(mask_red1, mask_red2)  # 合并两段红色范围
  
  mask_blue = cv2.inRange(hsv, lower_blue, upper_blue)
  
  # 4. 提取对应颜色区域
  res_red = cv2.bitwise_and(img, img, mask=mask_red)
  res_blue = cv2.bitwise_and(img, img, mask=mask_blue)
  
  # 5. 显示结果
  cv2.imshow("Original", img)
  cv2.imshow("Red Extracted", res_red)
  cv2.imshow("Blue Extracted", res_blue)
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ```

+ 绘图功能
  ```python
  import cv2
  import numpy as np
  
  # 创建一个黑色背景的图像 (高度400, 宽度600, 3通道BGR)
  img = np.zeros((400, 600, 3), dtype=np.uint8)
  
  # -------------------------- 1. 画点 --------------------------
  # 函数: cv2.circle()
  # 参数:
  #   img: 要绘制的图像
  #   center: 点的坐标 (x, y)
  #   radius: 半径 (画点时设为1或2)
  #   color: 颜色 (B, G, R) 格式，如 (0, 0, 255) 表示红色
  #   thickness: 线条粗细，-1表示填充
  cv2.circle(img, center=(100, 100), radius=2, color=(0, 0, 255), thickness=-1)  # 红色点
  
  # -------------------------- 2. 画线 --------------------------
  # 函数: cv2.line()
  # 参数:
  #   img: 要绘制的图像
  #   pt1: 起点坐标 (x1, y1)
  #   pt2: 终点坐标 (x2, y2)
  #   color: 颜色 (B, G, R)
  #   thickness: 线条粗细
  cv2.line(img, pt1=(200, 100), pt2=(400, 100), color=(0, 255, 0), thickness=2)  # 绿色线
  
  # -------------------------- 3. 画圆 --------------------------
  # 函数: cv2.circle()
  # 参数:
  #   img: 要绘制的图像
  #   center: 圆心坐标 (x, y)
  #   radius: 半径
  #   color: 颜色 (B, G, R)
  #   thickness: 线条粗细，-1表示填充圆
  cv2.circle(img, center=(300, 200), radius=50, color=(255, 0, 0), thickness=2)  # 蓝色空心圆
  
  # -------------------------- 4. 画矩形 --------------------------
  # 函数: cv2.rectangle()
  # 参数:
  #   img: 要绘制的图像
  #   pt1: 左上角坐标 (x1, y1)
  #   pt2: 右下角坐标 (x2, y2)
  #   color: 颜色 (B, G, R)
  #   thickness: 线条粗细，-1表示填充矩形
  cv2.rectangle(img, pt1=(450, 150), pt2=(550, 250), color=(0, 255, 255), thickness=-1)  # 黄色填充矩形
  
  # 显示图像
  cv2.imshow("Drawing", img)
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ``` 
+ 腐蚀、膨胀、开运算和闭运算
  https://www.bilibili.com/video/BV1zBCAYdEWd/?spm_id_from=333.337.search-card.all.click&vd_source=0f90f2fa90be4f490a6243549c4fbe7f


