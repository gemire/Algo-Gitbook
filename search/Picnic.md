Source: [https://algospot.com/judge/problem/read/PICNIC](https://algospot.com/judge/problem/read/PICNIC)

### Matter
Andromeda kindergarten Express van and then go on a picnic in the park on the main rhythm. Ore teacher tries to act to build a two by two students when paired picnic. But rather than give each other because friends do not walk around in pairs among the students as each other or fight, you have to always be in pairs of students each kkiriman friends.

When given to whether they are friends with each other for each pair of students, please write a program that counts the number of ways to give students mate. Students are paired only partially different, try it another way. For example, the following two methods in different ways.

(Taeyeon, Jessica) (Sunny, Tiffany) (Hyoyeon, glass)
(Taeyeon, Jessica) (a sunny, glass) (Hyoyeon, Tiffany)
### Input
The first line of input contains the number of test cases C (C <= 50) is given. The first line contains the number of students in each test case n (2 <= n <= 10) and a pair of friends m (0 <= m <= n * (n-1) / 2) will be given. Then the number of students in the two pairs of integers m line will be given another friend. The number is an integer from 0 N-1 both, such pair is given twice the input. The number of students is even.
### Print

Each test every student in each case one line output the number of ways you can mate kkiriman friends.

### Example input

```
3
2 1
0 1
4 6
0 1 1 2 2 3 3 0 0 2 1 3
6 10
0 1 0 2 1 2 1 3 1 4 2 3 2 4 3 4 3 5 4 5
```

### Example output

```
1
3
4
```

### Solution:

```c++
#include <iostream>
#include <array>
#include <vector>
#include <list>
#include <iterator>


using namespace std;

/**
 * https://algospot.com/judge/problem/read/PICNIC
 *
 */

int countPairings(bool *taken, vector<vector<int>> &rvec, int n) {
    int firstFree = -1;
    for (int i = 0; i < n; ++i) {
        if (!taken[i]) {
            firstFree = i;
            break;
        }
    }
    if (firstFree == -1) {
        return 1;
    }

    int ret = 0;
    for (int pairWith = firstFree + 1; pairWith < n; pairWith++) {
        if (!taken[pairWith] && rvec[firstFree][pairWith] == 1) {
            taken[firstFree] = taken[pairWith] = true;
            ret += countPairings(taken, rvec, n);
            taken[firstFree] = taken[pairWith] = false;
        }
    }
    return ret;
}


int main() {
#ifdef ONLINE_JUDGE
#else
    freopen("F:\\ClionProjects\\Algorithm\\input.txt", "r", stdin);
//    freopen("F:\\ClionProjects\\Algorithm\\output.txt", "w", stdout);
#endif
    int C = 0, n = 0, m = 0;
    scanf("%d", &C);
//    printf("%d\n", C);
    while (C--) {

        scanf("%d %d", &n, &m);
//        printf("%d %d\n", n, m);
//        array<array<int, 2>, m> relation;
//        int relation[][] = new int[m][2];
//        int relation[m][2];
//        int **relation = new int*[m];
        vector<vector<int>> relation(m, vector<int>(2));

        for (int i = 0; i < m; ++i) {
            scanf("%d %d", &relation[i][0], &relation[i][1]);
        }
        vector<vector<int>> rvec(n, vector<int>(n, -1));
        for (auto &row : relation) {
            int rl = row[0];
            int rr = row[1];
            if (rl > rr) {
                int tmp = rl;
                rl = rr;
                rr = tmp;
            }
            rvec[rl][rr] = 1;
            rvec[rr][rl] = 1;
        }


        bool *taken = new bool[n];
        for(int i = 0; i<n; i++){
            taken[i] = false;
        }

        int way = countPairings(taken, rvec, n);
        printf("%d\n", way);

    }


    return 0;
}

```
