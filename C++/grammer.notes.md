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


# lambda 函数 -- 定义函数的一种方式
| 普通函数                     | lambda 函数                                                       |
|-----------------------------|------------------------------------------------------------------|
| 返回类型 函数名(形参){函数体}; | 返回类型 函数名 = [捕获函数外部变量](形参){函数体：函数体可访问捕获变量和形参}; |
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














