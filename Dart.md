# Dart Programming Language

## Dart简介
### 言语背景
Dart初期因为Google对Javascript的不满而创造的新轮子来代替Javascript的，只是作为浏览器脚本运行在浏览器上的，为了推广Dart，Google在自己的Chrome上内置了DartVM的引擎。但是在NodeJS开源项目的推动下，Javascript又焕发了生机，到了在编程界无缝不钻的境界。因此在Google有偷偷的移除掉DartVM，但是google又开始使用Dart在移动端解决跨平台开发，也开始在多端应用起来。在Dart2.0以前，Dart是一门弱类型语言，2018年8月份正式发布2.0之后成为一门强类型语言。
Dart作为一门应用层编程语言，具有自己的Dart VM，通常情况下运行在自己的虚拟机上，特定情况下也可以编译成Native Code 运行在硬件上。是一门面向对象编程语言，借鉴于SmallTalk，比Java简单、比Javascript规范，更加工程化。
### Dart 的特性
* 单进程异步事件模型；
* 强类型，可以类型推断；
* DartVM，具有极高的运行效率和优秀的代码运行优化，根据早前的基准测试，性能比肩 Java7 的JVM；
* 独特的隔离区( Isolate )，可以实现多线程；
* 面向对象编程，一切数据类型均派生自 Object ；
* 运算符重载，泛型支持；
* 强大的 Future 和 Stream 模型,可以简单实现高效的代码；
* Minix 特性，可以更好的实现方法复用；
* 全平台语言，可以很好的胜任移动和前后端的开发。
* 在语法上，Dart 提供了很多便捷的操作，可以明显减少代码量。比如字符连接，可以直接 "my name is $name, age is $age"，无需+号拼接，也无需做类型转换。

### 建议学习步骤
``` mermaid
 graph LR
 id>1基础语言语法] ==> id2>2代码编写风格]
 id2 ==> id3>3基础类库的使用]
 id3 ==>id4>4开始你的编程]
```

## 基础语法
### 程序入口
```dart
main() {
  // 变量及取值
  int number   = 42;
  String text  = "number 的数值为";

  // 控制台输出
  print("$text $number.");
}
```
### 运行模式
* 生产模式（Production mode）：Dart程序的默认运行模式，为速度而优化，可选静态类型声明会被忽略。
* 强制模式（Checked mode）：适合开发者使用的模式，可以检测出运行过程中的一些类型错误。
> 建议在强制模式下开发和调试，在生产模式下部署。

### 内置类型
Dart语言提供的内置类型有
1. 字符串
2. 数字
3. 布尔
4. 列表
5. 映射

#### 字符串
Dart中的字符串是一组Unicode字符代码的序列，可以使用单引号或双引号创建字符串。
```dart
    var s1 = '单引号可以很好地作为字符串常量。';
    var s2 = "双引号的效果也是一样的。";
    var s3 = '字符串分界符 \' 的转义很方便。';
    var s4 = "使用双引号作为分界符更方便，不用对 ' 进行转义。";
```
可以使用字符串表达式嵌入表单式 ${}，如果表达式为变量名称，可以省略{}
```dart
    var s = '内插字符串（string interpolation）';
    
    print('Dart 的 $s 很方便使用。');
    print('如果需要全部大写，${s.toUpperCase()} 非常方便!');
```
相邻的字符串常量可以连接为新的字符串
```dart
    var s = '字符串''连接'
            "甚至可以跨行进行";
    print(s); // 字符串连接甚至可以跨行进行
```
可以使用三个单引号或者双引号创建多行字符串。
```dart
    var s1 = '''
    您可以像这样
    创建多行字符串。
    ''';
    
    var s2 = """我也是
    多行字符串啊喂。""";
```
可以在字符串个开头使用 @ 创建纯字符串，赋值时不会被转义
```dart
    var s = @'在纯字符串中，连 \n 都会被忽略。';
```
使用 === 运算符检测两个字符串是否完全等价
```dart
    var name = 'NAME';
    var greeting = "Hello, $name!";
    var greetingTemplate = 'Hello, NAME!';
    
    print(greeting == greetingTemplate); // 输出 true；字符完全相同
```
字符串常用方法

```dart
    var fullName = 'Cuthbert Musgrave Girdlestone, III';
    
    fullName.startsWith('Cuthbert');            // true；以“Cuthbert”开头
    fullName.endsWith('III');                   // true；以“III”结尾
    fullName.contains(new RegExp('Musgrave'));  // true；匹配正则表达式“/Musgrave/”
```
通过程序生成字符串，可以使用StringBuilder的同String方法，在调用此方法之前是不会生成新的String对象的。
```dart
var sb = new StringBuffer();

sb.add("使用 StringBuffer");
sb.addAll([" 可", "高效", "创建", "字符串，"]);
sb.add("数量越多 ").add("效果越明显。");

var fullString = sb.toString();

print(fullString); // 使用 StringBuffer 可高效创建字符串，
                   // 数量越多 效果越明显。
sb.clear();        // 清空对象！
```
> 字符串对象只能创建不能改变，所有的String方法全部是创建新的String，并没有修改原来的String对象。另外，编译为 JavaScript 代码后 StringBuffer 执行很慢。

