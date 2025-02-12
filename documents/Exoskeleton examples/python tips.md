`mid_activation: nn.Module = nn.ReLU`參數中用:來註解建議使用的變數型
`Iterable`是一个来自`collections.abc`模块（或在较新版本的Python中，直接從`typing`模塊導入）
在`nn.Sequential(*layers)`中的`*`符号：用於unpacking，作用給可迭代对象（如列表、元组）中的元素解包成位置参数传递给函数
`zip`將兩個list變成tuplel list `[(1, 'A'), (2, 'B'), (3, 'C'), (4, 'D'), (5, 'E')]`

argpase方法：用於將Scirpt做成應用
```python
import argparse
# 創建 ArgumentParser 對象
parser = argparse.ArgumentParser(description="命令行參數示例")
# 添加一個布林型參數，使用 store_true 作為 action，表示如果出現參數則將其設置為 True
parser.add_argument("--flag", action="store_true", help="這是一個布林型參數")
# 添加一個必填的字串參數
parser.add_argument("-n", "--name", required=True, help="必填的名稱參數")
# 解析命令行參數
args = parser.parse_args()
# 打印參數值
print("flag 參數的值:", args.flag)
print("name 參數的值:", args.name)
print(args)
```

`args = parser.parse_args()`會返回所有剛剛有指定儲存的變數