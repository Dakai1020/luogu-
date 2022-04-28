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
