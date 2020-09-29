# 范围for
## 语法
```c++
for(变量声明: 序列型对象){
    语句;
}
```
变量声明声明一个变量，序列型对象则定义了要历遍的对象。变量会自动储存好序列对象的下一个对象。然后执行语句一次。
## 例子
```c++
#include<bits/stdc++.h>
using namespace std;
int main(){
    string s("I am the wise man!");
    for(char c : s){
        cout<<c<<endl;
    }
    return 0;
}
```
