# block

简单语法网站：[fuckingblocksyntax](http://fuckingblocksyntax.com/)

简单来说，声明的方式就是C语言声明函数的语法，将functionName替换成(^funcitonName)的形式



调用的时候因为不需要name了，所以作为赋值或者作为实参传递的block不需要block的name了

void (^)(parameter) {}

在作为值进行传递的时候void可以省略掉

```objective-c
//返回值是BOOL的Block
[[statements objectsPassingTest:^BOOL(FMStatement* statement, BOOL *stop) {
        *stop = ![statement inUse];
        return *stop;
}] anyObject];
//头文件
- (NSSet<ObjectType> *)objectsPassingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, BOOL *stop))predicate
```

```objective-c
//这里的Block因为返回值是Void，所以省略了
[self.skuImageView scs_setImageURL:[NSURL URLWithString:model.goodsImageURL] placeholderImage:[UIImage scsImageScsBundlePNGWithNamed:kSCSOrderCellPlaceholderImageName] success:^(UIImage *image) {
	ws.skuImageView.image = image;
} failure:nil];

//头文件
- (void)scs_setImageURL:(NSURL *)imageURL placeholderImage:(UIImage *)placeholderImage success:(void (^)(UIImage *image))success failure:(void (^)(NSError *error))failure;
```

