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
# 2392
之前没有学深度搜索，在暴力枚举里面接触此题未通过

```c++
int nowtime, maxtime, sum;    //子集中的时间和、最大合法时间和、该课作业总时长
int ans, maxdeep;   //答案、最深递归层层数限制
int s[4], a[21];    //每科作业数量、每个作业耗时

void dfs(int x) {
    if (x > maxdeep) {//所有作业枚举完毕，达到了最大递归层数
        maxtime = max(maxtime, nowtime); //如果解更优，更新答案
        return;
    }

    if (nowtime + a[x] <= sum / 2) {  //如果这个作业合法，选择它加入nowtime
        nowtime += a[x];    //增加子集中这道题目的时间
        dfs(x + 1);     //下一层
        nowtime -= a[x];    //去除子集中这道题的时间
    }
    dfs(x + 1);    //不选这个题目，直接进行下一层递归
}

int main() {
    F(i, 0, 3) cin >> s[i];
    F(i, 0, 3) {
        nowtime = 0;    maxtime = 0;     maxdeep = s[i];        sum = 0;     //每一科的初始化
        F(j,1,s[i]) {cin >> a[j]; sum += a[j];}     //输入耗时 & 记录总耗时
        dfs(1); //开始枚举第一个题目
        ans += (sum - maxtime); //加上答案
    }
    cout << ans;
    return 0;
}

```