#### 数字
dart语言中的数字分为两种，int 和 double。十进制64位双精度浮点数，遵循 IEEE 754 规范所约定的格式 。int 和 double都是num的子接口。num定义了基本的运算符。
num接口中还有abs、ceil、floor等方法。如果子接口中没有提供相应的功能，则可以使用Math类的可能提供了的功能。
```dart
    var x = 1;
    var hex = 0xDEADBEEF;
    var bigInt = 3465346583465243765923847659234765928347659567398475647495873984572947593470294387093493456870849216348723763945678236420938467345762304958724596873045876234572037862934765294365243652548673456705673465273465246734506873456729457623845623456234650457693475603768922346728346256;
    //双精度浮点数
    var y = 1.1;
    var exponents = 1.42e5;
```
> **注：** dart中的整数的行为类似于数学整数。它们并不局限于某个可以用32位或64位表示的最大值,它们的大小的唯一限制是可用内存。但是有些dart实现可能并不总是符合这个要求。当dart被翻译成javascript时，javascript数字有时被用来表示整数，因为javascript本身不支持整数数据类型。因此，大于2^53的整数可能不容易得到。

字符串和数字类型之间进行相互转换
```dart
    // string -> int
    var one = Math.parseInt("1");                   // 1
    
    // string -> double
    var onePointOne = Math.parseDouble("1.1");      // 1.1
    
    // int -> string
    String oneAsString = 1.toString();              // "1"
    
    // double -> string
    String piAsString = 3.14159.toStringAsFixed(2); // "3.14"
```

#### 布尔
Dart有正式的布尔类型，名为 bool。 只有两种对象的类型为 bool： 布尔常量，true 和 false。当Dart 需要一个布尔值时，如果该值不是 true，那就肯定是 false。不像在JavaScript中 1 或非 null 对象作为 true 对待:
```dart
    var name = 'Bob';
    if (name) {
      print("你有名字耶！"); // 在 JavaScript 中可以输出，但 Dart 中不能
    }
    
    if (1) {
      print("JavaScript 会输出本行，因为它认为 1 等于 true。");
    } else {
      print("Dart 会输出本行，因为它认为 1 *不* 等于 true。");
    }
```

#### 列表
说白了就是数组，在Dart中，数组属于 List 类型的对象。 当您将Dart编译为JavaScript脚本时，Dart 列表会被编译为JavaScript数组。 
```dart
    var list = [1,2,3];
    print(list.length); // 元素数目：3
    print(list[1]);     // 第二项：2
```
常见操作
```dart
    var list = [1,2,3];
    list.add(4);
    var list = [1,2,3,4];
    list.removeRange(2, 1); // 移除第三个元素
```
列表的遍历
对列表的遍历可以使用for、for ... in 或 forEach()，如果需要当前的索引，使用for语句。
```dart
    var list = [1,2,3,4];
    for (var x = 0; x < list.length; x++) {
      print(list[x]);
    }
    
    for (final x in list) {
      print(x);
    }
    
    [1,2,3].forEach((element) => print(element));
```

列表与集合常用方法
forEach方法是List接口及其超接口Collection所定义的方法之一，还有其他如sort、filter、every、some。

#### 映射
映射说白了就是Map的键值对对象。类似与JSON对象。可以使用.length获取长度，remove移除指定键值对、使用Map.from()进行复制。

```dart
var user = {"name": '张三', "age": '24'};
print(user["name"]);
print(user.length);

var newUser = Map.from(user);
print(user["name"]);

```
遍历forEach
```dart
var user = {"name": '张三', "age": '24'};
user.forEach((k,v) => print('$k : $v'));
```
> 跟Java中一样，不要指望forEach按特定顺序进行键值对遍历。不过可以使用getKeys()和getValues()返回对应的键值数组，属于Collection对象。

### 运算符
Dart支持运算符。它不仅定义运算符，还允重新定义其中很多运算符。下表按优先级顺序 列出了Dart的全部运算符:
| 描述 |运算符|结结合性|
|--| --| :-: |
|一元后缀|表达式++ 表达式-- () [] .|左|
|一元前缀|-表达式 !表达式 ~表达式 ++表达式 --表达式|右|
|乘除|* / % ~/|左|
|加减| + - | 左 |
|移位| << >> | 左 |
|关系|is is! >= > <= <| 无|
|相等性| == != === !== | 无 |
|位 AND| & |左|
| 位 XOR | ^ | 左|
| 位 OR | \| | 左 |
| 逻辑 AND | && |左 |
| 逻辑 OR | \| \| | 左 |
| 三元运算符| 表达式 ? 表达式 : 表达式 | 无 |
| 赋值 | = *= /= ~/= %= += -= <<= >>= &= ^=  \|= | 右 |

