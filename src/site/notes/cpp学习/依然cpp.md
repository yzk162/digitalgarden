---
{"dg-publish":true,"创建时间":"2026-02-09","标签":["C++","编程","笔记"],"permalink":"/cpp学习/依然cpp/","dgPassFrontmatter":true}
---

## 静态变量 静态函数

当声明静态变量或者静态函数的时候，它们只在声明的文件中被看到。
全局变量是不好的，尽量标记为静态。


## 一、一句话理解
**静态成员变量是类的"共享财产"，所有对象共用同一份。**

## 二、核心特点
### 1. **共享性**
```cpp
class Student {
public:
    static int total;  // 所有学生共享这个计数器
    string name;
    
    Student(string n) {
        name = n;
        total++;  // 每创建一个学生，总数+1
    }
};

// 必须单独"安家"
int Student::total = 0;
```

### 2. **访问方式**
```cpp
// 方式1：通过类名访问（推荐）
Student::total = 100;

// 方式2：通过对象访问（可以但不推荐）
Student s("张三");
cout << s.total;  // 容易误解为对象的属性
```

## 三、关键对比
| 类型     | 存储位置 | 对象数量   | 访问方式      |
| ------ | ---- | ------ | --------- |
| 普通成员变量 | 对象内  | 每个对象一份 | `对象.变量名`  |
| 静态成员变量 | 全局区  | 全类只有一份 | `类名::变量名` |

## 四、实际应用
### 场景1：对象计数器
```cpp
class Car {
public:
    static int carCount;  // 统计总共制造的汽车
    
    Car() { carCount++; }
    ~Car() { carCount--; }
};

int Car::carCount = 0;  // 初始为0
```

### 场景2：共享配置
```cpp
class Game {
public:
    static int maxPlayers;  // 所有游戏对象共享的配置
};

int Game::maxPlayers = 4;  // 默认4人游戏
```

## 五、必须记住的规则
1. **声明在类内**：`static int count;`
2. **定义在类外**：`int 类名::count = 值;`
3. **初始化一次**：程序开始时就初始化
4. **所有对象共享**：修改一个，所有对象都看到变化

**静态函数没有`this`指针，只能访问静态成员。**
因为静态函数写在类内跟类外事一样的。

比如，这样是错误的。
```cpp
struct Entity
{
	int x, y;

	static void Print()
	{
		std::cout << x << "," << y << std::endl;
	}
};
```
这样是正确的，传入了类内变量，可以访问。
```cpp
struct Entity
{
	int x, y;

	static void Print(Entity e)
	{
		std::cout << e.x << "," << e.y << std::endl;
	}
};
```

静态局部变量
函数局部变量：每个函数独有，外界无法访问，且函数执行结束后保留。
```cpp
#include <iostream>

void Function()
{
	static int i = 0;
	i++;
	std::cout << i << std::endl;

}

int main()
{
	Function();
	Function();
	Function();
	Function();
	std::cin.get();
}
```
相当于外部无法访问改变i。


【23】节听得有点懵。
这段程序很厉害
```cpp
#include <iostream>

class Singleton
{
public:
	static Singleton& Get()
	{
		static Singleton instance;
		return instance;
	}
	void Hello()
	{ 
		std::cout << "hello" << std::endl;
	}
};

int main()
{
	Singleton::Get().Hello();
	std::cin.get();
}
```
看懂了，等于 static Singleton instance;这句话把创造的对象的生存周期延长到永远，然后可以一直存在调用。

类的学习先告一段落，感觉有点不懂。主要是记不住，后面用多了可能就记住了。

### 枚举

```cpp
enum Example
{
	A, B, C
};
```
如果不指定，A,B,C就是0 1 2递增。（默认）

```cpp
enum Example
{
	A=5, B, C
};
```
这时候就是5 6 7递增。

枚举等于是用整数值来表示想要表示的东西。

用枚举爆改昨天的代码。
```cpp
#include <iostream>

int a = 5;
void function()
{

}


class Log
{
public:
	enum Level
	{
		LogLevelError,
		LogLevelWarning,
		LogLevelInfo
	};
	

private:
	Level m_Level= LogLevelInfo;

public:
	void SetLevel(Level level)
	{
		m_Level = level;
	}

	void Error(const char* message)
	{
		if (m_Level >= LogLevelError)
			std::cout << "[ERROR]:" << message << std::endl;
	}

	void Warn(const char* message)
	{
		if (m_Level >= LogLevelWarning)
			std::cout << "[WARNING]:" << message << std::endl;
	}

	void Info(const char* message)
	{
		if (m_Level >= LogLevelInfo)
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