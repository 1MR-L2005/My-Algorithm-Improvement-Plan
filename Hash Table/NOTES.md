# 🌳 C++ map 常用操作笔记

`std::map` 是 C++ 中最常用的关联容器之一，用于存储 **键值对 (key-value)** 数据。  
它会自动按照键排序，并提供高效的查找、插入和删除操作。


## 一、map 的定义与初始化


#include <iostream>
#include <map>
using namespace std;

int main() {
    map<int, string> mp;  // 空 map

    // 初始化方式 1
    map<int, string> mp1 = {{1, "A"}, {2, "B"}, {3, "C"}};

    // 初始化方式 2：赋值插入
    mp[1] = "Apple";
    mp[2] = "Banana";
    mp[3] = "Cherry";

    for (auto &p : mp)
        cout << p.first << " => " << p.second << endl;
}
输出：

ini
复制代码
1 => Apple
2 => Banana
3 => Cherry

## 🧮 二、常用操作汇总
操作	语法	说明
插入	mp.insert({key, value});	插入键值对
访问	mp[key]	若 key 不存在则自动创建默认值
查找	mp.find(key)	返回迭代器，未找到则为 mp.end()
删除	mp.erase(key);	删除指定键
清空	mp.clear();	清空所有元素
判断空	mp.empty();	返回布尔值
获取大小	mp.size();	返回元素个数
判断存在	mp.count(key)	返回 0 或 1
交换	mp1.swap(mp2);	交换两个 map 的内容

## 🧭 三、遍历 map 的方式
✅ 方式 1：迭代器遍历
cpp
复制代码
for (map<int, string>::iterator it = mp.begin(); it != mp.end(); ++it)
    cout << it->first << " => " << it->second << endl;
✅ 方式 2：范围 for（推荐）
cpp
复制代码
for (const auto &pr : mp)
    cout << pr.first << " => " << pr.second << endl;
✅ 方式 3：C++17 结构化绑定
cpp
复制代码
for (auto [key, val] : mp)
    cout << key << " => " << val << endl;
## 🔍 四、查找元素
cpp
复制代码
auto it = mp.find(2);
if (it != mp.end())
    cout << "找到键 2，值为：" << it->second << endl;
else
    cout << "未找到键 2" << endl;
或使用 count()：

cpp
复制代码
if (mp.count(3))
    cout << "键 3 存在" << endl;
## 🗑️ 五、删除元素
cpp
复制代码
mp.erase(2);  // 删除键 2

auto it = mp.find(3);
if (it != mp.end())
    mp.erase(it);  // 删除指定位置

mp.clear();  // 清空整个 map
## 🧠 六、map 的自动排序特性
std::map 会自动按照 键的升序 排序：

cpp
复制代码
map<int, string> mp = {{3,"C"},{1,"A"},{2,"B"}};
for (auto &p : mp)
    cout << p.first << " ";
输出：

复制代码
1 2 3
若需降序：

cpp
复制代码
map<int, string, greater<int>> mp = {{3,"C"},{1,"A"},{2,"B"}};
## 🧮 七、map 元素的类型
每个元素本质上是一个：

cpp
复制代码
pair<const Key, Value>
例如：

cpp
复制代码
for (auto &pr : mp)
    cout << typeid(pr).name() << endl;
输出类似：

cpp
复制代码
std::pair<int const, std::string>
## 🧰 八、常见应用场景
1️⃣ 统计频率
cpp
复制代码
map<string, int> freq;
freq["apple"]++;
freq["banana"]++;
freq["apple"]++;
// apple:2, banana:1
2️⃣ 建立映射关系
cpp
复制代码
map<char, int> score = {{'A', 100}, {'B', 80}};
cout << score['A'];  // 输出 100
3️⃣ 按键自动排序输出
cpp
复制代码
map<int, string> id_to_name = {{2,"Tom"},{1,"Amy"},{3,"Jack"}};
// 输出顺序：1, 2, 3
## 🔄 九、map 与 unordered_map 对比
特性	map	unordered_map
底层结构	红黑树（有序）	哈希表（无序）
键是否排序	✅ 是	❌ 否
查找/插入复杂度	O(log n)	O(1) 平均
适用场景	需要顺序输出	只需快速查找

## ✅ 十、总结
功能	示例
插入	mp.insert({key, value});
修改	mp[key] = new_value;
查找	mp.find(key)
删除	mp.erase(key);
遍历	for (auto [k,v] : mp)
判断存在	if(mp.count(key))
清空	mp.clear();

##unordered_map为不按照key值排序的无序map

