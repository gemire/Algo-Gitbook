**Source:** [https://algospot.com/judge/problem/read/BOARDCOVER](https://algospot.com/judge/problem/read/BOARDCOVER)

### Problem Descirption
![](boardcover.png)

H * W size of the game are different. The game board is a grid consisting of white spaces and black and white Cannes Cannes would like to cover all of these in blocks of 3-bin-old L-shaped. This time blocks can be placed to rotate freely, but overlap one another, or cover, or a black square, the board should not go out. The above illustration shows how to cover it with a board.

Write a program to count the number of ways to cover this edition of the game given.

### Input

The first line of output contains the number of test cases C (C <= 30) is given. The first line of each test case contains two integers H, W (1 <= H, W <= 20) is given. The shape of the board in each of W characters are given in the following H lines. # is a black square, . it represents a white field. The number of white space on the board is given the input does not exceed 50.

### Print
The output can be one way of covering all of t

### Example input

```
3
3 7
#.....#
#.....#
##...##
3 7
#.....#
#.....#
##..###
8 10
##########
#........#
#........#
#........#
#........#
#........#
#........#
##########
```

### Exaple output

```
0
2
1514
```


Solution:

```cpp
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

//board[i][j] = 1 表示已被覆盖的格子或者黑格子
//board[i][j] = 0 表示未被覆盖的格子或者白格子
const int coverType[4][3][2] = {
        { {0, 0}, {1, 0}, {0, 1} },
        { {0, 0}, {0, 1}, {1, 1} },
        { {0, 0}, {1, 0}, {1, 1} },
        { {0, 0}, {1, 0}, {1, -1} }
};
bool set(vector<vector<int>> &board, int y, int x, int type, int delta){
    bool ok = true;
    for(int i = 0; i<3; i++){
        const int ny = y + coverType[type][i][0];
        const int nx = x + coverType[type][i][1];
        if(ny < 0 || ny >= board.size() || nx < 0 || nx >= board[0].size()){
            ok = false;
        }else if((board[ny][nx] += delta) > 1){
            ok = false;
        }
    }
    return ok;
}

int cover(vector<vector<int>> &board) {
    //在剩余未被覆盖的格子中，寻找摆放在最左上角的格子
    int y = -1, x = -1;
    for (int i = 0; i < board.size(); ++i) {
        for (int j = 0; j < board[i].size(); ++j) {
            if (board[i][j] == 0) {
                y = i;
                x = j;
                break;
            }
        }
        if (y != -1) {
            break;
        }
    }

    //初始部分： 已覆盖所有白格子，则返回1.
    if (y == -1) {
        return 1;
    }

    int ret = 0;
    for (int type = 0; type < 4; type++) {
        //如果能以type的形式覆盖board[y][x], 就进行递归调用
        if (set(board, y, x, type, 1)) {
            ret += cover(board);
        }
        set(board, y, x, type, -1);

    }
    return ret;

}




int main() {
#ifdef ONLINE_JUDGE
#else
    freopen("F:\\ClionProjects\\Algorithm\\input.txt", "r", stdin);
//    freopen("F:\\ClionProjects\\Algorithm\\output.txt", "w", stdout);
#endif
    int C = 0, H = 0, W = 0;
    scanf("%d", &C);
//    printf("%d\n", C);


    while (C--) {
        scanf("%d %d", &H, &W);
        vector<vector<int>> board(H, vector<int>(W));
        char ch;
        for (int i = 0; i < H; i++) {
            for (int j = 0; j < W; j++) {
                scanf(" %c", &ch);
                if (ch == '#') {
                    board[i][j] = 1;
                } else {
                    board[i][j] = 0;
                }
            }
        }

        int ways = cover(board);
        printf("%d\n", ways);
    }
    return 0;
}
```
