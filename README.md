

#Objective-C代码规范


#### 语言

应该使用US英语

应该：

```
UIColor *myColor = [UIColor whiteColor];

UIColor *backgroundColor = [UIColor greenColor];
```


不应该：

```
UIColor *myColour = [UIColor whiteColor]; （X 英式英语）

UIColor *beijingColor = [UIColor greenColor]; (X拼音)
```
#### 组织

在函数分组和protocol/delegate实现中使用“ #pragma mark - ” 来分类方法，要遵循以下一般结构：

```
#pragma mark - Lifecycle  
- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Public Method 
- (void)publicMethod {}

#pragma mark - Private Method
- (void)privateMethod {}

#pragma mark - Protocol conformance  
#pragma mark - UITextFieldDelegate
#pragma mark - Other Delegate...
#pragma mark - UITableViewDataSource  
#pragma mark - UITableViewDelegate  

#pragma mark - Getters & Setters  
- (id)customProperty {} 
```

###空格

* 缩进使用4个空格，确保在Xcode偏好设置来设置。
* 方法大括号和其他大括号(if/else/switch/while 等.) 总是在同一行语句打开但在新行中关闭（不强制，新一行开始也可以，但开始{和结束}对其）

应该
```
if (user.isHappy) {  
    //Do something  
} else {  
    //Do something else  
}  

或

if (user.isHappy) 
{  
    //Do something  
} 
else 
{  
    //Do something else  
}  
```

不应该
```
if (user.isHappy)  
{  
  //Do something  
}  
else {  
  //Do something else  
}  
```

* 在方法之间应该有且只有一行，这样有利于在视觉上更清晰和更易于组织。在方法内的空白应该分离功能，但通常都抽离出来成为一个新方法。
* 当一个函数有多个参数时并且超过100个字符时，调用时尽量使用多行冒号对齐的方式调用，参数中包含block的可以依情况而定。

应该
```
- (void)readLargeFile:(NSString *)filePath
           withObject:(id)object
           completion:(Void_Block)completion;


// blocks are easily readable  
[UIView animateWithDuration:1.0 animations:^{  
  // something  
} completion:^(BOOL finished) {  
  // something  
}];  

```

不应该

```
- (void)readLargeFile:(NSString *)filePath withObject:(id)object completion:(Void_Block)completion;


// colon-aligning makes the block indentation hard to read  
[UIView animateWithDuration:1.0  
                 animations:^{  
                     // something  
                 }  
                 completion:^(BOOL finished) {  
                     // something  
                 }]; 
```

###注释

＊ 当需要注释时，注释应该用来解释这段特殊代码为什么要这样做。
＊ 任何被使用的注释都必须保持最新,如果注释已失效请立刻被删除。
＊ 一般都避免使用块注释，因为代码尽可能做到自解释，只有当断断续续或几行代码时才需要注释。例外：这不应用在生成文档的注释

针对整个函数的注释，推荐使用XCode插件[VVDocumenter](https://github.com/onevcat/VVDocumenter-Xcode)








应该
```
```

不应该

```
```

应该
```
```

不应该

```
```












命名规则 
类名首字母大写，方法首字母小写，方法中的参数首字母小写，同时尽量让方法的命名读起来像一句话，能够传达出方法的意思，同时取值方法前不要加前缀“get”

变量名小写字母开头

常量以小写字母k开头，后续首字母大写

声明类或方法时，注意空格的使用，参数过多时可换行保持对齐，

调用方法时也是如此，参数都写在一行或换行冒号对齐，

关于注释
注释很重要，但除了开头的版权声明，尽可能把代码写的如同文档一样，让别人直接看代码就知道意思，写代码时别担心名字太长，相信Xcode的提示功能。

代码行最大字符数100

实例变量应该在实现文件.m中声明或以@property形式在.h文件中声明，一定要直接在.h文件声明，加上@priavte，另外，使用@private、@public，前面需要一个缩进空格。

尽可能保证 .h文件的简洁性，可以不公开的API就不要公开了，写在实现文件中即可。

写delegate的时候类型应该为weak弱引用，以避免循环引用，当delegate对象不存在后，我们写的delegate也就没有存在意义了自然是需要销毁的，weak与strong可以参考上一篇文章介绍。

建议使用“#pragma mark”，方便阅读代码



#参考
- [Apple Coding Guideline](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingBasics.html#//apple_ref/doc/uid/20001281-1002931-BBCFHEAB)
