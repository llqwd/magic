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

+ canny边际
  本质是通过像素值的骤变来判断边界
  优化：
  https://blog.csdn.net/lw18781108072/article/details/78974362?ops_request_misc=elastic_search_misc&request_id=9bb3b5b76431deb350f79221336bebdb&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-78974362-null-null.142^v102^pc_search_result_base3&utm_term=canny%E8%BE%B9%E7%BC%98%E6%A3%80%E6%B5%8B%E7%AE%97%E6%B3%95%E6%94%B9%E8%BF%9B&spm=1018.2226.3001.4187

+ 硬币连通域标记与重心绘制
  重要函数：
  
  1.`cv2.threshould(...)`
  
  < img src="https://github.com/llqwd/magic/blob/main/Screenshots/6e177f20552543e17a98cd2b02740b80.jpg" width="50%" alt="描述">

  2.`cv2.morphologyEx(...)`
  ```python
  import cv2
  import numpy as np
  
  # 假设你已经得到了binary图像
  kernel = np.ones((3,3), np.uint8)  # 定义结构元素（核）
  
  # 开运算：去除文字周围的小亮点噪点
  opening = cv2.morphologyEx(binary, cv2.MORPH_OPEN, kernel)
  
  # 闭运算：填充文字内部的小暗孔洞
  closing = cv2.morphologyEx(binary, cv2.MORPH_CLOSE, kernel)
  
  # 形态学梯度：提取文字的边缘
  gradient = cv2.morphologyEx(binary, cv2.MORPH_GRADIENT, kernel)
  ```
  
  ```python
  import cv2
  import numpy as np
  img = cv2.imread("coins.jpg")
  gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY) #转为灰度图
  
  # ---------------------- 3. 二值化 ----------------------
  # cv2.threshold：二值化函数
  # 参数1：灰度图
  # 参数2：阈值（这里用0表示自动计算）
  # 参数3：最大值255
  # 参数4：二值化方式：反二值化 + 大津法自动求阈值（函数中对应
  # 返回值：自动计算的阈值thresh，二值图像binary
  thresh, binary = cv2.threshold(gray, 0, 255,
      cv2.THRESH_BINARY_INV + cv2.THRESH_OTSU)
  
  # ---------------------- 4. 形态学开运算去噪 ----------------------
  # 生成[[1. 1. 1.]
         [1. 1. 1.]
         [1. 1. 1.]]
  kernel = np.ones((3, 3), np.uint8)
  binary = cv2.morphologyEx(binary, cv2.MORPH_OPEN, kernel)
  
  # ---------------------- 5. 连通域分析 ----------------------
  # cv2.connectedComponentsWithStats：带统计信息的连通域检测
  # 参数1：二值图
  # 参数2：connectivity=8 表示8邻域连通
  # 返回4个值：
  # num_labels：连通域总数（含背景）
  # labels：每个像素所属的连通域编号
  # stats：每个连通域的信息（x,y,w,h,面积）
  # centroids：每个连通域的重心坐标 (cx, cy)
  num_labels, labels, stats, centroids = cv2.connectedComponentsWithStats(
      binary, connectivity=8
  )
  
  # ---------------------- 6. 遍历每个硬币，画重心 ----------------------
  coin_count = 0
  # 从1开始，跳过背景0
  for i in range(1, num_labels):
      # 取出第i个连通域的重心
      cx, cy = centroids[i]
  
      # cv2.circle：画圆（这里用来画点）
      # 参数1：要画的图像
      # 参数2：圆心坐标 (int(cx), int(cy))
      # 参数3：半径5
      # 参数4：颜色(0,255,255) BGR→黄
      # 参数5：thickness=-1 表示实心
      cv2.circle(img, (int(cx), int(cy)), 5, (0, 255, 255), -1)
  
      coin_count += 1
  
  # ---------------------- 7. 显示结果 ----------------------
  print("硬币数量：", coin_count)
  cv2.imshow("Result", img)
  cv2.waitKey(0)       # 等待按键
  cv2.destroyAllWindows() # 关闭所有窗口
  ```
