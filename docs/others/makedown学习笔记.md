---
title: Makedown Node
date: 2023-05-29
tags: Study
---

# Title

## Subtitle

* 字体：

  * *斜体*，**粗体**，***粗斜体***

  * `高光`，~~删除线~~，<u>下划线</u>

---

* 插入：

  * 代码：

    * 段落插入：`print()`

    * 代码块：

      ```C++
      #include <iostream>
      using namespace std;
      int main(){
      	cout << "Hello world!" << endl;
      	return 0;
      }
      ```

* 公式：

  * 段落插入：$\mathbf{F}_n = \mathbf{F}_{n-1}^2$

  * 公式块：
    $$
    \mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix}
    \mathbf{i} & \mathbf{j} & \mathbf{k} \\
    \frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
    \frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
    \end{vmatrix}
    $$

* 图片：

> <img src="https://cdn.luogu.com.cn/upload/image_hosting/tz9gnswb.png" alt="洛谷图床" style="zoom: 50%;" />
>
> ```
> 网络：
> ![洛谷图床](https://cdn.luogu.com.cn/upload/image_hosting/tz9gnswb.png)
> 本地：
> ![一果流汗](C:\Users\86133\Desktop\SMILE\一果流汗.jpg)
> 缩放：
> <img src="C:\Users\86133\Desktop\SMILE\一果流汗.jpg" alt="一果流汗" style="zoom:50%;" />
> ```

* 链接：
  * [Baidu](https://www.baidu.com/)

---