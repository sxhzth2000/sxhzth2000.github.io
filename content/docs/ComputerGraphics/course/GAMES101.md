---
title: GAMES 101
date: 2024-06-23
math: true

bookSearchExclude: false

categories:
  - graphics
tags:
  - 光追
  - MVP变换
  - 线性代数
---
学习games101


coconut


<!--more-->

---
[games101的课程](https://sites.cs.ucsb.edu/~lingqi/teaching/games101.html)
# Overview of Computer Graphics
Overview of Computer Graphics

**• What is Computer Graphics?** 

**• Why study Computer Graphics?** 
- Applications 
- Fundamental Intellectual Challenges 
- Technical Challenges 

**• Course Topics**  课程主题
**• Course Logistics** 课程准备(后勤)
## What is Computer Graphics?


The use Of computers to synthesize and manipulate
visual information.

fuck me

##  Why study Computer Graphics?
### Application

- Video Games
- Moves
- Animations
- Design
- Visualization
- Virtual Reality
- Augmented Relity 增强现实
- Digjtal lllustration 数字绘画
- Simulation 
- Graphical User Interfaces GUI
- Typography 字体
  
## **Fundamental Intellectual Challenges**


<center>基础的知识挑战</center>

- Creates and interacts with realistic virtual world 
- Requires understanding of all aspects of physical world 
- New computing methods, displays, technologies

## Technical Challenges

- Math of (perspective) projections, curves, surfaces 
- Physics of lighting and shading 
- Representing / operating shapes in 3D - Animation / simulation 
- 3D graphics software programming and hardware

![](https://i.imgur.com/G5l1NeO.png)

# Review of Linear Algebra
线性代数回顾

**Graphics’Dependencies**
**• Basic mathematics** 
- Linear algebra, calculus, statistics 

• **Basic physics** 
- Optics, Mechanics 
- Misc 
- Signal processing 
- Numerical analysis 

• **And a bit of aesthetics**

## Vectors


## Vector Normalization

## Vector Addition

## Cartesian Coordinates

## Vector Multiplication

- Dot product
- Cross product
- Orthonormal bases and coordinate frames
### Dot product 

$$\begin{align}
-4 + 5x &= 2 + y \nonumber \\
w + 2 &= -1 + w \\
ab &= cb
\end{align}$$

$$\infty \cdot \ \times \ \alpha \ \beta \ \gamma \ \Gamma \ \delta \ \Delta \ \epsilon \ \zeta \ \eta \ \theta \ \Theta \ \iota \ \kappa \ \lambda \ \mu \ \nu \ \xi \ \Xi \ \pi \ \Pi \ \chi \ \rho \ \sigma \ \Sigma \ \tau \ \upsilon \ \ \Upsilon \phi \ \Phi \ \chi \ \phi\ \psi\ \Psi \ \omega \ \Omega  $$
### Cross product 

### Orthonormal bases and coordinate frames


# Transformation 2D 3D
# Transformation MVP

## Orthographic Projection
### 几何推导

	此处屏幕空间NDC为 右手坐标系，视锥体也为，世界空间也为右手坐标系 
	Opengl的NDC为 左手坐标系，平时使用右手坐标系进行计算
作业使用右手的归一化映射(右手坐标系)。Opengl默认左手，结果不同，都对 
重点在于缩放的正负，正是同方向，负为反方向，映射的方向
![](https://i.imgur.com/KdiekPa.png)



$$
 M_{ortho} =\begin{bmatrix}
\frac{2}{r-l} & 0 & 0 & -\frac{r+l}{r-l} \\
0 & \frac{2}{t-b} & 0 & -\frac{t+b}{t-b} \\
0 & 0 & \frac{2}{n-f} & -\frac{n+f}{n-f} \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

### 数学推导

再Opengl的坐标和NDC中
### 定义视景体
设定一个三维视景体，其边界为：
- 左边界 \( l \)
- 右边界 \( r \)
- 底边界 \( b \)
- 顶边界 \( t \)
- 近平面 \( n \)
- 远平面 \( f \)

#### 变换坐标范围
正交投影的目标是将这个视景体映射到标准的单位立方体范围，即 \([-1, 1] \) 的范围。

#### x轴方向的变换
将 \( x \) 从 \([l, r]\) 映射到 \([-1, 1]\)，可以使用线性插值：


$$
x' = \frac{2(x - l)}{r - l} - 1 
$$

#### y轴方向的变换
将 \( y \) 从 \([b, t]\) 映射到 \([-1, 1]\)：

$$
y' = \frac{2(y - b)}{t - b} - 1 
$$

#### z轴方向的变换
将 \( z \) 从 \([-n, -f]\) 映射到 \([-1, 1]\)：
此处的映射为左手

$$
 z' = \frac{2(z - n)}{f - n} - 1 
$$

### 构建变换矩阵
根据上述变换公式，我们可以构建出正交投影矩阵：

$$
\begin{aligned}
x' &= \frac{2x}{r-l} - \frac{r+l}{r-l} \\
y' &= \frac{2y}{t-b} - \frac{t+b}{t-b} \\
z' &= \frac{-2z}{f-n} - \frac{f+n}{f-n}
\end{aligned}
$$


将这些变换公式写成矩阵形式，我们得到正交投影矩阵：

$$
 M_{ortho} =\begin{bmatrix}
\frac{2}{r-l} & 0 & 0 & -\frac{r+l}{r-l} \\
0 & \frac{2}{t-b} & 0 & -\frac{t+b}{t-b} \\
0 & 0 & \frac{-2}{f-n} & -\frac{f+n}{f-n} \\
0 & 0 & 0 & 1
\end{bmatrix}
$$




Opengl的正交投影矩阵, z轴移动方向相反
![](https://i.imgur.com/PkPLhqr.png)
## Perspective Projection
### 几何推导
对正交投影进行积压

![](https://imgur.com/iKimK2n.png)

![](https://i.imgur.com/UlzVlWF.png)

![](https://i.imgur.com/OiQGN73.png)

![](https://i.imgur.com/0a1s8kg.png)

正交投影=正交左乘透to正交视投影
$M_{persp}=M_{ortho} M_{persp-ortho}$

$$
 M_{ortho} =\begin{bmatrix}
\frac{2}{r-l} & 0 & 0 & -\frac{r+l}{r-l} \\
0 & \frac{2}{t-b} & 0 & -\frac{t+b}{t-b} \\
0 & 0 & \frac{2}{n-f} & -\frac{n+f}{n-f} \\
0 & 0 & 0 & 1
\end{bmatrix}
$$


$$
 M_{persp-ortho} =\begin{bmatrix}
n & 0 & 0 & 0 \\
0 & n & 0 & 0 \\
0 & 0 & n+f & -nf \\
0 & 0 & 1 & 0
\end{bmatrix}
$$

$$
M_{perspective} = \begin{bmatrix}
\frac{2n}{r-l} & 0 & -\frac{r+l}{r-l} & 0 \\
0 & \frac{2n}{t-b} & -\frac{t+b}{t-b} & 0 \\
0 & 0 & \frac{n+f}{n-f} & -\frac{2nf}{n-f} \\
0 & 0 & 1 & 0
\end{bmatrix}
$$


![](https://i.imgur.com/JzLtXJ2.png)


![](https://i.imgur.com/i64vvVv.png)


POV视角中   
结果与Opengl官方相比较  结果不一样，NDC不一样的问题
![](https://i.imgur.com/9zKZePJ.png)
### 数学推导
from ChatGPT
透视投影矩阵（Perspective Projection Matrix）是一种将三维空间中的物体映射到二维平面上的投影矩阵，它与正交投影不同，会根据深度（距离视点的远近）对物体进行缩放，使得离视点越远的物体看起来越小，产生透视效果。

透视投影矩阵的一般形式如下：Opengl官方矩阵

$$
M_{perspective} = \begin{bmatrix}
\frac{2n}{r-l} & 0 & \frac{r+l}{r-l} & 0 \\
0 & \frac{2n}{t-b} & \frac{t+b}{t-b} & 0 \\
0 & 0 & -\frac{f+n}{f-n} & -\frac{2fn}{f-n} \\
0 & 0 & -1 & 0
\end{bmatrix}
$$


其中：
- \( l \) 和 \( r \) 分别是视景体的左边和右边。
- \( b \) 和 \( t \) 分别是视景体的底部和顶部。
- \( n \) 和 \( f \) 分别是视景体的近平面和远平面。

### 透视投影矩阵推导

透视投影的主要思想是将三维点投影到二维平面，并根据深度进行缩放。

#### 1. 定义视景体
设定一个三维视景体，其边界为：
- 左边界 \( l \)
- 右边界 \( r \)
- 底边界 \( b \)
- 顶边界 \( t \)
- 近平面 \( n \)
- 远平面 \( f \)

#### 2. 透视投影公式
透视投影的核心是将视景体内的点 \( (x, y, z) \) 变换为点 \( (x', y', z') \)，并将它们的齐次坐标 \( (x', y', z', w') \) 转换到标准视景体范围 \([-1, 1]\)。

通过透视投影，得到如下转换公式：

$$
x' = \frac{n x}{z}
$$

$$
y' = \frac{n y}{z}
$$

$$
z' = \frac{f(n - z)}{z (f - n)}
$$

$$
w' = -z
$$

#### 3. 构建变换矩阵
根据透视投影公式，我们构建矩阵如下：


$$
\begin{aligned}
x' &= \frac{2n x}{r-l} - \frac{r+l}{r-l} \\
y' &= \frac{2n y}{t-b} - \frac{t+b}{t-b} \\
z' &= -\frac{f+n}{f-n}z + \frac{2fn}{f-n} \\
w' &= -z
\end{aligned}
$$


将这些公式写成矩阵形式，我们得到透视投影矩阵：


$$
M_{perspective} = \begin{bmatrix}
\frac{2n}{r-l} & 0 & \frac{r+l}{r-l} & 0 \\
0 & \frac{2n}{t-b} & \frac{t+b}{t-b} & 0 \\
0 & 0 & -\frac{f+n}{f-n} & -\frac{2fn}{f-n} \\
0 & 0 & -1 & 0
\end{bmatrix}
$$


### 应用


```Cpp

Eigen::Matrix4f get_view_matrix(Eigen::Vector3f eye_pos)
{
    Eigen::Matrix4f view = Eigen::Matrix4f::Identity();

    Eigen::Matrix4f translate;
    translate << 1, 0, 0, -eye_pos[0],
                 0, 1, 0, -eye_pos[1],
                 0, 0, 1, -eye_pos[2],
                 0, 0, 0, 1;
    //std::cout << translate << std::endl;


    view = translate * view;

    return view;
}

Eigen::Matrix4f get_model_matrix(float rotation_angle)
{
    Eigen::Matrix4f model = Eigen::Matrix4f::Identity();

    // TODO: Implement this function
    // Create the model matrix for rotating the triangle around the Z axis.
    model << cos(rotation_angle), -sin(rotation_angle), 0, 0,
             sin(rotation_angle), cos(rotation_angle), 0, 0,
             0, 0, 1, 0,
             0, 0, 0, 1;

    // Then return it.

    return model;
}


// r.set_projection(get_projection_matrix(45, 1, 0.1, 50));
Eigen::Matrix4f get_projection_matrix(float eye_fov, float aspect_ratio,
                                      float zNear, float zFar)
{
    // Students will implement this function

    Eigen::Matrix4f projection = Eigen::Matrix4f::Identity();

    // TODO: Implement this function
 
    // Create the projection matrix for the given parameters.
    
		// Convert field of view from degrees to radians
	float fov_rad = eye_fov * MY_PI / 180.0f;

	// Calculate the values for the projection matrix
	float t = tan(fov_rad / 2.0f) * zNear;
	float r = t * aspect_ratio;

	float l = -r;
	float b = -t;
	float n = -zNear;
	float f = -zFar;
    
	// Set up the projection matrix

    //
	projection <<   (2.0f * n) / (r - l),    0, -(r+l)/(r-l), 0,
					0, (2.0f * n) / (t - b), 0, -(t + b) / (t - b),
					0, 0, (f + n) / (n-f), -(2.0f * f * n) / (n - f),
					0, 0, 1, 0;

    //std::cout << projection << std::endl;


    // Then return it.

    return projection;
}
```


# Rasterization1(Triangles)

# Rasterization2(Antialiasing and Z-Buffe)