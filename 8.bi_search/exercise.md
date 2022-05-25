# 2249

二分查找
在有序的基础上使用二分查找函数

```C++
//
// Created by 王 on 2022/5/23.
//
#include "iostream"
#include "cstdio"
#include "cstring"
#include "algorithm"
#define F(i, a, b) for(int i = a;i <= b;i++)
using namespace std;

#define MAXN 1000010

int a[MAXN],m,n,q;

int find(int x){
    int l = 1,r = n;
    int mid;

    while (l<r){

        mid = (l+r)/2;

        if(a[mid] >= x){
            r = mid;
        } else
            l = mid + 1  /* +1 */;
    }

    if(a[l] == x) return l;
    else return -1;

}

int main(){
    cin >> n>>m;

    F(i,1,n) cin >> a[i];

    F(i,1,m) {
        cin >> q;
        cout << find(q) <<' ';
    }
    return  0;
}



```

# 1102
```C++

/*
 * 1102
 */
typedef long long LL;
#define MAXN 200010
LL a[MAXN];
int n,c;
int main(){
    cin >> n >>c;
    F(i,1,n) scanf("%lld",&a[i]);
    sort(a+1,a+1+n);
    LL tot = 0;
    F(i,1,n)
        tot += upper_bound(a + 1, a + 1 + n, a[i] + c) - lower_bound(a + 1, a + n + 1, a[i] + c);
    /*
     * upper_bound(begin,end,val) ,返回地址， bigin ~ end最后出现 val 的地址
     * lower_bound(begin,end,val) ,返回地址， bigin ~ end首次出现 val 的地址
     */
    cout << tot;
}


```

# 二分答案 1873
``` c++
/*
 * 二分答案
 * 1873
 */

#define maxn 1000010
typedef long long LL;
LL a[maxn],n,m;

// 判别 高度
bool P(int h){
    LL tot = 0;
    F(i,1,n) if(a[i] > h) tot += a[i] - h;
    return tot >= m;
}

int main(){
    cin >> n >>m;
    F(i,1,n) scanf("%lld",&a[i]);
    int l = 0,r = 1e9,ans,mid;
    while (l <= r)
        if(P(mid = (l + r) >> 1)) ans = mid,l = mid +1;
        /*
         * >>1 ：右移1位，相当于除以二
         * << 1 : 左移1位，相当于乘以2
         */
        else r = mid - 1;
    printf("%d",ans);
}

```