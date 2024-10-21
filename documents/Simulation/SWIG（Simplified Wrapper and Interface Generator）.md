可以用來生成高效率的python接口

需要Interface File `*.i` or  `*.swg`
寫法：
- header file 或 declaration 不需要compile

C wrapper
Default arguments
`void bar(int x, int y = 3, int z = 4);`
明確宣告使用不同數量的參數所需要的量
```
void bar(int x, int y, int z);
void bar(int x, int y);
void bar(int x);
```

swig -python speedup_performance.i
會產生
- `.py`
- `.c`：需要編譯成shared library

python動態加載