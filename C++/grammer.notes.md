# std
| 功能类别       | 代表内容举例                                   | 简单说明                   |
| -------------- | ---------------------------------------------- | -------------------------- |
| 容器           | std::vector, std::string, std::map, std::unordered_set | 用于存储和管理数据的集合     |
| 算法           | std::sort, std::find, std::accumulate          | 作用于容器或数据的算法       |
| 迭代器         | std::vector<T>::iterator 等                      | 用于遍历容器元素             |
| 输入输出       | std::cin, std::cout, std::cerr, std::ifstream   | 标准输入输出流和文件读写     |
| 智能指针       | std::unique_ptr, std::shared_ptr, std::weak_ptr | 用于自动管理动态分配内存     |
| 异常处理       | std::exception, std::runtime_error               | C++的异常类和异常处理机制    |
| 函数和函数对象 | std::function, std::bind, std::invoke            | 用于封装和调用函数           |
| 线程和并发     | std::thread, std::mutex, std::future, std::async | 多线程支持和同步机制         |
| 时间和日期     | std::chrono                                      | 处理时间点、时间段和计时     |
| 数学           | std::abs, std::pow, std::sqrt                     | 常用数学函数                 |
| 类型工具       | std::move, std::forward, std::enable_if, std::is_same | 用于类型推断、类型转换和模板编程 |
| 字符串和字符处理 | std::string, std::to_string, std::stoi            | 字符串操作和转换             |
| 内存管理       | std::allocator, std::aligned_alloc                | 内存分配工具                 |


## std::vector
动态数组容器:
可以自动扩容（不像 C 风格数组大小固定）-- 每次超容量会翻倍分配空间（有性能开销）
元素在内存中连续存储
支持插入、删除、遍历等操作
```
#include <vector>
```	
常见构造方式
| 示例                             | 说明                       |
| ------------------------------ | ------------------------ |
| `std::vector<int> v;`          | 空 vector                 |
| `std::vector<int> v(5);`       | 创建有 5 个元素的 vector，初始值为 0 |
| `std::vector<int> v(5, 42);`   | 创建 5 个元素，每个都是 42         |
| `std::vector<int> v{1, 2, 3};` | 使用初始化列表创建                |
| `std::vector<int> v2(v);`      | 拷贝构造                     |

添加和删除元素--插入/删除中间元素开销大	vector 是连续内存结构，频繁 insert/erase 建议用 std::list
| 方法                            | 说明           |
| ----------------------------- | ------------ |
| `v.push_back(x);`             | 在末尾添加元素      |
| `v.pop_back();`               | 删除最后一个元素     |
| `v.insert(v.begin() + i, x);` | 在第 `i` 个位置插入 |
| `v.erase(v.begin() + i);`     | 删除第 `i` 个元素  |
| `v.clear();`                  | 清空所有元素       |

访问元素
| 方法          | 说明                |
| ----------- | ----------------- |
| `v[i]`      | 访问第 `i` 个元素，不检查越界 |
| `v.at(i)`   | 访问第 `i` 个元素，会检查越界（推荐） |
| `v.front()` | 第一个元素             |
| `v.back()`  | 最后一个元素            |
| `v.data()`  | 返回底层指针（C 数组）      |

遍历元素
```
// 传统 for
for (size_t i = 0; i < v.size(); ++i) {
    std::cout << v[i] << "\n";
}

// 范围 for（推荐）
for (int x : v) {
    std::cout << x << "\n";
}
```
大小和容量
| 方法                  | 说明                  |
| ------------------- | ------------------- |
| `v.size()`          | 当前元素数量              |
| `v.empty()`         | 是否为空                |
| `v.capacity()`      | 当前分配的内存大小（比 size 大） |
| `v.resize(n)`       | 改变大小，多则补默认值，少则删尾部   |
| `v.reserve(n)`      | 提前分配容量，避免频繁扩容       |
| `v.shrink_to_fit()` | 回收多余内存              |

排序、查找等
```
#include <algorithm>

std::sort(v.begin(), v.end());
std::reverse(v.begin(), v.end());
std::find(v.begin(), v.end(), 42); // 找值为 42 的元素
std::count(v.begin(), v.end(), 1); // 数一数有几个 1
```

