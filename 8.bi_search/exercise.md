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
