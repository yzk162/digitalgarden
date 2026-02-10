---
{"dg-publish":true,"permalink":"/cpp学习/cpp函数/","dgPassFrontmatter":true}
---

## 构造函数
如果没有实例化对象，构造函数不会运行。
等于是对象中写一个函数，能够初始化。创建对象，运行构造函数。
```cpp
#include <iostream>

class Entity
{
public:
	float X,Y;
	
	Entity()
	{
		X = 0.0f;
		Y = 0.0f;
	}
	Entity(float x, float y)
	{
		X = x;
		Y = y;
	}

	void Print()
	{
		std::cout << X << "," << Y<<std::endl;

	}
};


int main()
{
	Entity e(10.0f,5.0f);
	e.Print();                                                                                                                                                                                                                                                                                                                                   

	std::cin.get();
}
```

## 析构函数
**析构函数的作用是清理资源：**当对象生命周期结束时自动调用，用于释放对象占用的内存之外的其他资源，比如关闭文件、释放网络连接、删除动态分配的内存等，防止内存泄漏和资源泄露。

**它做了：**

1. 在对象被销毁时自动执行清理工作
    
2. 释放对象在生命周期中申请的非内存资源
    
3. 确保资源被正确释放，避免内存泄漏
    

**在你的代码中：**

- `Function()`中的局部变量`e`在函数结束时自动销毁
    
- 析构函数`~Entity()`被自动调用，输出"Destroyed Entity!"
    
- 如果没有手动申请额外资源，编译器生成的默认析构函数也足够
    

**重要用途：**当类中有指针成员并使用`new`分配内存时，必须在析构函数中用`delete`释放，否则会造成内存泄漏。
```cpp
#include <iostream>

class Entity
{
public:
	float X, Y;
	
	
	Entity()
	{
		X = 0.0;
		Y = 0.0;
		std::cout << "Created Entity!" << std::endl;

	}

	~Entity()
	{
		std::cout << "Destroyed Entity!" << std::endl;

	}

	void Print()
	{
		std::cout << X << "," << Y<<std::endl;

	}
};

//当退出的时候，析构函数才会运行
void Function()
{
	Entity e;
	e.Print();
}

int main()
{
	Function();

	std::cin.get();
}
```
