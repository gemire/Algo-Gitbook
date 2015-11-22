# 递归调用与穷举搜索

```c++
#include <iostream>
#include <vector>
#include <iterator>

using namespace std;

//void composite(int, int, vector<int> &);
void pick(int n, vector<int> &picked, int toPick);

void printPicked(vector<int> &vec);

int main() {
    vector<int> vec{};
    pick(7, vec, 4);
    return 0;
}

void pick(int n, vector<int> &picked, int toPick) {
    if (toPick == 0) {
        printPicked(picked);
        return;
    }

    int smallest = picked.empty()?0:picked.back()+1;
    for (int next = smallest; next < n; ++next) {
        picked.push_back(next);
        pick(n, picked, toPick -1 );
        picked.pop_back();
    }
}

void printPicked(vector<int> &vec) {
    for (auto &&i:vec) {
        cout << i << " ";
    }
    cout << endl;
}
```
