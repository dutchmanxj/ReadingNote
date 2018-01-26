

# UIButton相关设置

UIButton里面可以加text和image。

但是UIButton苹果默认的排列方式是左边image右边text，想要修改这个默认设置，要用到Edge。

详细代码如下：

```objective-c
[button setTitleEdgeInsets:UIEdgeInsetsMake(0, - button.imageView.image.size.width, 0, button.imageView.image.size.width)];
[button setImageEdgeInsets:UIEdgeInsetsMake(0, button.titleLabel.bounds.size.width, 0, -button.titleLabel.bounds.size.width)];
//通过上述设置能够让图片和titleLabel的位置反过来
```

