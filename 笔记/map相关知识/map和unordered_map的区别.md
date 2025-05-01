`std::map` 和 `std::unordered_map` 都是 C++ STL 中用于存储键值对的容器，但它们在实现和性能特性上有一些显著的区别。以下是它们的主要区别：

### 1. 实现方式

- **`std::map`**：
  - 底层实现通常是红黑树（自平衡二叉搜索树）。
  - 键是有序的，存储时会根据键的顺序进行自动排序。
- **`std::unordered_map`**：
  - 底层实现通常是哈希表。
  - 键是无序的，不保持元素的顺序。

### 2. 时间复杂度

- **`std::map`**：
  - 查找、插入和删除操作的平均和最坏时间复杂度都是 O(log⁡n)O(\log n)O(logn)，因为需要遍历树结构。
- **`std::unordered_map`**：
  - 查找、插入和删除操作的平均时间复杂度是 O(1)O(1)O(1)，但最坏情况（如哈希冲突）时复杂度可能达到 O(n)O(n)O(n)。

### 3. 元素顺序

- **`std::map`**：
  - 自动按照键的顺序进行排序，可以使用迭代器按升序遍历元素。
- **`std::unordered_map`**：
  - 元素的顺序是不可预测的，遍历时不会按照插入顺序或任何顺序排列。

### 4. 内存开销

- **`std::map`**：
  - 由于需要维护树结构，每个节点的开销相对较大。
- **`std::unordered_map`**：
  - 使用哈希表，因此可能会有额外的内存开销用于存储哈希表的桶和处理冲突。

### 5. 键的要求

- **`std::map`**：
  - 键需要可比较（必须支持 `<` 运算符），以便进行排序。
- **`std::unordered_map`**：
  - 键需要可哈希（必须实现 `std::hash` 函数），并且需要相等比较（必须实现 `==` 运算符）。

### 选择建议

- 如果你需要保持元素的有序性，或者需要按顺序遍历元素，使用 `std::map`。
- 如果你更关注性能，特别是在查找和插入操作上，且不关心元素顺序，使用 `std::unordered_map`。

### 示例

```cpp
cpp复制代码#include <iostream>
#include <map>
#include <unordered_map>

int main() {
    // 使用 std::map
    std::map<int, std::string> orderedMap;
    orderedMap[2] = "two";
    orderedMap[1] = "one";
    orderedMap[3] = "three";
    
    std::cout << "Map contents (ordered):\n";
    for (const auto& pair : orderedMap) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    // 使用 std::unordered_map
    std::unordered_map<int, std::string> unorderedMap;
    unorderedMap[2] = "two";
    unorderedMap[1] = "one";
    unorderedMap[3] = "three";
    
    std::cout << "Unordered Map contents:\n";
    for (const auto& pair : unorderedMap) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    return 0;
}
```