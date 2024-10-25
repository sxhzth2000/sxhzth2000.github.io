---
title: LearnOpenGL
author: Hao-Tan
date: 2024-10-14T13:45:50+08:00
categories: 
tags: 
bookSearchExclude: false
bookHidden: true
math: true
draft: false
weigth: 20
---
**This blog follow  [learnopengl](https://learnopengl.com/)**.
<!--more-->

---
# Getting Started
## Creating a window

1. 配置开发环境  
- GLAD  
- GLFW  

>  **NOTE**: 1. Include glad before glfw. 2. don forgot add "glad.c" to source file.
---

2. Code
```cpp
#include <GLAD/glad/glad.h>
#include  <GLFW/glfw3.h>
#include <iostream>
void framebuffer_size_callback(GLFWwindow* window, int width, int height)
{
	glViewport(0, 0, width, height);
}
void processInput(GLFWwindow* window)
{
	if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
		glfwSetWindowShouldClose(window, true);
}
int main()
{
	glfwInit();
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 6);
	glfwWindowHint(GLFW_OPENGL_PROFILE,GLFW_OPENGL_CORE_PROFILE);
	//glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, GL_TRUE);
	
	GLFWwindow* window = glfwCreateWindow(800, 600, "Create window", NULL, NULL);
	if (window == NULL)
	{
		std::cout << "faile to create window" << std::endl;
		glfwTerminate();
		return -1;
	}
	glfwMakeContextCurrent(window);

	if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress))
	{
		std::cout << "failed to initialize GLAD" << std::endl;
		return -1;
	}

	glViewport(0, 0, 800, 600);
	glfwSetFramebufferSizeCallback(window, framebuffer_size_callback);

	while (!glfwWindowShouldClose(window)) 

	{
		processInput(window);

		glClearColor(0.1f,0.2f,0.3f,0);//glClearColor is state seeting function
		glClear(GL_COLOR_BUFFER_BIT);//glClear is state using function

		glfwSwapBuffers(window);
		glfwPollEvents();
	}
	glfwTerminate();
	return 0;
}
```

---
## Render a triangle.

1. OpenGL 工作模式：状态机。
- Vertices: (Position, Color, Texture Coordinates, Normal, Tangent,etc)
```cpp
	float vertices[] = {    
	  -0.5f, -0.5f, 0.0f,  //left
	   0.5f, -0.5f, 0.0f,	//right
	   0.0f,  0.5f, 0.0f	//top
	};
```
- VBO	VAO EBO etc
```cpp
unsigned int VAO, VBO;
glGenVertexArrays(1, &VAO);
glGenBuffers(1, &VBO);
///GLuint VAOs[5];  // 用于存储多个 VAO 的 ID
//glGenVertexArrays(5, VAOs);  // 生成 5 个 VAO



//bind the vertex array  object first ,then  bind and set vertex buffers(s), and then configure vertex attribute(s).
glBindVertexArray(VAO);//指定当前的VAO
glBindBuffer(GL_ARRAY_BUFFER, VBO);//指定当前GL_ARRAY_BUFFER为VBO
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);//给指定当前GL_ARRAY_BUFFER传数据

glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);//当前VAO的顶点属性。1.index 2.当前属性的内容的个数,这里为坐标 3.类型 4.normalized 归一化 5. 大小 6.offset偏移
glEnableVertexAttribArray(0);//启用的索引

// note that this is allowed, the call to glVertexAttribPointer registered VBO as the vertex attribute's bound vertex buffer object so afterwards we can safely unbind
glBindBuffer(GL_ARRAY_BUFFER, 0);


glBindVertexArray(0);
//-----render loop----------------
//-----------------------------------
// draw our first triangle
glUseProgram(shaderProgram1);
glBindVertexArray(VAO1);
glDrawArrays(GL_TRIANGLES, 0, 3);
//if ebo
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);


```
## Shaders 
4. Texture