### 函数
```dart
String say(String from, String msg) => "$from 说“$msg”";

print(say("Bob", "Hello")); // "Bob 说“Hello”"

//可选参数
String say(String from, String msg, [String device]) {
  var result = "$from 说“$msg”";
  if (device != null) {
    result = "$result（通过 $device 发送）";
  }
  return result;
}
```
* 可选参数
可以给可选参数指定默认值。默认值必须为编译时常量。如果没有提供默认值null，如果省去可选参数，则会使用默认值。
```dart

    String say(String from, String msg, [String device='信鸽']) {
      var result = "$from 说“$msg”";
      if (device != null) {
        result = "$result（通过 $device 发送）";
      }
      return result;
    }
    
    print(say("Bob", "你好呀", device: "易拉罐话筒"));
```
> **注：** 可选参数同时也是命名参数。可以将函数作为参数，传给其他函数、也可以赋值给变量。类似于Javascript中的函数。
所有函数都会返回一个值。如果未指定返回值，则将在函数主体的末端隐式调用return null;语句。

### 流程控制语句
跟其他语言类似，主要分为：
1. if ... else if... else ...
2. for循环
3. while 与 do while
4. break 与 continue
5. switch 与 case

### 异常处理
跟Java类似，Dart 代码可以抛出与捕捉异常。异常是预期以外情况发生的错误信号。如果没有捕捉，异常将不断返回至程序顶层。但不同的是Dart的所有异常都是非强制异常。方法不会声明可能抛出的异常，也不必捕捉所有异常，Dart程序可以将任意对象作为异常抛出。Dart提供了Exception接口以及很多定义的异常类型。当然也可以更具自己需求去扩展Exception。常用的有：
1. IndexOutOfRangeException 索引越界
2. NoSuchMethodException 无此方法
3. NullPointerException null 指针
4. IllegalArgumentException 参数非法
```dart
 throw new IllegalArgumentException('数值必须大于零');
 throw "这是个怪胎!";
 
    try {
      breedMoreLlamas();
    } catch (final OutOfLlamasException e) {
      buyMoreLlamas();
    }
    
    //多种处理
    try {
      breedMoreLlamas();
    } catch (final OutOfLlamasException e) {  // 特定异常
      buyMoreLlamas();
    } catch (final Exception e) {             // 任意异常
      print("Unknown exception: $e");
    } catch (final e) {                       // 类型不确定，全部处理
      print("Something really unknown: $e");
    }finally {
      cleanLlamaStalls();  // 总会执行，即使有异常抛出
    }
```

### 类阐述
对象由字段（状态）、方法（行为），对象的有可变性和不可变性状态；对象的方法集永远不能为空。对象行为来源于类，可以说对象是类的实例。类似与Java，Dart是一款面向对象的语言，支持类与单继承。 根类为Object。所有未初始化的实例变量都有默认值 null，其类型为Null类型。
```dart
    class Point {
      num x, y;
    }
```
> **注：** 不论实例变量是否为 final 变量，均隐式包含了 getter 方法。非 final 实例变量隐式包含了 setter 方法。

* 实例变量的初始化 与 构造函数
Dart将每个新分配的变量(不仅是实例变量，还有局部变量、类变量和顶级变量)初始化为null, 在Dart中，null是一个对象其类型为 Null类，这与c、c++、c#、java或javascript等语言中的情况不同，“一切都是对象”，貌似说的过去。
```dart
    class Point {
      num x = 0,
          y = 0;
    }
    
    class Point {
      num x, y;
      // this.x = x 与 this.y = y 的糖衣语法构造函数
      Point(this.x, this.y);
    }
    
    //命名构造函数
    class Point {
      num x, y;
    
      // 命名构造函数
      Point.fromJson(Map json) : x = json['x'], y = json['y'];
    
      Point(this.x, this.y);
    }
    
    var jsonData = JSON.parse('{"x":1, "y":2}');
    var point = new Point.fromJson(jsonData);
    
    //常量构造函数
    class Point {
      final num x, y;
      const Point(this.x, this.y);
      static final Point origin = const Point(0, 0);
    }
    
   void main() {
      var a = const Point(1, 1);
      var b = const Point(1, 1);
    
      print(a === b); // 输出 true，两个实例完全一样！
    }
```

> 如果您不声明构造函数，将会调用默认构造函数。默认构造函数没有参数，调用的是超类的无参构造函数。由于编译时常量是常量且固定， 构造两个一样的 const 对象 会生成完全一样的实例。  

要实现不总是创建类的新实例的构造函数， 可使用 factory 关键字。 例如，factory 构造函数 可能会返回缓存中的实例，或是可能返回子类的实例。 
下例演示了返回缓存中对象的 factory 构造函数：
```dart
class Logger {
  final String name;
  bool mute = false;

  static Map<String, Logger> _cache;

  factory Logger(String name) {
    if (_cache == null) {
      _cache = {};
    }

    if (_cache.containsKey(name)) {
      return _cache[name];
    } else {
      final logger = new Logger._internal(name);
      _cache[name] = logger;
      return logger;
    }
  }

  Logger._internal(this.name);

  log(String msg) {
    if (!mute) {
      print(msg);
    }
  }
}
//对其他构造函数， 如需调用 factory 构造函数，您可以使用 new 关键字：
var logger = new Logger('UI');
logger.log('按钮被点击了');
```
> **注：** factory 构造函数无权访问 this。 