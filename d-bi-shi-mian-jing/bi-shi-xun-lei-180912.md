# 迅雷

* 单选 10，多选 10，编程 2

## Index

* [AI-A-01](bi-shi-xun-lei-180912.md#ai-a-01)
* [AI-A-02](bi-shi-xun-lei-180912.md#ai-a-02)

## AI-A-01

**Python**（AC）

```python
A = list(map(int, input().split(',')))

def foo(A):
    for i in range(1, len(A) - 1):

        if sum(A[:i]) == A[i] and A[i] == sum(A[i + 1:]):
            return i

    return False

ret = foo(A)
if ret:
    print(A[ret])
else:
    print("False")
```

## AI-A-02

**Python**（AC）

```text
IN = input()

a1, a2k = IN.split('-')
a1 = list(map(int, a1.split(',')))
a2, k = a2k.split(':')
a2 = list(map(int, a2.split(',')))
k = int(k)

# print(a1)
# print(a2)
# print(k)

tmp = []
for i in a1:
    tmp += [i + t for t in a2]

print(','.join(list(map(str, sorted(tmp, reverse=True)))[:k]))
```

