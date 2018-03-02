关于tableVIew滚动逻辑

如果想要滚动的时候立马停止之前已经出发的滚动动画

在跳转的制定位置的btn逻辑里面加上

[self.tableView setContentOffset:self.tableView.contentOffset animated:NO];//表示立即固定在当前的滚动窗口状态。



example

```objective-c
- (void)tapScrollBottomBtn:(id)sender {
    //相当于立即停止当前的滚动，执行下面的操作
    [self.tableView setContentOffset:self.tableView.contentOffset animated:NO];
    [self scrollToBottomWithAnimated:YES];
}
```

