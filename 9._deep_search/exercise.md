# 1219 八皇后
```c++
//
// Created by 王 on 2022/5/27.
//
#include "iostream"
#include "cstdio"
#include "cstring"
#include "algorithm"

#define F(i, a, b) for(int i = a;i <= b;i++)
using namespace std;

#define maxn 100

int a[maxn];
int b1[maxn],b2[maxn],b3[maxn];
int n,ans=0;

void dfs(int x){

    /*
     * 所有皇后已经放置
     */
    if(x > n){
        ans ++;
        if(ans <= 3){
            F(i,1,n)    printf("%d ",a[i]);
            puts(" ");
        }
        return;
    }

    /*
     * 递归
     */
    F(i,1,n){
        if(b1[i] == 0 && b2[x+i] == 0 && b3[x-i+15] ==0){
            a[x] = i; //记录位置
            b1[i] = 1; b2[x+i] = 1; b3[x-i+15] = 1; //占位
            dfs(x+1); // 下一层递归
            b1[i] = 0; b2[x+i] = 0; b3[x-i+15] = 0; //取消占位
        }
    }
}

int main(){
    cin >> n;
    dfs(1);
    printf("%d",ans);
    return 0;
}

```