## 常见容器
| 容器                   | 特点             | 适合场景       | 底层结构 |
| -------------------- | -------------- | ---------- | ---- |
| `std::vector`        | 动态数组，支持随机访问    | 读写多、插入删少   | 连续数组 |
| `std::list`          | 双向链表           | 频繁插入/删除    | 链表   |
| `std::deque`         | 双端队列           | 头尾都要插入/删除  | 分段数组 |
| `std::map`           | 有序键值对，按 key 排序 | 要保持顺序，查找快  | 红黑树  |
| `std::unordered_map` | 无序键值对，查找更快     | 快速查找，不需要排序 | 哈希表  |

```
#include <list>

std::list<int> l = {1, 2, 3};
l.push_front(0);   // 头插
l.push_back(4);    // 尾插
l.remove(2);       // 删除值为 2 的元素
```
优点：任意位置插入/删除 O(1)
缺点：不能随机访问（不能用 l[i]）; 占用内存大，不支持连续存储

```
#include <deque>

std::deque<int> d;
d.push_back(1);
d.push_front(0);
d.pop_back();
```
优点：支持头尾高效插入/删除; 支持随机访问（d[i]）
缺点：插入中间位置开销大

```
#include <map>

std::map<std::string, int> ages;
ages["Tom"] = 20;
ages["Jerry"] = 18;
```
优点：自动按 key 排序; 查找、插入、删除 O(log n)
缺点：较慢，不适合频繁查找时用

```
#include <unordered_map>

std::unordered_map<std::string, int> scores;
scores["Alice"] = 90;
scores["Bob"] = 85;
```
优点：查找、插入、删除 O(1) 平均时间; 比 map 快很多（尤其是大数据）
缺点：无序，不能按 key 排序; 哈希冲突时性能下降



## std::filesystem 
| 类型 / 函数                                             | 说明                                                                 | 常用方法 / 参数示例                                     |
|--------------------------------------------------------|----------------------------------------------------------------------|----------------------------------------------------------|
| `std::filesystem::path`                                | 表示文件或目录的路径，支持路径拼接、提取扩展名、父路径等操作                         | `.filename()`, `.extension()`, `.extension().string()`,`.parent_path()`         |
| `std::filesystem::directory_entry`                     | 表示文件系统中某个条目（文件或目录），带有文件状态缓存                                   | `.path()`, `.is_directory()`, `.is_regular_file()`, `.file_size()`, `std::filesystem::path(entry)` to `path` |
| `std::filesystem::exists(path)`                        | 检查给定路径是否存在                                                       | 接受 `path` 或 `directory_entry`                        |
| `std::filesystem::is_directory(path)`                  | 判断路径是否为一个目录                                                     | 同上                                                     |
| `std::filesystem::is_regular_file(path)`               | 判断路径是否为常规文件（非目录、非符号链接等）                                         | 同上                                                     |
| `std::filesystem::file_size(path)`                     | 获取文件的字节大小（仅限常规文件）                                               | 返回 `uintmax_t` 文件大小                                |
| `std::filesystem::create_directory(path)`              | 创建一个目录（如果目录已存在则返回 false）                                        | 可递归用 `create_directories()` 创建多层路径              |
| `std::filesystem::remove(path)`                        | 删除文件或空目录                                                         | 返回 `true/false` 是否成功                               |
| `std::filesystem::rename(old_path, new_path)`          | 重命名文件或目录                                                        | 也可用于移动文件                                         |
| `std::filesystem::copy(src, dst)`                      | 复制文件或目录（可设置策略）                                                  | 选项：`copy_options::recursive` 等                      |
| `std::filesystem::directory_iterator(path)`            | 用于遍历目录（不递归子目录）                                                  | 范围 for 支持：`for (const auto& e : directory_iterator)` |
| `std::filesystem::recursive_directory_iterator(path)`  | 用于递归遍历目录及其子目录                                                  | 支持 `++` 进入子目录                                     |
| `std::filesystem::absolute(path)`                      | 获取路径的绝对路径                                                       | 通常用于标准化路径输入                                   |
| `std::filesystem::canonical(path)`                     | 获取规范化的绝对路径，解析符号链接                                               | 适用于真实文件系统结构处理                                |
| `std::filesystem::current_path()`                      | 获取当前工作目录路径                                                     | 可用于确定程序运行环境                                   |
| `std::filesystem::remove_all(path)`                    | 删除路径及其包含的所有内容（递归删除）                                            | 删除文件夹及其所有内容                                   |


