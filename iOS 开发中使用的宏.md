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

4. 最常用的weakself宏

   ```objective-c
   #define weakify(object) autoreleasepool{} __weak __typeof__(object) weak##_##object = object;
   //使用方法
   ```

   ​