+ 回形针

  ```python
  import cv2
  import numpy as np
  
  # 1. 读取图像
  img = cv2.imread("paperclips.jpg")
  # 2. 转灰度
  gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
  # 3. 二值化
  thresh, binary = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY_INV + cv2.THRESH_OTSU)
  
  # ---------------------- 轮廓检测 ----------------------
  # cv2.findContours：查找轮廓
  # 参数1：二值图
  # 参数2：cv2.RETR_EXTERNAL 只检测最外层轮廓
  # 参数3：cv2.CHAIN_APPROX_SIMPLE 压缩轮廓点，节省内存
  # 返回值：contours 是所有轮廓的列表
  contours, hierarchy = cv2.findContours(
      binary, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE
  )
  
  # 遍历每个轮廓
  for cnt in contours:
      # cv2.drawContours：画轮廓
      # 参数1：原图
      # 参数2：轮廓列表
      # 参数3：-1表示画所有
      # 参数4：颜色(0,0,255) 红
      # 参数5：线条粗细2
      cv2.drawContours(img, [cnt], -1, (0, 0, 255), 2)
  
      # cv2.convexHull：求凸包（包裹轮廓的最小凸多边形）
      hull = cv2.convexHull(cnt)
      # 画凸包，绿色
      cv2.drawContours(img, [hull], -1, (0, 255, 0), 2)
  
  print("回形针数量：", len(contours))
  cv2.imshow("Contours & Convex Hull", img)
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ```

+ 人像美容
  ```python
  import cv2
  import numpy as np
  
  img = cv2.imread("face.jpg")
  
  # ---------------------- 双边滤波去皱纹 ----------------------
  # cv2.bilateralFilter：双边滤波（平滑图像，去除噪声同时，保留边缘信息 ）
  # 参数1：原图
  # 参数2：d 滤波直径
  # 参数3：sigmaColor 颜色相似度
  # 参数4：sigmaSpace 空间相似度
  beauty = cv2.bilateralFilter(img, d=9, sigmaColor=75, sigmaSpace=75)
  #空间相似度和颜色相似度设置得都比较大意味着滤波效果较强，能有效平滑皮肤机理同时保留五官等重要边缘
  
  # ---------------------- 生成瑕疵掩膜 ----------------------
  mask = np.zeros(img.shape[:2], np.uint8)
  # 手动标记几个痘区域
  mask[100:120, 200:220] = 255
  mask[150:170, 250:270] = 255
  
  # ---------------------- 图像修复去痘 ----------------------
  # cv2.inpaint：图像修复
  # 参数1：待修复图
  # 参数2：掩膜（白色表示要修复）
  # 参数3：修复半径(指的是算法在修复时会参考周围3像素半径的信息)
  # 参数4：修复算法
  result = cv2.inpaint(beauty, mask, 3, cv2.INPAINT_TELEA)
  
  cv2.imshow("Original", img)
  cv2.imshow("Beauty", result)
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ```
  
+ 滑动调节二值化
  ```python
  import cv2
  import numpy as np
  
  # 滑动条回调函数
  # val：当前滑动条的值
  def on_trackbar(val):
      # 二值化
      aaa, binary = cv2.threshold(gray, val, 255, cv2.THRESH_BINARY)
      cv2.imshow("Binary", binary)
  
  # 读取并转灰度
  img = cv2.imread("coins.jpg")
  gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
  
  # 创建窗口
  cv2.namedWindow("Binary")
  
  # ---------------------- 创建滑动条 ----------------------
  # cv2.createTrackbar：创建滑动条
  # 参数1：滑动条名
  # 参数2：窗口名
  # 参数3：初始值127
  # 参数4：最大值255
  # 参数5：回调函数
  cv2.createTrackbar("Threshold", "Binary", 127, 255, on_trackbar)
  
  # 初始化调用一次
  on_trackbar(127)
  
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ```
 + 鼠标获取颜色
  ```python
  import cv2
  import numpy as np
  
  # 鼠标回调函数
  # event：事件类型
  # x,y：坐标
  # flags：按键状态
  # param：用户传入参数
  def mouse_callback(event, x, y, flags, param):
      # 左键按下
      if event == cv2.EVENT_LBUTTONDOWN:
          # 若按下左键，则取出该点颜色 BGR
          b, g, r = img[y, x]
          print(f"坐标({x},{y})  B={b} G={g} R={r}")
  
  img = cv2.imread("coins.jpg")
  cv2.namedWindow("Image")
  
  cv2.setMouseCallback("Image", mouse_callback)
  #在Image这个窗口上发生任何鼠标时间opencv都会自动调用这个函数
  
  cv2.imshow("Image", img)
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ```

+ ROI区域提取
  ```python
  import cv2
  
  img = cv2.imread("multi_objects.jpg")
  
  # ---------------------- ROI截取 ----------------------
  # 图像切片：图像[ y起始:y结束, x起始:x结束 ]
  roi = img[50:250, 50:250]
  
  cv2.imshow("ROI", roi)
  cv2.waitKey(0)
  cv2.destroyAllWindows()
  ```
