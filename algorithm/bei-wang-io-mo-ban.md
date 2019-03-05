# IO模板

* 不少网络笔试不像 LeetCode 帮你完成 I/O，需要手动完成
* 如果没有 ACM 经验，很可能会在这上面浪费不少时间
* 这里总结了几种常见的 IO 模板，分别提供了 C/C++ 和 Python\(TODO\) 代码

## Index

* [输入不说明有多少个 Input，以 EOF 为结束标志](bei-wang-io-mo-ban.md#输入不说明有多少个-input以-eof-为结束标志)
  * [C](bei-wang-io-mo-ban.md#c)
  * [C++](bei-wang-io-mo-ban.md#c)
* [输入不说明有多少个 Input，以某个特殊输入为结束标志](bei-wang-io-mo-ban.md#输入不说明有多少个-input以某个特殊输入为结束标志)
  * [C](bei-wang-io-mo-ban.md#c-1)
  * [C++](bei-wang-io-mo-ban.md#c-1)
* [指示有 N 个 Input](bei-wang-io-mo-ban.md#指示有-n-个-input)
  * [C](bei-wang-io-mo-ban.md#c-2)
  * [C++](bei-wang-io-mo-ban.md#c-2)
  * [Python3](bei-wang-io-mo-ban.md#python3)
* [指示有 N 组输入，并以某个特殊输入退出](bei-wang-io-mo-ban.md#指示有-n-组输入并以某个特殊输入退出)
  * [C/C++](bei-wang-io-mo-ban.md#cc)
* [输入是一整行（包括空格）](bei-wang-io-mo-ban.md#输入是一整行包括空格)
  * [用 char\[\] 接收（C/C++）](bei-wang-io-mo-ban.md#用-char-接收cc)
  * [用 string 接收（C++）](bei-wang-io-mo-ban.md#用-string-接收c)
* [输入是多行（包括空格）](bei-wang-io-mo-ban.md#输入是多行包括空格)
  * [C++](bei-wang-io-mo-ban.md#c-3)
* [从文件读取](bei-wang-io-mo-ban.md#从文件读取)
  * [C](bei-wang-io-mo-ban.md#c-3)
  * [C++](bei-wang-io-mo-ban.md#c-4)

## 输入不说明有多少个 Input，以 EOF 为结束标志

### C

```c
int a, b;
// scanf 返回值为变量的个数，如果没有返回 -1，EOF 是一个预定义的常量 -1
while (scanf("%d %d", &a, &b) != EOF) {  
    // ...
}
```

### C++

```cpp
int a, b;
while (cin >> a >> b) {
    // ...
}
```

## 输入不说明有多少个 Input，以某个特殊输入为结束标志

### C

```c
// 示例 1
int a, b;
while (scanf("%d %d", &a, &b) != EOF && (a != 0 && b != 0)) {
    // ...
}

// 或者
while (scanf("%d %d", &a, &b) != EOF && (a || b)) {
    // ...
}

// 示例 2
int n;
while (scanf("%d", &n) != EOF && n != 0) {
    // ...
}
```

### C++

```cpp
// 示例 1
int a, b;
while (cin >> a >> b) {
    if (a == 0 && b == 0)
        break;
    // ...
}

// 示例 2
int n;
while (cin >> n && n != 0) {
    // ...
}
```

## 指示有 N 个 Input

### C

```c
int n;
scanf("%d", &n);

int a, b;
for (int i = 0; i < n; i++) {
    scanf("%d %d", &a, &b);
    // ...
}
```

### C++

```cpp
int n;
cin >> n;

int a, b;
while(n--) {
    cin >> a >> b;
}
```

### Python3

```python
n = int(input())
for _ in range(n):
    # ...
```

## 指示有 N 组输入，并以某个特殊输入退出

### C/C++

```cpp
int n;
while (cin >> n && n != 0) {
    int a, b;
    for (int i = 0; i < n; i++) {
        cin >> a >> b;
        // ...
    }
}
```

## 输入是一整行（包括空格）

### 用 char\[\] 接收（C/C++）

```cpp
const int MAXN = 1000;
char buff[MAXN];

// C
gets(buff);
puts(buff); // 输出

// C++
cin.getline(buff, MAXN);  // 第三个参数默认是 '\n'
cin.getline(buff, MAXN, '\n');
```

### 用 string 接收（C++）

```cpp
string s;
getline(cin, s);          // 第三个参数默认是 '\n'
getline(cin, s, '\n');
```

## 输入是多行（包括空格）

### C++

```cpp
int n;
cin >> n;
cin.get();  // 否则，n 也会计入下面的 getline()，导致少一组数据

while (n--) {
    string s;
    getline(cin, s);
}
```

## 从文件读取

### C

```c
FILE *cfin = fopen("in.txt", "r");
FILE *cfout = fopen("out.txt", "w");

int a, b;
// 注意要传入文件指针
while (fscanf(cfin, "%d %d", &a, &b) != EOF) { // 类似的，把 scanf 替换成 fscanf
    fprintf(cfout, "%d\n", a + b);             // 把 printf 替换为 fprintf
}

fclose(cfin);
fclose(cfout);
```

### C++

```cpp
ifstream fin("in.txt");
ofstream fout("out.txt");

int a, b;
while (fin >> a >> b) {
    fout << a + b << endl;
}

fin.close();
fout.close();
```

