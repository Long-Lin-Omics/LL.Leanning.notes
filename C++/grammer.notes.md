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
| 类型 / 函数                                        | 说明                                         |
|--------------------------------------------------|--------------------------------------------|
| `std::filesystem::path`                          | 表示文件或目录的路径，支持路径拼接和解析等操作     |
| `std::filesystem::exists(path)`                  | 检查给定路径是否存在                             |
| `std::filesystem::is_directory(path)`            | 判断路径是否为一个目录                             |
| `std::filesystem::is_regular_file(path)`         | 判断路径是否为常规文件（非目录、非符号链接等）             |
| `std::filesystem::file_size(path)`               | 获取文件的字节大小（仅限常规文件）                     |
| `std::filesystem::create_directory(path)`        | 创建一个目录（如果目录已存在则返回 false）              |
| `std::filesystem::remove(path)`                  | 删除文件或空目录                                   |
| `std::filesystem::rename(old_path, new_path)`    | 重命名文件或目录                                  |
| `std::filesystem::copy(src, dst)`                | 复制文件或目录（可设置策略）                          |
| `std::filesystem::directory_iterator(path)`      | 用于遍历目录（不递归子目录）                          |
| `std::filesystem::recursive_directory_iterator(path)` | 用于递归遍历目录及其子目录                        |
| `std::filesystem::absolute(path)`                | 获取路径的绝对路径                                 |
| `std::filesystem::canonical(path)`               | 获取规范化的绝对路径，解析符号链接                        |
| `std::filesystem::current_path()`                | 获取当前工作目录路径                               |
| `std::filesystem::remove_all(path)`              | 删除路径及其包含的所有内容（递归删除）                   |

```
namespace fs = std::filesystem;
fs::path p = "/tmp/example.txt";
```


# lambda 函数
