# Swift笔记

### optional相关内容

1. optional binding ： 用于判断一个可选类型是否含有值，一般通过条件控制语句和let搭配完成，let 用于将可选类型的值保存在一个临时变量里面。

   Sample code:

   ```swift
   if let actualNumber = Int(possibleNumber) {
       print("\"\(possibleNumber)\" has an integer value of \(actualNumber)")
   } else {
       print("\"\(possibleNumber)\" could not be converted to an integer")
   }
   //这里的actualNumber就不是可选类型了，他是possibleNumebr里面解析出来的Int值，生命周期为当前的整个if语法块。
   ```

2. implicity unwrapped：加感叹号，类型等同于常规类型。这个可以视作自动取值的可取类型。可以直接赋值给常规类型。

   ```swift
   var testStringO:String? = "hello"
   let receiveString:String = testStringO //报错
   let receiveString:String = testStringO! //编译通过

   let testString:String! = "hello"
   let receiveString = testString //变异通过

   //同理，！类型也能够使用binding
   if let saveString = testString {
     //拆开分析，if判断的是 let saveString = testString，这条语句的结果就是saveString本身的值，如果为Nil就不会打印，如果有值得话才会进入下面的逻辑
     print(saveString)
   }
   ```

   ​

### enforce precondition

类似一种保险条件，跟断言方式很像，但是判断逻辑跟断言相反，是precondition条件本身为false的时候才会进行检查。

```Swift
precondition(index > 0, "Index must be greater than zero.");
//上述语句只有在index小于等于0的时候才会中！
```



### 运算符汇总

> 专业词汇：运算符的类型Unary(单目),Binary,Ternary(三目)

1. Swift中的赋值运算符 = 并不会反悔值，也就是说下面这条语句并不能通过编译，因为 a = b这句话返回的并不是值。 系统帮你拦截，防止你本来想写 == 结果错写成 = 

```Swift
if x = y {
  //不会被执行
}
```

2. \+ 运行算符也支持String类型的拼接

3. 可选类型特有运算符 **??**  syntax的格式为：

   ```swift
   let a:Int? = 3
   let b:Int = 4
   //a必须是可选类型，b必须是常规类型并且跟a的取值类型一致，也就是Int的可选只能对应Int的常规
   let testVal = a ?? b
   //这种语法的使用场景在于各种给默认值的场合
   ```

4. 范围运算符

   * 全闭 1…5   1到5
   * 半闭 1..<5 1到4
   * 集合类型的切片
     * array[…2] 数组中的0，1，2
     * array[2….]数组中的 2，以后的数据
     * array[..<2]数组中的0，1

   ！！范围运算符能单独表意

   ```Swift
   let range = ...2
   range.contain(3)  //return false
   range.contain(1)  //yes
   ```

   ​

### String类型

1. 关键是append方法，这个方法返回的不是String类型，只是单纯作为append修改了调用append的String变量本身！

2. String有着类似数组的索引，String.startIndex, .endIndex, .Index ; index可以搭配offset找到制定位置的字符，syntax是

   ```Swift
   let greeting = "Guten Tag!"
   greeting[greeting.startIndex]
   // G
   greeting[greeting.index(before: greeting.endIndex)]
   // !
   greeting[greeting.index(after: greeting.startIndex)]
   // u
   let index = greeting.index(greeting.startIndex, offsetBy: 7)
   greeting[index]
   // a
   ```

   ​