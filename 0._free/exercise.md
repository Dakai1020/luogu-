# 1789

RE 60分
未解决数组越界
```c++
#include "iostream"
#include "cstdio"
#include "cstring"
#include "algorithm"

#define F(i, a, b) for(int i = a;i <= b;i++)
using namespace std;


//初始化
int matrix[110][110];
int n, m, k;
int x, y;

int main() {
    int cnt = 0;
    memset(matrix, 0, sizeof matrix);
    cin >> n >> m >> k;

    F(ii, 1, m) {
        cin >> x >> y;
        for (int i = x - 1; i <= x + 1; i++)
            for (int j = y - 1; j <= y + 1; j++) matrix[i][j] = 1;
        matrix[x - 2][y] = 1;
        matrix[x + 2][y] = 1;
        matrix[x][y - 2] = 1;
        matrix[x][y + 2] = 1;
    }

        F(ii, 1, k) {
            cin >> x >> y;
            for (int i = x - 2; i <= x + 2; i++)
                for (int j = y - 2; j <= y + 2; j++)
                    matrix[i][j] = 1;
        }

    F(i, 1, n)F(j, 1, n)if (!matrix[i][j]) cnt++;
    cout << cnt ;

}
```
