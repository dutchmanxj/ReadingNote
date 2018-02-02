# GCD逻辑

> 因为不经常使用GCD的缘故，到时一些借口的写法都有些生疏了，蛋疼不行，在这里记录一下

1. 在主线程执行逻辑

```objective-c
 dispatch_async(dispatch_get_main_queue(), ^{
   		//在主线程执行逻辑
        [_circleProgressBar setProgress:progress animated:YES];
    });
```

