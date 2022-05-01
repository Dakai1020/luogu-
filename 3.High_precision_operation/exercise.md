# 高精度运算

几百位以上的运算，使用数组模拟位数

## p1601 A + B 高精度

```C++
//
// Created by 王 on 2022/4/27.
//

#include "iostream"
#include "string"
#include "algorithm"
using namespace std;

/*
 * A + B 高精度
 * 使用数组
 */

#define MAXN 510
int num1[MAXN],num2[MAXN],result[MAXN];
/*
 * 把字符串的数字转换为int数组，数组的低位存放数字低位，即是字符串的高位
 */
void  string_to_num(string s,int num[MAXN]){
    for (int i = s.length()-1,j = 1; i >= 0 ; --i) {
        num[j++] = s[i] - '0';
    }
}

int main(){
    string A,B;
    cin >> A;
    cin >> B;
    string_to_num(A,num1);
    string_to_num(B,num2);

    int len = max(A.length(),B.length());

    for (int i = 1; i <= len ; ++i) {
        result[i] +=  num1[i] + num2[i];
        result[i + 1] = result[i] / 10; //进位
        result[i] %= 10;
    }
    /*
     * 最后一位数进位可能会导致len++
     */
    if(result[len + 1])
        len ++;

    for (int i = len; i >= 1; --i) {
        cout << result[i];
    }
}

```

## A*B

```C++
/*
 * A * B 高精度
 */

int main(){
    //输入
    string A,B;
    cin >> A;
    cin >> B;
    string_to_num(A,num1);
    string_to_num(B,num2);

    //实现 A + B 中间值 过渡
    int lena = A.length(),lenb = B.length();

    for(int i = 1;i <= lena;i ++){
        for(int j =  1; j <= lenb; j++){
            result[i + j - 1] += num1[i] * num2[j];
        }
    }
    int len = lena + lenb;


    //处理进位
    for(int i = 1; i <= len; i ++ ){
        result[i+1] += result[i] / 10;
        result[i] %= 10;
    }

    for(;!result[len];)  len --; //去除高位0

        for (int i = max(1,len); i >= 1; --i) {
        cout << result[i];
    }

}
/*
 * len小于1问题
 * 数组长度问题
 */


```

## p1009
```C++
#define maxn 100
/*
 * p1009 阶乘之和
 * 思想：封装大整数类并重载运算
 */
struct Bigint{
    //属性
    int len, a[maxn];

    //初始化 默认0
    Bigint(int x = 0){
        memset(a,0,sizeof (a));
        for(len = 1; x; len ++){
            a[len] = x % 10, x /= 10;
        }
        len -- ;
    }

    //重载[]
    int &operator[](int i){
        return a[i];
    }

    //处理1~L长度的进位并且重置长度
    void flatten(int L){
        len = L;
        for(int i = 1; i <= len; i ++){
            a[i + 1] += a[i] / 10, a[i] %= 10;
        }
        for(;!a[len];)  //重置长度为有效长度
            len --;
    }

    void print(){
        for (int i = max(1,len); i >= 1 ; --i) {
            printf("%d",a[i]);
        }
    }


};


/* 重载运算符*/
Bigint operator+(Bigint a, Bigint b){
    Bigint c;
    int len = max(a.len,b.len);

    for(int i = 1; i <= len; i++){
        c[i] += a[i] + b[i];
    }

    c.flatten(len + 1); //相加，答案不超过 len+1位
    return c;
}

Bigint operator*(Bigint a, int b){
    Bigint c;
    int len = a.len;
    for(int i = 1; i <= len; i ++)
        c[i] = a[i] * b;

    c.flatten(len + 11);

    return c;
}


int main(){
    Bigint ans(0),fac(1);

    int m;
    cin >> m;
    for(int i = 1; i <= m; i ++){
        fac = fac * i;
        ans = ans + fac;
    }
    ans.print();
}


```

## p 1591 1000位阶乘
使用之前定义的结构体
```C++

/*
 * p1591
 */

int main() {


    int t;
    cin >> t;
    int n, a;
    int cnt;

    for (int i = 1; i <= t; i++) {
        cnt = 0;
        Bigint ans(1);
        cin >> n >> a;

        for (int j = 1; j <= n; j++) {
            ans = ans * j;
        }


        for (int k = ans.len; k >= 1; k--) {
            if (ans[k] == a)
                cnt ++;
        }

        cout << cnt <<endl;

    }

}

```

## p1405

```C++

/*
 * 常规做法 40分 艹
 */
//int main() {
//    long long P;
//    cin >> P;
//    Bigint a(1);
//    for (int i = 1; i <= P; i++)
//        a = a * 2;
//    a = a + Bigint(-1);
//    a.print();
//    printf("\n");
////    Bigint(-3).print();
//    int len = a.len;
//
//
//    printf("%d\n", len);
//
//
//
//    int digit[501];
//    memset(digit, 0, sizeof(digit));
//
//    if(a.len <= 500){
//        for(int i = 1; i <= a.len; i ++){
//            digit[i] = a[i];
//        }
//    }
//
//    if(a.len > 500){
//        for(int i = 1; i <= 500; i ++){
//            digit[i] = a[i];
//        }
//    }
//
//
//    int line = 0;
//
//    for(int i = 500; i >= 1 ; i --) {
//        printf("%d",digit[i]);
//        line ++;
//        if(line == 50){
//            printf("\n");
//            line = 0;
//        }
//
////    }
//
//
//}}
/*
 * 网上优质解法
 * 这题全是用快速幂的，其实可以不用，310万乘500等于15亿，常数好能过。题解里有一篇不用快速幂压位的解法，但是代码长得要死。所以，以下是30行以内的代码：（150ms以内）
首先，我们要计算位数。我们知道10^k有k+1位，而k=lg(10^k)。所以2^p的位数是lg(2^p)+1=p*lg(2)。那么把p读进来之后直接cout出位数就行了。
下面解决500位求值的问题：这里还是开一个a[501]的unsigned long long数组，记为ull，然后还是用每个元素表示1位数，没错，是1位数，这样时间够而且代码简单。每次乘一轮不要乘2，乘2^60（9乘以2的60次方刚好不会溢出），记得把p多减掉59就行了。然后你发现15亿除以60等于2500万，貌似可以...自己机器上只用了半秒。
代码：
 */
#include <iostream>
#include <cstdio>
#include <cmath>
using namespace std;
typedef unsigned long long ull;
ull a[501]={1};
int main()
{
    int p;
    cin>>p;
    cout<<(int)(p*log10(2))+1<<endl;//log10才是以十为底的对数
    for(;p>0;p-=60)//每次减掉60次幂
    {
        ull f=0;//进位
        for(int i=0;i<500;i++)
        {
            if(p>60)a[i]<<=60;
            else a[i]<<=p;//如果剩下的不够60了就不要乘60了，乘p
            a[i]+=f;
            f=a[i]/10;
            a[i]%=10;
        }
    }
    a[0]-=1;//千万不要忘记减1，否则你会和我第一次一样WA掉全部
    for(int i=499;i>=0;i--)
    {
        putchar(a[i]+'0');
        if(i%50==0)putchar('\n');
    }
    return 0;
}

```
