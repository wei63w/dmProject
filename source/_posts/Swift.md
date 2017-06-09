---
title: Swift入门
date: 2016-11-05 17:53:14
categories: 
	- IOS
tags: 
	- Swift
    
---

### 变量,常量
```
//再日常开发中,应当首选 let ,再必须修改的时候再使用var

//变量 : var       ---   var x = 20   //var 设置数值之后 可以修改
//常量 : let      --- let l =     20       //let 设置数值之后不可修改
//Swift  是一个语法严格的语言 任何情况下不会做隐式转换
//两个变量进行计算必须是相同类型
//判断该变量是神马类型 option + click 查看
let a = 2
let b = 2.5
let sum = a + b     //错误
//必须进行显示转换类型
let sum1 = Double(a)  +  b
let sum2 = a  + Int(b)
//也可以声明时 指定变量类型
let i : Double = 10
```

### Optional  可选的  ,可以有值  可以为nil
```
//init? 说明可能无法实例化 url
let url = NSURL(string: "http://www.baidu.com/")
// !  强行解包  程序员认为这里url一定有值
//let request = NSURLRequest(URL: url!)
//安全的写法
if(url != nil){
    let request = NSURLRequest(URL: url!)
}
```

###  分支控制
```
// 1. 没有()  好像也可以加()
// 2. 必须有{}
// 3. 没有非0即真 swift只有true false
let num = 20
if num > 10{
    print("大于10")
}
//三元  与oc一致
let a = 10
let b = 20
let c = a > b ? 100 : 200
// if let 判断并且设置数值
let aa = "ss"

if let maa:String = aa {
    print(maa)
}

var oName:String? = "张三"
var oAge:Int? = 18
//多值之间使用,号分隔
if let name:String = oName,age:Int = oAge{
    print(name + String(age))
}
//操作符 ??
//如果 oName为nil  使用?? 后面的字符串 否则使用oName 的结果
let cName:(String) = oName ?? "abc"
let xName:(String) = "abc" == cName ? cName :"ccc"

// ?? 常见的场景  表格要返回数据数量
var datalist :[String]?
datalist = ["xxx","aaa"]
//datalist? 表示datalist可以为空可能为nil
//如果为nil, .count不会报错 仍然返回nil
// ?? 如果datalist 为nil 了 就会返回 后面的 0
let count = datalist?.count ?? 0
//强行解包
//表示程序员承诺 datalist 一定有值 ,当为nil的时候就崩
let count1 = datalist!.count
```

###  Switch
```
//oc 1. switch的表达式 必须是证书
//2.再case中定义的变量 需要使用大括号抱起来才不会所有的case公用
//3.如果case中没有写操作 那么两个case会共同调用一个结果操作

//swift 中 
//1.表达式可以是任何类型 2.作用于仅再case内部 
//3.不需要break 4.每个case都需要有代码结果操作
let name = "aa"
switch name{
    case "aa":
        let age = 80
        print("aa \(age)")
    case "bb","cc":
        print("bb")
default:
    print("other")
}
```
### 字符串拼接
```
//String: 结构体 ,效率比对象高 一般推荐使用String  ,结构体 支持遍历
//NSString:  集成NSObject 不支持遍历
var strr:String = "你好美女"

for c in strr.characters{
    print(c)
}
//字符串拼接
let name = "老王"
let age = 19
let title = "xxx"
print(name + String(age) + title)
//直接用\(变量) 放在引号内会自动转换
print("\(name)\(age)\(title)")
//拼接字符串 陷阱  ?    当为可控类型时需要用双引号判断
let namee:String? = "张三"
print(namee ?? "" + String(age))
//可选项时 输出会加上Option 缺点
print("\(namee)")
//需要格式
let h = 9
let m = 5
let s = 3
let timeStr = "\(h):\(m):\(s)"

//参数以数组的方式输入
let timeStr1 = String(format: "%02d:%02d:%02d", arguments: [h,m,s])
//再swift中如果碰到 range,由于range 变化非常大 最好把string 改成NSString
let sstr = "abcdefg"
(sstr as NSString ).substringWithRange(NSMakeRange(2, 3))
//如果简单取值  endIndex表示前面字符串的长度
sstr.substringFromIndex("c".endIndex)
```

### for 循环
```
for var i = 0 ; i < 10 ; i++ {
    print(i)
}
//swift for
//  0..<10  从0到9
for i in 0..<10{
    print(i)
}
// 0...10 从0 到10
for i in 0...10{
    print(i)
}
// Range<Int> 泛型
let range = 0...10
```

