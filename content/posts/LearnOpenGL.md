---
title: LearnOpenGL
author: Hao-Tan
date: 2024-10-14T13:45:50+08:00
categories: 
tags: 
bookSearchExclude: true
bookHidden: true
math: true
draft: false
---
**This blog follow  [learnopengl](https://learnopengl.com/)**.
<!--more-->
---

###### 1123123
# Getting Started
## Creating a window

1. 配置开发环境  
- GLAD  
- GLFW  

>  **NOTE**: 1. Include glad before glfw. 2. don forgot add "glad.c" to source file.
---

2. Code
```
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
		glfwSwapBuffers(window);
		glfwPollEvents();
	}
	glfwTerminate();
	return 0;
}
```