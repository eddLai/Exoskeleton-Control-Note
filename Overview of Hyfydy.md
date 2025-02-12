一個檔案HyFyDy.scone檔案只能有一個model(來自.hfd)
- 可以動態調整contact嗎(有開端口嗎)
- Gym裡頭可以調用兩個物件嗎
- 在現有環境已入控制器權重

```
model {
    name = my_model 
    body {
        name = my_body
        mass = 3
        inertia = [ 1.5 1.5 1.5 ]
        pos = [ 0 1 0 ] # single-line comment
    }
    /* multi line
    comment */
}
```

- 可以選material: contact forces
- 