### 数组的操作
```
let array = ["a","b","c"]
//可以放任何数组 不需要包装
let array2 = ["a",2,UIView()]

//遍历数组
for tem in array{
    print(tem)
}
//追加数组
var list = ["a","b","c"]
//追加
list.append("d")
//删除元素
list.removeLast()
list.removeFirst()
list.removeAtIndex(1)
//如果提前删完 再用all删会报错
//list.removeAll()
list.removeAll(keepCapacity: true)
//数组容量
print(list.capacity)
//1.定义数组 实例化一个只能保存字符串的数组
var list2 = [String()]
//2.追加元素 跟踪容量变化
//如果数组容量不够 会在当前的基础上 * 2
for i in 0..<16{
    list2.append("hello\(i)")
    print("索引\(i),数组容量为:\(list2.capacity)")
}
var list3 = [Int]()
//指定数组类型 并没有创建数组对象  :号指定类型
print(list3.capacity)
var list4: [Int]
//创建数组对象  =号赋值
list4 = [Int]()
//定义数组 指定容量
//count:指定数组长度 repeatedValue:指定数组默认存放内容
var array3 = [Int](count: 10, repeatedValue: 0)
//数组拼接  拼接的数组类型必须一致
var a1 = [1,2,3,4]
var a2 = [5,6,7,8]
var a3 = a1 + a2
```

###  字典操作
```
//key 通常为字符串   value 可以是任意类型
var dict = ["name":"zhangsan","age":18]
dict["age"] = 11
//如果key不存在会新建
dict["height"] = 22
print("\(dict)")
//遍历 k,v 随便写,要求前面是键 后面是值
for (k,v) in dict{
    print("key:\(k),value:\(v)")
}
//合并
var dict2 = ["a":"a","b":"b"]
let dict3 = ["aa":"aa","bb":"bb"]
for(k,v) in dict3{
    //依次设置dict2的内容
    dict2[k] = v
}
dict2
```
### 函数的定义
```
/格式 func 函数名(形参:形参类型,形参:形参类型) -> 返回类型{ //代码实现}
func sum(x:Int, y:Int) -> Int{
    return x + y
}
//调用函数格式 函数名(值1,参数名:值2)
sum(4, y: 5)

//外部参数
//num1 , num2 供外部调用的程序员参考,能够保证函数的语义更加清晰
//内部参数 x,y 供函数内部使用
func sum1(num1 x:Int,num2 y:Int) ->Int{
    return x + y
}
sum1(num1: 3, num2: 3)

//返回值  '->' 
//没有返回值  有三种写法
//1.直接省略
func demo(){
    print("abc")
}
demo()
//2.  -> Void
func demo2 () -> Void{
    print("abc")
}
demo2()
//3. -> ()
func demo3 () -> (){
    print("abc")
}
demo3()
//OC 的Block  是一组预先准备好的代码 1.可以当做参数传递 2.可以再需要的时候执行
//类似匿名函数
//闭包  可以暂时理解OC的block
//定义
func summ(num1 x:Int,num2 y:Int) -> (Int){
    return x + y
}
summ(num1: 2, num2: 2)
//Swift 中 ,变量可以直接记录函数
//summFunc 指向了summ ,summFunc 常量 记录了一个函数
//使用外部参数 可以有提示
let summFunc = summ
summFunc(num1: 3, num2: 2)
//闭包定义
//1.形参,返回值,代码 都包含在{}中
let demoFunc = {
    print("hello")
}

//执行闭包
demoFunc()
//闭包格式: {(带外部参数的形参列表)-> 返回类型 in  代码实现}
//用 in 来区分函数的定义和需要执行的代码
let demoFunc2 = { (num1 x:Int,num2 y:Int) -> Int in
    return x + y
}
demoFunc2(num1: 10, num2: 20)

//尾随闭包
//1.闭包是最后一个函数 2.函数的()可以提前关闭 3.最后一个参数直接使用(就是可以直接代码实现)
//4.例如下面这个  再GCD中
dispatch_async(dispatch_get_global_queue(0, 0)) { () ->Void in
    print("abc")
}
//带参数的闭包回调
func loaddata (finished:(msg:String) -> ()) {
    dispatch_async(dispatch_get_global_queue(0, 0)) { () -> Void in
        //异步耗时操作
        print("加载中")
        //如果使用同步 主线程回调
        dispatch_sync(dispatch_get_main_queue(), { () ->Void in
            //通过闭包回调结果 ,执行完成回调函数
            print("主线程回调")
            finished(msg: "我传值了")
        })
    }
}
loaddata { (msg) -> () in
    print(msg)
}
```
### 闭包返回值练习
```
    override func viewDidLoad() {
        super.viewDidLoad()
        
    let rect = CGRect(x: 0, y: 20, width:view.bounds.width, height: 44)
    let sv = scrollView(rect, numberOfLabel: { () -> Intin
        return 16
        }) { (index) -> (UILabel) in
            //根据index 创建label并且返回
            let label = UILabel()
            label.text = "hello\(index)"
            label.font = UIFont.systemFontOfSize(18)
            label.sizeToFit()
            label.font = UIFont.systemFontOfSize(14)
            return label
        }
     view.addSubview(sv)
    }
    //标签的行数,内容 都由闭包实现
    //闭包返回值:用来接收闭包返回结果  继续后续代码
    //闭包参数:用来将内容传递给闭包内部执行
    func scrollView(frame:CGRect,numberOfLabel:()->Int,labelOfIndex:(index:Int)->(UILabel)) -> (UIScrollView){
        //1.实例化scrollView 并制定大小
        let sv = UIScrollView(frame: frame)
        sv.backgroundColor = UIColor.lightGrayColor()
        
        //2.知道标签的数量,执行闭包,得到数量
        let count = numberOfLabel()
        print("标签数量\(count)")
        //3.遍历count知道标签内容 添加到scrollView
        let margin:CGFloat = 8
        var x = margin
        for i in 0..<count{
            let label = labelOfIndex(index: i)
            //设置label的frame位置
            label.frame = CGRect(x: x, y: 0, width: label.bounds.width, height: frame.height)
            //添加
            sv.addSubview(label)
            //递增
            x += label.bounds.width
        }
        //4.返回sv
        sv.contentSize = CGSize(width: x + margin, height: frame.height)
        return sv
    }
    ```
    