```
namespace fs = std::filesystem;
fs::path p = "/tmp/example.txt";
```

## 智能指针
普通指针申请的内存需要手动写delete，不然内存会一直被占用。
智能指针会自动处理。
```
引用计数智能指针
std::shared_ptr<指向类型>指针名{初始化}
std::shared_ptr<指向类型>指针名 = std::make_shared<指向类型>("指向类型的构造函数决定的初始化")
	多个 shared_ptr 可以同时指向同一个对象
	内部有引用计数
	最后一个引用释放时，自动 delete 掉对象
	用途：当多个地方要共享同一份 Info，但又不想手动管理释放的时候。
独占式智能指针
std::unique_ptr<指向类型>指针名{初始化}
std::unique_ptr<指向类型>指针名 = std::make_unique<指向类型>("指向类型的构造函数决定的初始化")
	只能有一个 unique_ptr 拥有某个对象
	不允许拷贝（copy 构造和赋值都被禁了）
	但可以move
	离开作用域/手动 reset 会自动释放内存
	用途：某个类或者函数独占拥有这份 Sheet，别的地方不能随意共享。
```
访问指向的数据
```
1. 使用 * 解引用（像普通指针一样）
2. 使用 -> 访问成员（像普通指针一样）: 适用于指向对象的情况. 调用类的成员函数或变量
3. 使用 .get() 获取原始裸指针（不推荐修改它）
```

## std::variant -- 类似 模板 的功能
它可以在多个类型中存储一个值，但同一时间只能是其中一个类型，并且类型是安全检查的。
```
using Message = std::variant<SimplexReadPtr,
                             BamMessage,
                             ReadPair,
                             CacheFlushMessage,
                             DuplexReadPtr,
                             CorrectionAlignments>; 
```
相当于定义了一种新类型，兼容好几种类型。


# lambda 函数 -- 定义函数的一种方式
| 普通函数                     | lambda 函数                                                       |
|-----------------------------|------------------------------------------------------------------|
| 返回类型 函数名(形参){函数体}; | 返回类型 函数名 = \[捕获函数外部变量\](形参){函数体：函数体可访问捕获变量和形参}; 可以没有形参列表|
| 使用方式：函数名(实参)        | 使用方式：函数名(实参)                                            |
```
优势：
1) 定义方便，临时用
Lambda可以定义在用的地方，马上写马上用，不需要提前声明或放到类/命名空间里。
适合只在一处使用的小功能，减少函数命名的杂乱
2) 可以捕获外部变量
普通函数没法做到，除非把外部变量作为参数传进来。
3) 写成内联，利于编译器优化
4) 表达式更灵活，支持匿名
```
### lambda捕获变量类型
| 捕获写法          | 类型             | 含义                                  | 示例代码                               |
| ------------- | -------------- | ----------------------------------- | ---------------------------------- |
| `[]`          | 空捕获            | 不捕获任何外部变量                           | `[] { return 42; }`                |
| `[this]`      | 指针捕获           | 捕获当前对象的 `this` 指针，允许访问成员变量和函数       | `[this] { foo(); # foo 是对象的成员函数}`                |
| `[*this]`     | 值捕获（C++17）     | 捕获当前对象的副本（按值，深拷贝）                   | `[*this] { bar = this->bar + 1; }` |
| `[=]`         | 值捕获            | 捕获所有外部变量的副本（按值）                     | `[=] { return x + y; }`            |
| `[&]`         | 引用捕获           | 捕获所有外部变量的引用（按引用）                    | `[&] { x++; y++; }`                |
| `[x]`         | 指定值捕获          | 捕获变量 `x` 的副本                        | `[x] { return x + 1; }`            |
| `[&x]`        | 指定引用捕获         | 捕获变量 `x` 的引用                        | `[&x] { x++; }`                    |
| `[x, &y]`     | 混合捕获           | 捕获 `x` 的副本，`y` 的引用                  | `[x, &y] { y += x; }`              |
| `[=, &y]`     | 默认值 + 指定引用     | 捕获所有变量的副本，但 `y` 以引用方式捕获             | `[=, &y] { y += x; }`              |
| `[&, x]`      | 默认引用 + 指定值     | 捕获所有变量的引用，但 `x` 是副本                 | `[&, x] { z += x + y; }`           |
| `[z = x + y]` | 初始化捕获（C++14）   | 捕获表达式的结果为一个变量 `z`，作为 lambda 内部变量    | `[z = x + y] { return z * 2; }`    |
| `[&z = ref]`  | 引用初始化捕获（C++14） | 把外部变量 `ref` 以引用形式绑定为 lambda 内部名 `z` | `[&z = ref] { z++; }`              |

