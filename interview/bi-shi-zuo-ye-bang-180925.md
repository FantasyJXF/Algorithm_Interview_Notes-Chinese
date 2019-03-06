# 作业帮

## 笔试-作业帮-180925

* 单选 5，填空 5，编程 2，问答 2
* 编程不允许跳出页面

### Index

* [1. 点对距离](bi-shi-zuo-ye-bang-180925.md#1-点对距离)
* [2. 扩展型表达式求值](bi-shi-zuo-ye-bang-180925.md#2-扩展型表达式求值)

### 1. 点对距离

**Python**（60%）

* 试了各种情况，不知道哪里有问题

  \`\`\`python

  from math import ceil, floor

def foo\(ax, ay, bx, by\): d = \(\(ax - bx\)**2 + \(ay - by\)**2\)\*\*0.5

```text
#return round(d, 5)
return d
```

k = int\(input\(\)\) n = int\(input\(\)\)

P = \[\] for \_ in range\(n\): x, y = list\(map\(float, input\(\).split\(\)\)\) P.append\(\[x, y\]\)

D = \[\] for i in range\(n\): for j in range\(i+1, n\): d = foo\(P\[i\]\[0\], P\[i\]\[1\], P\[j\]\[0\], P\[j\]\[1\]\) D.append\(d\)

D.sort\(\)

## print\(D\)

N = len\(D\) - 1

## print\(N\)

## print\(ceil\(N \* \(k / 100\)\)\)

ans = D\[ceil\(N \* \(k / 100\)\)\]

## print\("%0.5f" % ans\)

print\(round\(ans, 5\)\)

## print\(ans\)

```text
## 2. 扩展型表达式求值

<div align="center"><img src="../_assets/TIM截图20180925203442.png" height="" /></div>
<div align="center"><img src="../_assets/TIM截图20180925203454.png" height="" /></div>
<div align="center"><img src="../_assets/TIM截图20180925203504.png" height="" /></div>

**Python**（57.14%）
- 不能跳出页面，实在不想写这种题，偷鸡过了 57%
```python
def bar(s):
    while "%" in s:
        i = s.find("%")
        j = i - 1
        while s[j].isdigit():
            j -= 1

        s = s[:j+1] + str(int(s[j+1: i]) / 100) + s[i+1:]
    return s

def foo(s):
    if "**" in s or "++" in s or "--" in s:
        return "error"

    s = bar(s)

    try:
        ans = eval(s)
        if isinstance(ans, int):
            return "%d" % ans
        else:
            return "%0.3f" % ans
            #return round(ans, 3)
    except e:
        return "error"

s = input()
ans = foo(s)
#print(bar(s))
print(ans)
```

