

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

* 在方法之间应该有且只有一行，这样有利于在视觉上更清晰和更易于组织。
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

* 注释很重要，但除了开头的版权声明，尽可能把代码写的如同文档一样，让别人直接看代码就知道意思，写代码时别担心名字太长，相信Xcode的提示功能。
* 任何被使用的注释都必须保持最新,如果注释已失效请立刻被删除。

针对函数的注释，推荐使用XCode插件[VVDocumenter](https://github.com/onevcat/VVDocumenter-Xcode)

###命名

Apple命名规则尽可能坚持，长的，描述性的方法和变量命名是好的。

应该：
```
UIButton *settingsButton;
```

不应该：
```
UIButton *setBut;  
```

三个字符前缀应该经常用在类和常量命名，但在Core Data的实体名中应被忽略。
常量应该使用驼峰式命名规则，所有的单词首字母大写和加上与类名有关的前缀。

应该：

```
static NSTimeInterval const RWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;  
```

不应该：

```
static NSTimeInterval const fadetime = 1.7;  
```

属性也是使用驼峰式，但首单词的首字母小写。对属性使用auto-synthesis，而不是手动编写@synthesize语句，除非你有一个好的理由。

应该：

```
@property (strong, nonatomic) NSString *descriptiveVariableName;  
```

不应该：

```
id varnm;  
```

###下划线

当使用属性时，实例变量应该使用self.来访问和改变。这就意味着所有属性将会视觉效果不同，因为它们前面都有self.。

但有一个特例：在初始化方法里，实例变量(例如，_variableName)应该直接被使用来避免getters/setters潜在的副作用。

局部变量不应该包含下划线。


###方法

在方法签名中，应该在方法类型(-/+ 符号)之后有一个空格。在方法各个段之间应该也有一个空格(符合Apple的风格)。在参数之前应该包含一个具有描述性的关键字来描述参数。

"and"这个词的用法应该保留。它不应该用于多个参数来说明，就像initWithWidth:height以下这个例子：

应该：

```
- (void)setExampleText:(NSString *)text image:(UIImage *)image;  
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;  
- (id)viewWithTag:(NSInteger)tag;  
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;  
```

不应该：

```
-(void)setT:(NSString *)text i:(UIImage *)image;  
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;  
- (id)taggedView:(NSInteger)tag;  
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;  
- (instancetype)initWith:(int)width and:(int)height;  // Never do this. 
```

###变量

变量尽量以描述性的方式来命名。单个字符的变量命名应该尽量避免，除了在for()循环。

星号表示变量是指针。例如， NSString *text 既不是 NSString* text 也不是 NSString * text，除了一些特殊情况下常量。

私有变量应该尽可能代替实例变量的使用。尽管使用实例变量是一种有效的方式，但更偏向于使用属性来保持代码一致性。

通过使用'back'属性(_variable，变量名前面有下划线)直接访问实例变量应该尽量避免，除了在初始化方法(init, initWithCoder:, 等…)，dealloc 方法和自定义的setters和getters。

应该：

```
@interface RWTTutorial : NSObject  
@property (strong, nonatomic) NSString *tutorialName;  
@end  
```

不应该：

```
@interface RWTTutorial : NSObject {  
  NSString *tutorialName;  
}  
```

属性特性

所有属性特性应该显式地列出来，有助于新手阅读代码。属性特性的顺序应该是storage、atomicity，与在Interface Builder连接UI元素时自动生成代码一致。

应该：

[cpp] view plaincopy
@property (weak, nonatomic) IBOutlet UIView *containerView;  
@property (strong, nonatomic) NSString *tutorialName;  
不应该：

[cpp] view plaincopy
@property (nonatomic, weak) IBOutlet UIView *containerView;  
@property (nonatomic) NSString *tutorialName;  


NSString应该使用copy而不是strong的属性特性。

为什么？即使你声明一个NSString的属性，有人可能传入一个NSMutableString的实例，然后在你没有注意的情况下修改它。


###点符号语法

点语法是一种很方便封装访问方法调用的方式。当你使用点语法时，通过使用getter或setter方法，属性仍然被访问或修改。

点语法应该**总是**被用来访问和修改属性，因为它使代码更加简洁。[]符号更偏向于用在其他例子。

应该：

```
objc  
NSInteger arrayCount = [self.array count];  
view.backgroundColor = [UIColor orangeColor];  
[UIApplication sharedApplication].delegate;  
```

不应该：

```
NSInteger arrayCount = self.array.count;  
[view setBackgroundColor:[UIColor orangeColor]];  
UIApplication.sharedApplication.delegate;  
```


###字面值

NSString、NSDictionary、NSArray和NSNumber的字面值应该在创建这些类的不可变实例时被使用。请特别注意nil值不能传入NSArray和NSDictionary字面值，因为这样会导致crash。

应该：

```
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];  
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};  
NSNumber *shouldUseLiterals = @YES;  
NSNumber *buildingStreetNumber = @10018;  
```

不应该:

```
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];  
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];  
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];  
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];  
```

###常量

常量是容易重复被使用和无需通过查找和代替就能快速修改值。常量应该使用static来声明而不是使用#define，除非显式地使用宏。

应该：

```
static NSString * const kAboutViewControllerCompanyName = @"RayWenderlich.com";  
static CGFloat const kImageThumbnailHeight = 50.0;  
```

不应该：

```
#define CompanyName @"RayWenderlich.com"  
#define thumbnailHeight 2  
```

###枚举类型

当使用enum时，推荐使用新的固定基本类型规格，因为它有更强的类型检查和代码补全。现在SDK有一个宏NS_ENUM()来帮助和鼓励你使用固定的基本类型。

例如：

```
typedef NS_ENUM(NSInteger, RWTLeftMenuTopItemType) {  
  RWTLeftMenuTopItemMain,  
  RWTLeftMenuTopItemShows,  
  RWTLeftMenuTopItemSchedule  
};  

或

typedef NS_ENUM(NSInteger, RWTGlobalConstants) {  
  RWTPinSizeMin = 1,  
  RWTPinSizeMax = 5,  
  RWTPinCountMin = 100,  
  RWTPinCountMax = 500,  
}; 
```


不应该：

```
typedef enum {  
  GlobalConstantsPinSize = 5,  
  GlobalConstantsPinCount = 500,  
} GlobalConstants;  
```


###布尔值

Objective-C使用YES和NO。因为true和false应该只在CoreFoundation，C或C++代码使用。
既然nil解析成NO，所以没有必要在条件语句比较。不要拿某样东西直接与YES比较，因为YES被定义为1和一个BOOL能被设置为8位。

这是为了在不同文件保持一致性和在视觉上更加简洁而考虑。

应该：

```
if (someObject) {}  
if (![anotherObject boolValue]) {}  
```

不应该：

```
if (someObject == nil) {}  
if ([anotherObject boolValue] == NO) {}  
if (isAwesome == YES) {} // Never do this.  
if (isAwesome == true) {} // Never do this.  
```

如果BOOL属性的名字是一个形容词，属性就能忽略"is"前缀，但要指定get访问器的惯用名称。例如：

```
@property (assign, getter=isEditable) BOOL editable; 
```

###条件语句

条件语句主体为了防止出错应该使用大括号包围，即使条件语句主体能够不用大括号编写(如，只用一行代码)。这些错误包括添加第二行代码和期望它成为if语句；
还有，更危险的事情可能发生在if语句里面一行代码被注释了，然后下一行代码不知不觉地成为if语句的一部分。除此之外，这种风格与其他条件语句的风格保持一致，所以更加容易阅读。

应该：

```
if (!error) {  
  return success;  
}  
```

不应该：

```
if (!error)  
  return success;  
或

if (!error) return success;  
```

###三元操作符

当需要提高代码的清晰性和简洁性时，三元操作符?:才会使用。单个条件求值常常需要它。多个条件求值时，如果使用if语句或重构成实例变量时，代码会更加易读。一般来说，最好使用三元操作符是在根据条件来赋值的情况下。

Non-boolean的变量与某东西比较，加上括号()会提高可读性。如果被比较的变量是boolean类型，那么就不需要括号。

应该：

```
NSInteger value = 5;  
result = (value != 0) ? x : y;  
BOOL isHorizontal = YES;  
result = isHorizontal ? x : y;  
```

不应该：

```
result = a > b ? x = c > d ? c : d : y;  (X 嵌套)
```

###Init方法

Init方法应该遵循Apple生成代码模板的命名规则，返回类型应该使用instancetype而不是id。

```
- (instancetype)init {  
  self = [super init];  
  if (self) {  
    // ...  
  }  
  return self;  
}  
```

###类构造方法

当类构造方法被使用时，它应该返回类型是instancetype而不是id。这样确保编译器正确地推断结果类型。

```
@interface Airplane  
+ (instancetype)airplaneWithType:(RWTAirplaneType)type;  
@end  
```

###CGRect函数

当访问CGRect里的x, y, width, 或 height时，应该使用CGGeometry函数而不是直接通过结构体来访问。引用Apple的CGGeometry：

在这个参考文档中所有的函数，接受CGRect结构体作为输入，在计算它们结果时隐式地标准化这些rectangles。因此，你的应用程序应该避免直接访问和修改保存在CGRect数据结构中的数据。相反，使用这些函数来操纵rectangles和获取它们的特性。
应该：

```
CGRect frame = self.view.frame;  
CGFloat x = CGRectGetMinX(frame);  
CGFloat y = CGRectGetMinY(frame);  
CGFloat width = CGRectGetWidth(frame);  
CGFloat height = CGRectGetHeight(frame);  
CGRect frame = CGRectMake(0.0, 0.0, width, height);
```

不应该：

```
CGRect frame = self.view.frame;  
CGFloat x = frame.origin.x;  
CGFloat y = frame.origin.y;  
CGFloat width = frame.size.width;  
CGFloat height = frame.size.height;  
CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };  
```

###黄金路径

当使用条件语句编码时，左手边的代码应该是"golden" 或 "happy"路径。也就是不要嵌套if语句，多个返回语句也是OK。

应该：

```
- (void)someMethod {  
  if (![someOther boolValue]) {  
    return;  
  }  
  //Do something important  
}  
```

不应该：

```
- (void)someMethod {  
  if ([someOther boolValue]) {  
    //Do something important  
  }  
}  
```

###单例模式

单例对象应该使用线程安全模式来创建共享实例。

```
+ (instancetype)sharedInstance {  
  static id sharedInstance = nil;  
  static dispatch_once_t onceToken;  
  dispatch_once(&onceToken, ^{  
    sharedInstance = [[self alloc] init];  
  });  
  return sharedInstance;  
}  
```

这会防止possible and sometimes prolific crashes。

###换行符

换行符是一个很重要的主题，因为它的风格指南主要为了打印和网上的可读性。

例如：

```
self.productsRequest = [[SKProductsRequest alloc] initWithProductIdentifiers:productIdentifiers];  
```

一行很长的代码应该分成两行代码，下一行用两个空格隔开。

```
self.productsRequest = [[SKProductsRequest alloc]   
  initWithProductIdentifiers:productIdentifiers]; 
```

###Xcode工程

尽可能在target的Build Settings打开"Treat Warnings as Errors，和启用以下additional warnings。如果你需要忽略特殊的警告，使用Clang's pragma feature。




### 一句话规则
变量名小写字母开头
常量以小写字母k开头，后续首字母大写
声明类或方法时，注意空格的使用，参数过多时可换行保持对齐，
调用方法时也是如此，参数都写在一行或换行冒号对齐，
代码行最大字符数100
尽可能保证 .h文件的简洁性，可以不公开的API就不要公开了，写在实现文件中即可。
写delegate的时候类型应该为weak弱引用，以避免循环引用，当delegate对象不存在后，我们写的delegate也就没有存在意义了自然是需要销毁的


#参考
- [Apple Coding Guideline](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingBasics.html#//apple_ref/doc/uid/20001281-1002931-BBCFHEAB)
