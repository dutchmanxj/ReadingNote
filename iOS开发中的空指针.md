# nil,Nil,NULL,NSNULL的区别

`NULL`、`nil`、`Nil`这三者对于`Objective-C`中值是一样的，都是`(void *)0`，那么为什么要区分呢？又与`NSNull`之间有什么区别：

- `NULL`是宏，是对于`C`语言指针而使用的，表示空指针
- `nil`是宏，是对于`Objective-C`中的对象而使用的，表示对象为空
- `Nil`是宏，是对于`Objective-C`中的类而使用的，表示类指向空
- `NSNull`是类类型，是用于表示空的占位对象，一般用于集合元素中的占位。



NSNull常见用法：

```objective-c
NSArray *array = [NSArray arrayWithObjects:
                      [[NSObject alloc] init],
                      [NSNull null],
                      @"aaa",
                      nil,
                      [[NSObject alloc] init],
                      [[NSObject alloc] init], nil];

NSLog(@"%ld", array.count); // 输出 3，NSArray以nil结尾,用这种方式申明的数组以nil作为结尾，所以中间的nil会让数组提前结束。
```





1.日期格式优化
2.下拉动作交互样式优化
3.系统消息标准化
4.气泡格式优化