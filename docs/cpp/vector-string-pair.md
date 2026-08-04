# vector、string 与 pair

`vector`、`string` 和 `pair` 是 C++ 算法代码中最常见的三个工具。掌握它们后，大多数数组、文本和二元信息都能用清晰的方式表示。

## 适用场景

- 元素数量在运行时才确定，或需要动态追加元素时使用 `vector`。
- 需要保存、拼接或处理一段文本时使用 `string`。
- 需要把两个相关值一起传递、排序或存储时使用 `pair`。

## 常用操作

### vector

```cpp
vector<int> values = {3, 1, 4};
values.push_back(2);
values.pop_back();
int first = values.front();
int last = values.back();
int count = static_cast<int>(values.size());
```

`vector` 支持按下标随机访问，`values[i]` 的时间复杂度为 $O(1)$；在尾部 `push_back` 的均摊复杂度也是 $O(1)$。

### string

```cpp
string name = "algorithm";
name += " notes";
char first = name[0];
int length = static_cast<int>(name.size());
```

字符串同样支持按下标访问。需要整行读入时使用 `getline(cin, line)`。

### pair

```cpp
pair<int, string> item = {7, "seven"};
int id = item.first;
string label = item.second;
```

两个 `pair` 比较时会先比较 `first`，再比较 `second`，因此可以直接用于表示“权值与编号”这样的信息。

## 示例

下面的程序读入若干个名字与分数，按分数从小到大、名字字典序从小到大排序：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <utility>
#include <vector>

using namespace std;

int main() {
    int n;
    cin >> n;

    vector<pair<int, string>> students;
    for (int i = 0; i < n; ++i) {
        string name;
        int score;
        cin >> name >> score;
        students.push_back({score, name});
    }

    sort(students.begin(), students.end());

    for (const auto& [score, name] : students) {
        cout << name << ' ' << score << '\n';
    }
}
```

## 常见坑

- 不要用未检查的下标访问空 `vector` 或空 `string`。
- `size()` 的返回类型是无符号整数；与 `int` 比较或倒序循环时，先转换为 `int` 更不容易出错。
- 在 `cin >> value` 后立刻使用 `getline` 时，要先用 `cin.ignore()` 丢掉残留换行。
- `pair` 的默认排序是字典序；如果需要“分数从大到小”，应编写比较函数。
