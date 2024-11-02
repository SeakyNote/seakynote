## lua脚本持续打印字符串30s
```lua
    local start_time = os.time()  -- 获取当前时间
    local duration = 30           -- 设置持续时间为30秒
    local message = "Hello, World!" -- 要打印的字符串

    while os.time() - start_time < duration do
        print(message)
        os.execute("sleep 1")     -- 让程序等待1秒，避免打印太快
    end
```
