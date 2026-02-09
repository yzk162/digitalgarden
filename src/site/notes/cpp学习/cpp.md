---
{"dg-publish":true,"permalink":"/cpp学习/cpp/","dgPassFrontmatter":true}
---

开始了。
【【百万好评】国外大神！！油管千万级收藏，C++技术大佬带你从入门到精通，新手快速进阶！全中文字幕，学不会我退出IT界】 https://www.bilibili.com/video/BV1Dk4y1j7oj/?share_source=copy_web&vd_source=90200e9e40b0a430d34298005541255c

今天过了下基础的一些知识，比如说如何调试，之类的。
调试，设置断点
调试过程中可以进入反汇编。
else if 实际上是else+if

![文件结构.png](/img/user/cpp%E5%AD%A6%E4%B9%A0/%E9%99%84%E4%BB%B6/%E6%96%87%E4%BB%B6%E7%BB%93%E6%9E%84.png)
这里几个其实是过滤器。


指针只是一个保存内存地址的整数。
```cpp
#include <iostream>
#include "log.h"

#define LOG(x) std::cout << x <<std::endl

int main()
{
	char* buffer = new char[8];
	memset(buffer, 0, 8);
	char** ptr = &buffer;
	
	delete[] buffer;
	
	std::cin.get();
}
```

## 引用
引用必须引用真实存在的变量。
引用本身不是变量，它不占用内存。
```cpp
int a = 5;
int* b = &a;
//&符号在类型旁边，是一个引用。
int& ref = a;
ref = 2;
LOG(a);
```
上面的代码段中，等于说给a起了一个小名ref。

```cpp
void Increment(int* value)
{
	(*value)++;
}

int main()
{
	int a = 5;
	Increment(&a);
	LOG(a);

	
	std::cin.get();
}
```
输出a=6。
```cpp
int main()
{
	int a = 5;
	int b = 8;
	//创建引用，必须赋值。
	int& ref = a;
	ref = b;
	Increment(a);
	LOG(a);
	LOG(b);
	
	std::cin.get();
}
```


## 面向对象编程
### c++类
类用于整理格式，便于维护，用类实现的功能，不用类完全可以实现。

类与结构体的区别：
通常，类内变量函数是私有的，而结构体是公有的。
但是它们技术上没有区别。



写了一个class类LOG


```cpp
#include <iostream>

int a=5;
void function()
{

}


class Log
{
public:
	const int LogLevelError = 0;
	const int LogLevelWarning = 1;
	const int LogLevelInfo = 2;

private: 
	int m_LogLevel= LogLevelInfo;

public:
	void SetLevel(int level)
	{
		m_LogLevel = level;
	}

	void Error(const char* message)
	{
		if (m_LogLevel >= LogLevelError)
			std::cout << "[ERROR]:" << message << std::endl;
	}

	void Warn(const char* message)
	{
		if (m_LogLevel >= LogLevelWarning)
			std::cout << "[WARNING]:" << message << std::endl;
	}

	void Info(const char* message)
	{
		if (m_LogLevel>=LogLevelInfo)
			std::cout << "[INFO]:" << message << std::endl;
	}

};




int main()
{
	Log log;
	log.SetLevel(log.LogLevelWarning);
	log.Warn("Hello!");
	log.Info("Hello!");
	log.Error("Hello!");

	
	std::cin.get();
}
```
