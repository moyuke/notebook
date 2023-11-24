# CVLab

## python基础

```python
# 赋值：python的赋值是可以等号两边分别用逗号间隔然后互不干扰的
# e.g. a, b, c = 1, {'cat', 'dog'}, imageio.imread('img.jpg')

# Strings
len(s) #长度
c = a + ' ' + b
c = '{} {}'.format(a, b) # 拼接，二者等价
s.strip() #删除前后空格
s.upper() #大写
s.rjust(7) #7格居右
s.center(7) #7格居中
s.replace(a, b) #查找替换a换b

# Lists
a[-1] #最后一个元素
a.append()
a = lists(range(5)) #range(5) = [0, 1, 2, 3, 4]
a[2:4] #下标2到3的元素(x:y为左闭右开)

# Loops
a = [...]
for i in a:
	# i是a中的元素
for idx, i in enumerate(a):
    # idx是从0开始的下标，i是a中的元素
a = [x ** 2 for x in nums if x % 2 == 0] # 数组间快捷赋值

# Sets
animals = {'cat', 'dog'}
print('cat' in animals) #查询是否在set中
animals.add('fish') #添加
animals.remove('cat') #移除
len(animals) #数量
for idx, animal in enumerate(animals):
    print('#{}: {}'.format(idx + 1, animal))
    # 输出
```

## 常用库

### numpy

```python
np.pi
np.exp()
np.add(,)
np.sqrt()
np.power(,)
np.dot(,) #矩阵点乘，等价于'@'，顺带一提，矩阵转置是x.T
np.sum(x) #求和
np.sum(x, axis=0) #按列求和
np.sum(x, axis=1) #按行求和
np.array() #创建一个数组，可用其他数组创建
	#e.g. a = np.array([1, 2, 3])
    #e.g. b = np.array([[1,2,3],[4,5,6]])
np.array(dst).astype(dtype=int).tolist() #转为int
np.array(dst, dtype=np.int64) #转为int64
np.zeros(size) #创建一个大小为size的全0矩阵，注意为float，即[0.]
	#e.g. np.zeros((3, 3)) 3×3全0矩阵
np.full((3,3), 1) #创建一个3×3全1矩阵，用这个可自己控制类型
	# 0:int, 0.5:float,'0':string
np.random.random((3,3)) #值为0~1的3×3矩阵
```

### matplotlib.pyplot

```python
imageio.imread(img_path) #读取图片，格式为(H,W,3)数组
plt.imshow(img) #绘制图像
plt.show() #显示图像（绘制也会显示在预览区，但是会被后面的覆盖掉）

plt.subplot(1, 2, 1)
plt.imshow(images[0])
plt.subplot(1, 2, 2)
plt.imshow(images[1])
# subplot功能，显示多图，（1，2，1）表示1行2列中的第一张
ax = plt.subplot(231) #等价于(2,3,1)
ax.axis('off')
ax.imshow(img)
# 关闭坐标轴

concat_image = np.concatenate(images, axis = 1)
# 合并图片，axis=1沿x轴合并

x=np.linspace(-10, 10, 50)
y=2 * x**2 - 3
plt.plot(x, y)
# 绘制函数，np.linspace(start,stop, num)控制x范围与精细度

plt.scatter(u, v)
# 绘制散点图，u,v为数组
```

## OpenCV

```python
cv2.imread(img_path)
cv2.imwrite(img_path, img)
# 读取/存储图片

cv2.cvtColor(img, cv2.COLOR_RGB2BGR)
cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
# RGB转BGR和灰度图
# 顺带一提，cv读取的图片是BGR，而plt读取的是RGB

cv2.imshow('image', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
# 弹窗显示图片，按任意键关闭

cap = cv2.VideoCapture('sfm.mp4')
while(cap.isOpened()):
    ret, frame = cap.read()
    if ret == True:
        cv2.imshow('Frame',frame)
        if cv2.waitKey(25) & 0xFF == 27:
            # 按esc退出
            break
    else:
        break
cap.release()
# 播放视频

cv2.putText(img, text, (200, 100), cv2.FONT_HERSHEY_COMPLEX, 2.5, (0, 0, 255), 5)
# 图片加文字：(200, 100)为位置，text为字符串，2.5为大小，(0,0,255)为BGR，5为粗细
```

## Open3d

```python
o3d.io.read_point_cloud(model_path) #读取点云
o3d.visualization.draw_geometries([pcd]) #显示点云
pcd.points #点云中的点集

pcd.translate((tx,ty,tz)) #点云平移(tx,ty,tz)
pcd.translate((tx,ty,tz), relative=False) #点云平移到(tx,ty,tz)(质心)
pcd.paint_uniform_color([0, 0, 1]) #点云上色

pcd.rotate(R,center=(x,y,z)) #点云旋转（R:旋转矩阵）
pcd.get_rotation_matrix_from_xyz((0, np.pi, 0)) #点云旋转（用欧拉角，绕质心）

pcd_scale.rotate(self) #点云缩放，self：缩放倍数
```

