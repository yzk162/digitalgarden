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
