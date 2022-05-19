# 贪心算法

## 2240 部分背包

```C++
//
// Created by 王 on 2022/5/19.
//
#include "iostream"
#include "cstdio"
#include "cstring"
#include "algorithm"
#define F(i, a, b) for(int i = a;i <= b;i++)
using namespace std;

typedef struct coin{
    int m;
    int v;
    float d;
}coin;

int cmp(coin a,coin b){
    return a.d > b.d;
}

coin coin_heap[105];
int N;
int T;
float value = 0;

int main(){
    cin >> N >> T;

    F(i,1,N) {
        cin >> coin_heap[i].m >> coin_heap[i].v;
        coin_heap[i].d = (float)coin_heap[i].v / (float)coin_heap[i].m;
    }
//    F(i,1,N) cout << coin_heap[i].d << ' ';
//    cout << endl;
    sort(coin_heap+1,coin_heap+1+N, cmp);
//    F(i,1,N) cout << coin_heap[i].d << ' ';

    F(i,1,N){
        if(coin_heap[i].m < T) {
            T -= coin_heap[i].m;
            value += (float)coin_heap[i].v;
        } else{
            value += coin_heap[i].d * (float)T;
            break;
        }
    }

    printf("%.2f",value);
}
```

## 值得注意的点

+ 在cmp函数中，可以使用交叉相乘的算法，避免浮点数的除法运算

```C++
bool cmp(Node aa,Node bb){//定义排序方法
	return aa.v*bb.w>aa.w*bb.v;//按性价比从高到低排序，为防止精度问题直接交叉相乘
}
```

+ 并不是动态规划的背包问题，日后在探索真正的背包问题...