# for的两种形式
```
1) 
for (初始化; 条件判断; 每轮末尾动作) {
    // 循环体
}
2) 范围for： 自动遍历范围里的每一个元素 
for (声明 : 范围) {
    // 循环体
}
// 范围是任何可以被begin()和end()函数支持的类型（数组、标准容器、字符串、支持迭代器的自定义类型等）。
// 声明是用来接收当前迭代元素的变量，通常是元素类型或元素引用。
```
```
tips:
用 auto 和 auto& 可以省事，避免写错类型。
不确定是否会修改元素，默认用 const auto& 最安全。
```

# 类的函数类型和作用
| 函数名                       |       定义                          |作用                          |
|-----------------------------|-------------------------------------|-----------------------------|
| 成员函数（Member Functions）| 类内部定义的普通函数，用于操作类的成员变量，实现类的功能。|  操作对象状态，执行对象行为。|
| 构造函数（Constructor）| 用来***初始化***对象的特殊函数，***函数名和类名相同***，***没有返回值***。| 创建对象时自动调用，给成员变量赋初值。推荐使用***成员初始化列表***：***类名(形参声明):类成员(形参),类成员(形参){}***|
|析构函数（Destructor）|  用来清理资源的特殊函数，函数名是 ***~类名***，***没有返回值***，***无参数***。| 对象销毁时自动调用，释放对象占用的资源（内存、文件句柄等）。|
|静态成员函数（Static Member Functions）| 使用 ***static*** 关键字修饰的成员函数。 | 不依赖对象实例，可以***直接用类名调用***，不能访问非静态成员变量。|
| 常成员函数（Const Member Functions）| 函数名() 后面加 ***const*** 修饰，表示该函数不会修改类成员变量。| 用于保证该函数不会改变对象状态，允许对常对象调用。|
| 虚函数（Virtual Functions）|  使用 ***virtual*** 关键字修饰的成员函数。| 支持多态，允许子类重写父类函数，调用时根据对象实际类型执行对应函数。 |
| 纯虚函数（Pure Virtual Functions） |  虚函数 ***函数名() 后面加 = 0***，是抽象函数，类变成抽象类，***不能实例化***。 | 用来定义接口，必须在派生类中重写实现。|
| 内联函数（Inline Functions）| 使用 ***inline*** 关键字修饰，建议编译器将函数体展开，减少函数调用开销。 | 提高小函数的执行效率，减少函数调用时间。| 
```
private: 只能被类的成员函数（包括构造函数、普通函数、友元函数）访问。
不能被类的外部代码或对象直接访问。
类的成员变量应该尽量是 private 的，然后通过公共接口访问。
```


# 模板
### 函数模板
函数模板是C++的一种泛型编程机制，允许你写一个函数的“蓝图”，根据传入的类型自动生成不同版本的函数。
它使得函数可以处理多种数据类型，而不必为每种类型写重复代码。
```
template <typename T, typename U> // typename可以用class代替，不推荐
T add(T a, U b) {
    return a + b;
}
int result = add<int, double>(3, 4.5);  // T = int, U = double

```
### 类模板
template 后面跟具体类的定义。
适用于封装的对象中某些成员依赖类型。











