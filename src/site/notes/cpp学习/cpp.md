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


