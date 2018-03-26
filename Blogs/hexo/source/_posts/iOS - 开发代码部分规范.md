---
title: iOS - 开发代码部分规范
date: 2018-02-02 22:22:22
tags: [iOS, 代码规范]
categories: iOS
---


**1. 关于命名**

**1.1 统一要求**

- 含义清楚，尽量做到不需要注释也能了解其作用，若做不到，就加注释
- 使用全称，不适用缩写

**1.2 类的命名**

- 大驼峰式命名：每个单词的首字母都采用大写字母

| 例子：MFHomePageViewController |
| --- | --- |

- 后缀要求

**a.ViewController: 使用ViewController做后缀**

| 例子: MFHomeViewController |
| --- | --- |

**b.View: 使用View做后缀**

| 例子: MFAlertView |
| --- | --- |

**c.UITableCell:使用Cell做后缀**

| 例子: MFNewsCell |
| --- | --- |

**d.Protocol: 使用Delegate或者DataSource作为后缀**

| 例子: UITableViewDelegate |
| --- | --- |

**1.3 私有变量**

- 小驼峰式命名：第一个单词以小写字母开始，后面的单词的首字母全部大写

| 例子：firstName、lastName |
| --- | --- |

- 以 \_ 开头，第一个单词首字母小写

| 例子：NSString \* \_somePrivateVariable |
| --- | --- |

- 私有变量放在 .m 文件中声明

**1.4 property变量**

- 小驼峰式命名

| 例子：///注释  @property (nonatomic, copy) NSString \*userName; |
| --- | --- |

- 禁止使用synthesize关键词

**1.5 宏命名**

- 全部大写，单词间用 \_ 分隔。[不带参数]

| 例子: #define THIS\_IS\_AN\_MACRO @&quot;THIS\_IS\_AN\_MACRO&quot; |
| --- | --- |

- 以字母 k 开头，后面遵循大驼峰命名。[不带参数]

| 例子：#define kWidth self.frame.size.width |
| --- | --- |

- 小驼峰命名。[带参数]

| #define getImageUrl(url) [NSURL URLWithString:[NSString stringWithFormat:@&quot;%@%@&quot;,kBaseUrl,url]] |
| --- | --- |

**1.6 Enum**

- Enum类型的命名与类的命名规则一致
- Enum中枚举内容的命名需要以该Enum类型名称开头

例子:  typedef NS\_ENUM(NSInteger, AFNetworkReachabilityStatus) {      
    AFNetworkReachabilityStatusUnknown = -1,      
    AFNetworkReachabilityStatusNotReachable = 0,      
    AFNetworkReachabilityStatusReachableViaWWAN = 1,      
    AFNetworkReachabilityStatusReachableViaWiFi = 2  
    }; 

**1.7 Delegate命名**

- 类的实例必须为回调方法的参数之一

| 例子:-(NSInteger)tableView:(UITableView\*)tableView numberOfRowsInSection:(NSInteger)section |
| --- | --- |

- 回调方法的参数只有类自己的情况，方法名要符合实际含义

| 例子:  -(NSInteger)numberOfSectionsInTableView:(UITableView\*)tableView |
| --- | --- |

- 以类的名字开头(回调方法存在两个以上参数的情况)以表明此方法是属于哪个类的

| 例子:-(UITableViewCell\*)tableView:(UITableView\*)tableView cellForRowAtIndexPath:(NSIndexPath \*)indexPath |
| --- | --- |

- 使用did和will通知Delegate已经发生的变化或将要发生的变化,

例子:  
a.-(NSIndexPath\*)tableView:(UITableView\*)tableView willSelectRowAtIndexPath:(NSIndexPath\*)indexPath;     
b.-(void)tableView:(UITableView\*)tableView didSelectRowAtIndexPath:(NSIndexPath\*)indexPath; 


**2. 私有方法及变量声明**

**2.1 声明位置**

- 在.m文件中最上方，定义空的category进行声明