### 自定义视图Swift介绍
```
//当前类 是为了纯代码类准备
class LabelScrollView: UIScrollView {

    //再Swift中 函数支持重载,函数名称一样 参数的数量和类型不同
    //OC中叫InitWithFrame 使用纯代码开发的时候会被调用
    init(frame: CGRect,numberOfLabel:()->Int,labelOfIndex:(index:Int)->(UILabel)){
        
        super.init(frame: frame)
    }
    //再视图控制器中 UIViewController 有一个函数 InitWithCoder ,使用sb,xib开发的时候会被调用
    //再自定义视图中 必须要实现
    required init?(coder aDecoder: NSCoder) {
        //fatalError 函数 会让sb开发直接崩掉,可以区分强行使用纯代码
        fatalError("init(coder:) has not been implemented")
    }

}
```

### 封装ScrollView
```
        
    let rect = CGRect(x: 0, y: 20, width:view.bounds.width, height: 44)
        
        let sv = LabelScrollView(frame: rect, numberOfLabel: { () -> Int in
        return 16
        }) { (index) -> (UILabel) in
            //根据index 创建label并且返回
            let label = UILabel()
            label.text = "hello\(index)"
            label.font = UIFont.systemFontOfSize(18)
            label.sizeToFit()
            label.font = UIFont.systemFontOfSize(14)
            return label
        }
     view.addSubview(sv)
    }

//LabelScrollView 类
class LabelScrollView: UIScrollView {

    //再Swift中 函数支持重载,函数名称一样 参数的数量和类型不同
    //OC中叫InitWithFrame 使用纯代码开发的时候会被调用
    init(frame: CGRect,numberOfLabel:()->Int,labelOfIndex:(index:Int)->(UILabel)){
        
        super.init(frame: frame)
        
        //1.实例化scrollView 并制定大小
        backgroundColor = UIColor.lightGrayColor()
        
        //2.知道标签的数量,执行闭包,得到数量
        let count = numberOfLabel()
        print("标签数量\(count)")
        //3.遍历count知道标签内容 添加到scrollView
        let margin:CGFloat = 8
        var x = margin
        for i in 0..<count{
            let label = labelOfIndex(index: i)
            //设置label的frame位置
            label.frame = CGRect(x: x, y: 0, width: label.bounds.width, height: frame.height)
            //添加
            addSubview(label)
            //递增
            x += label.bounds.width
        }
        //4.返回sv
        contentSize = CGSize(width: x + margin, height: frame.height)
        //再Swift中构造函数 不需要返回值
    }
    //再视图控制器中 UIViewController 有一个函数 InitWithCoder ,使用sb,xib开发的时候会被调用
    //再自定义视图中 必须要实现
    required init?(coder aDecoder: NSCoder) {
        //fatalError 函数 会让sb开发直接崩掉,可以区分强行使用纯代码
        fatalError("init(coder:) has not been implemented")
    }

}
```
### 网络访问
```
        NSURLSession.sharedSession().dataTaskWithURL(NSURL(string: "http://localhost/demo.json")!) { (data, _, _) -> Voidin
            //将二进制数据转换成json
            let result = try!NSJSONSerialization.JSONObjectWithData(data!, options: [])
            print(result)
            
        }.resume()

```