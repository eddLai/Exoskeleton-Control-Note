[[SWIG（Simplified Wrapper and Interface Generator）]]

`sys`：修改interpreter的位址，用來動態加載
`importlib.util`：用來確認加載

```python
sorted(pathlib.Path(path).glob('sconepy*.*'))

pathlib.Path.home()
```

```python
importlib.util.find_spec('sconepy')

sys.path.append(path_to_sconepy)
```

