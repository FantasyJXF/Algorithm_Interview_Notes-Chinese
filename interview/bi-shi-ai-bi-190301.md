# 爱笔

## 笔试题

1. 单词逆转
2. 输入n,计算nx1,nx2,.....,nxxxx,直到0~9所有的数字都出现,求最小n
3. 实现strcpy
4. 编程实现多态
5. 括号匹配

## 题解

1. 单词逆转

```cpp
#include<iostream>
#include <string>
#include<stdio.h>

using namespace std;

void Reverse(char *pBegin, char *pEnd)
{
    if (pBegin == nullptr || pEnd == nullptr)
        return;

    while (pBegin < pEnd)
    {
        char temp = *pBegin;
        *pBegin = *pEnd;
        *pEnd = temp;

        pBegin++, pEnd--;
    }
}

char* ReverseSentence(char *pData)
{
    if (pData == nullptr)
        return nullptr;

    char *pBegin = pData;

    char *pEnd = pData;
    while (*pEnd != '\0')
        pEnd++;
    pEnd--;

    // 翻转整个句子
    Reverse(pBegin, pEnd);

    // 翻转句子中的每个单词
    pBegin = pEnd = pData;
    while (*pBegin != '\0')
    {
        if (*pBegin == ' ')
        {
            pBegin++;
            pEnd++;
        }
        else if (*pEnd == ' ' || *pEnd == '\0')
        {
            Reverse(pBegin, --pEnd);
            pBegin = ++pEnd;
        }
        else
            pEnd++;
    }

    return pData;
}

int main(int argc, char* argv[])
{
    char input[100];
    cin.get(input, 100);

    char *ret = ReverseSentence(input);

    while(*ret != '\0')
        cout << *ret++;

    cout << endl;

    return 0;
}
```

1. 输入n,计算nx1,nx2,.....,nxxxx,直到0~9所有的数字都出现,求最小n
2. 实现strcpy

```cpp
#include <assert.h>
#include <stdio.h>

char* strcpy(char* des, const char* src)
{
    assert((des!=NULL) && (src!=NULL)); 
    char *address = des;  
    while((*des++ = *src++) != '\0')  
        ;  
    return address;
}
```

1. 编程实现多态

```cpp
#include <iostream> 
using namespace std;

class Shape {
   protected:
      int width, height;
   public:
      Shape( int a=0, int b=0)
      {
         width = a;
         height = b;
      }
      int area()
      {
         cout << "Parent class area :" <<endl;
         return 0;
      }
};
class Rectangle: public Shape{
   public:
      Rectangle( int a=0, int b=0):Shape(a, b) { }
      int area ()
      { 
         cout << "Rectangle class area :" <<endl;
         return (width * height); 
      }
};
class Triangle: public Shape{
   public:
      Triangle( int a=0, int b=0):Shape(a, b) { }
      int area ()
      { 
         cout << "Triangle class area :" <<endl;
         return (width * height / 2); 
      }
};
// 程序的主函数
int main( )
{
   Shape *shape;
   Rectangle rec(10,7);
   Triangle  tri(10,5);

   // 存储矩形的地址
   shape = &rec;
   // 调用矩形的求面积函数 area
   shape->area();

   // 存储三角形的地址
   shape = &tri;
   // 调用三角形的求面积函数 area
   shape->area();

   return 0;
}
```

1. 括号匹配

就是一个`stack`,跟`top`比较

```cpp
#include <iostream>
#include <stack>
#include <string>

bool paren(const std::string &str)
{
    std::stack<char> s;
    for (auto i = 0; i < str.size();i++)
    {
        switch (str[i])
        {
        case '(':s.push(str[i]); break;
        case '[':s.push(str[i]); break;
        case '{':s.push(str[i]); break;
        case ')':
            if (s.top() != '(')
                return false;
            else
                s.pop(); break;
        case ']':
            if (s.top() != '[')
                return false;
            else
                s.pop(); break;
        case '}':
            if (s.top() != '{')
                return false;
            else
                s.pop(); break;

        default:
            break;
        }
    }
    return s.empty();
}

int main()
{
    std::string strBuf = "()[]{}[()]";
    std::cout << "The string is : " << strBuf<<" ";
    if (paren(strBuf))
        std::cout << "括号匹配";
    else
        std::cout << "括号不匹配";
    std::cout << std::endl;
    return 0;
}
```