例子:  
#import &quot;CodeStandardViewController.h&quot;  
// 在这个category（类目）中定义变量和方法  
@interface CodeStandardViewController (){ // 声明私有变量  }     
// 私有方法  
- (void)samplePrivateMethod;  
@end     
@implementation CodeStandardViewController     
// 私有方法的实现  
- (void)samplePrivateMethod  { //some code  } 


**3.关于注释**

最好的代码是不需要注释的 尽量通过合理的命名

良好的代码把含义表达清楚 在必要的地方添加注释

注释需要与代码同步更新

如果做不到命名尽量的见名知意的话，就可以适当的添加一些注释或者mark

**3.1 属性注释**

| 例子：/// 学生@property (nonatomic, strong) Student \*student; |
| --- | --- |

**3.2 方法声明注释**

/\*\* \* @brief 登录验证\*\* 
@param personId 用户名\* 
@param password 密码\* 
@param complete 执行完毕的block\*\* 
@return\*/+ (void)loginWithPersonId:(NSString \*)personId password:(NSString \*)password complete:(void (^)(CheckLogon \*result))complete; 


**4.关于UI布局**

使用Interface Builder进行界面布局

Xib文件的命名与其对应的.h文件保持相同

Xib文件中控件的组织结构要合理，Xib文件中控件需要有合理的可读性强的命名，方便他人理解

**5.格式化代码**

**5.1 指针 &quot;\*&quot; 位置**

- 定义一个对象时，指针 &quot;\*&quot; 靠近变量

| 例子: NSString \*userName; |
| --- | --- |

**5.2 方法的声明和定义**

- 在- 、+和返回值之间留一个空格，方法名和第一个参数之间不留空格

| - (id)initWithNibName:(NSString \*)nibNameOrNilbundle:(NSBundle \*)nibBundleOrNil{...} |
| --- | --- |

**5.3 代码缩进**

- 使用 xcode 默认缩进，即 tab = 4空格
- 使用 xcode 中 re-indent 功能定期对代码格式进行整理
- 相同类型变量声明需要独行声明

| 例子:  CGFloatoringX = frame.origin.x;  CGFloatoringY = frame.origin.y;  CGFloatlineWidth = frame.size.width; |
| --- | --- |

- Method与Method之间空一行

例子:  #pragma mark - private methods  
- (void)samplePrivateMethod  {...}     
- (void)sampleForIf  {...} 


**5.4 对method进行分组**

- 使用 #pragma mark - 方式对类的方法进行分组

例子:  
#pragma mark - private methods  
- (void)samplePrivateMethod  {...}     
- (void)sampleForIf  {...}     
- (void)sampleForWhile  {...}     
- (void)sampleForSwitch  {...}     
- (void)wrongExamples  {...}     
#pragma mark - public methods  
- (void)samplePublicMethodWithParam:(NSString\*)sampleParam  {...}     
#pragma mark - life cycle methods  
- (id)initWithNibName:(NSString \*)nibNameOrNil bundle:(NSBundle \*)nibBundleOrNil  {...}     
- (void)viewDidLoad  {...}     
- (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)interfaceOrientation  {...} 


**5.5 大括号写法**

- 对于类的method: 左括号另起一行写(遵循苹果官方文档)

- (id)initWithNibName:(NSString \*)nibNameOrNilbundle:(NSBundle \*)nibBundleOrNil  {      
    self = [super initWithNibName:nibNameOrNil      bundle:nibBundleOrNil];      
    if (self) {   // Custom initialization      }             
    return self;  
    } 



- 对于其他使用场景: 左括号跟在第一行后边

例子：  - (void)sampleForIf  {      
    BOOL someCondition = YES;      
    if(someCondition) {          // do something here      }  }     
    - (void)sampleForWhile  {      
        int i = 0;      
        while (i &lt; 10) {          
            // do something here          i = i + 1;      }  }     
            - (void)sampleForSwitch  {      
                SampleEnum testEnum = SampleEnumTwo;      
                switch(testEnum) {      
                    caseSampleEnumUndefined:{          // do something          break;      }      
                    caseSampleEnumOne:{          // do something          break;      }      
                    caseSampleEnumTwo:{          // do something          break;      }      
                    default:{          NSLog(@&quot;WARNING: there is an enum type not handled properly!&quot;);          
                    break;     
                     }  } 


 任何需要写大括号的部分，不得省略

  错误示例:   - (void)wrongExamples   {      
    BOOLsomeCondition = YES;      
    if (someCondition)      
    NSLog(@&quot;this is wrong!!!&quot;);      
    while(someCondition)      
    NSLog(@&quot;this is wrong!!!&quot;);   
    } 
