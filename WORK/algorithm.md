## 迪杰斯特拉算法

https://zhuanlan.zhihu.com/p/454373256

## 翻转链表
```c++
ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* current = head;
    ListNode* nextNode = nullptr;

    while (current != nullptr) {
        nextNode = current->next;  // 保存下一个节点的指针
        current->next = prev;      // 将当前节点的next指向前一个节点，完成翻转操作
        prev = current;            // 更新prev指针
        current = nextNode;        // 更新current指针
    }
    
    return prev;  // 返回新的头节点
}
```

## 获得整数转二进制置位的个数

```c++
int sumIndicesWithKSetBits(vector<int> &nums, int k)
{
    int sum = 0;

    for (int i = 0; i != nums.size(); ++i)
    {
        bitset<32> b(i);
        if (b.count() == k)
        {
            sum += nums[i];
        }
    }

    return sum;
}
```

## dot解析成C++类
```c++
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <map>
#include <sstream> // 添加头文件

struct Edge {
    std::string source;
    std::string target;
};

class Graph {
private:
    std::vector<std::string> nodes;
    std::vector<Edge> edges;
    std::map<std::string, std::vector<std::string>> adjacencyList;

public:
    void addNode(const std::string& node) {
        nodes.push_back(node);
    }

    void addEdge(const std::string& source, const std::string& target) {
        edges.push_back({source, target});
        adjacencyList[source].push_back(target);
    }
    
    void print() {
        std::cout << "Nodes:" << std::endl;
        for (const auto& node : nodes) {
            std::cout << node << std::endl;
        }
        std::cout << "Edges:" << std::endl;
        for (const auto& edge : edges) {
            std::cout << edge.source << " -> " << edge.target << std::endl;
        }
    }
};

void parseDot(const std::string& filename, Graph& graph) {
    std::ifstream file(filename);
    if (!file.is_open()) {
        std::cerr << "Error: Couldn't open file " << filename << std::endl;
        return;
    }

    std::string line;
    while (std::getline(file, line)) {
        if (line.find("->") != std::string::npos) {
            size_t arrowPos = line.find("->");
            std::string source = line.substr(0, arrowPos);
            std::string target = line.substr(arrowPos + 2);
            
            // 添加代码以处理逗号分隔的元素
            std::istringstream ss(target);
            std::string targetNode;
            while (std::getline(ss, targetNode, ',')) {
                graph.addEdge(source, targetNode);
            }
        } else if (line.find("node") != std::string::npos) {
            size_t startPos = line.find('"') + 1;
            size_t endPos = line.find_last_of('"');
            std::string node = line.substr(startPos, endPos - startPos);
            graph.addNode(node);
        }
    }
    
    file.close();
}

int main() {
    Graph graph;
    parseDot("example.dot", graph);
    graph.print();
    return 0;
}
```