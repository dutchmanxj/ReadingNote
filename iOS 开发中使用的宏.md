# iOS开发中的宏

这篇相当于一个读书笔记一样的东西

1. \##这个符号表示链接两个参数的意思	

```objective-c
//example
#define JOIN(A,B) A##B
	
JOIN（A，B）
//输出 AB

```

2. \#这个符号表示将后面跟的参数转换成String类型

   ```objective-c
   //example
   #define JOIN(x) #x

   JOIN（x）
   //输出 "x"
   ```

   ​

3. 宏命令虽然一般都是一行，但是如果要换行显示（为了可读性）可以先写一个转义符号\，然后再换行就可以了。

   ```objective-c
   //objc中MIN使用的宏
   #define __NSMIN_IMPL__(A,B,L) ({ __typeof__(A) __NSX_PASTE__(__a,L) = (A); \
                                    __typeof__(B) __NSX_PASTE__(__b,L) = (B); \
                                    (__NSX_PASTE__(__a,L) < __NSX_PASTE__(__b,L)) ? __NSX_PASTE__(__a,L) : __NSX_PASTE__(__b,L); \
                                 })
   ```

4. 最常用的weakself和strongself宏

   ```objective-c
   //学习了YYKit里面的写法
   #ifndef weakify
       #if DEBUG
           #if __has_feature(objc_arc)
           #define weakify(object) autoreleasepool{} __weak __typeof__(object) weak##_##object = object;
           #else
           #define weakify(object) autoreleasepool{} __block __typeof__(object) block##_##object = object;
           #endif
       #else
           #if __has_feature(objc_arc)
           #define weakify(object) try{} @finally{} {} __weak __typeof__(object) weak##_##object = object;
           #else
           #define weakify(object) try{} @finally{} {} __block __typeof__(object) block##_##object = object;
           #endif
       #endif
   #endif

   #ifndef strongify
       #if DEBUG
           #if __has_feature(objc_arc)
           #define strongify(object) autoreleasepool{} __typeof__(object) object = weak##_##object;
           #else
           #define strongify(object) autoreleasepool{} __typeof__(object) object = block##_##object;
           #endif
       #else
           #if __has_feature(objc_arc)
           #define strongify(object) try{} @finally{} __typeof__(object) object = weak##_##object;
           #else
           #define strongify(object) try{} @finally{} __typeof__(object) object = block##_##object;
           #endif
       #endif
   #endif

   //使用方法：
       @weakify(self)
       [self doSomething^{
           @strongify(self)
           if (!self) return;
           ...
       }];
   ```

   ​