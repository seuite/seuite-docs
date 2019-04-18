# 一分钟上手 Dart

## 特点
- 长得像 JavaScript
- 支持 AOT、JIT 编译
- 性能强大，不需要锁就能对象分配和垃圾回收，它被编译为本地代码，不需要建立语言间的桥梁(像 JavaScriptCore)
- 不需要单独的声明式布局语言
- 一切皆为对象
- Dart1 是弱数据类型，Dart2 是强类型语言
- 运行前解析，指定数据类型和编译时的常量，可以提高运行速度
- 有统一的入口 main
- 没有 public、protected、private 概念，私有特性通过上下划线表示
- 工具可以检查出警告信息和错误信息
- 支持 async / await


## Dart的常用库
- dart:async
- dart:collection
- dart:convert
- dart:core
- dart:html
- dart:io
- dart:math
- dart:svg
  
## 注释方法
```dart
// 单行注释

/*
多行注释
*/

/**
文档注释
*/

///文档注释
```

## 变量声明与数据类型
```dart
var name = "foo"; //变量
final username = "bar"; //只能被设定一次的常量，有点像Java里的final
const pi = 3.1415; //编译时常量
//以上声明变量只有一个类型，可以类型推断
dynamic myName; // myName变量没有类型
int lineCount; // 此时lineCount为null
```
变量类型：
- Number
  - int
  - double
- String
- Boolean
- List
- Map
  
```dart
var s1 = 'hi ';
var s2 = "flutter" //支持单引号和双引号
var s3 = '''
  多行文本
''';
var s4 = """;
  多行文本
"""; //类似于es6的```
const s = 'foo';
const ss = '${s}bar';
var sex = 'male';
if (sex) { } //错误，不支持像JavaScript里的真值判定
var list = [1, 2, 3];
print(list.length);
var map = {
  'Monday': '星期一'
}; //Map类似于JavaScript里的对象
print(map['Monday']);
print(map.length);
```

## 函数
```dart
bool equal(String str1, String str2) {
  return str1 == str2;
}

String getUserInfo(String name, [String form]) {
 //可选参数用[]
}
String getUserInfo(String name, [String form = 'China']) {} //参数默认值
```
所有函数都有返回值，如果没有指定返回值，则默认的返回值是null

## 运算符
```dart
//一些Dart里特殊的运算符 
5 ~/ 2 //整除
as //类型转换
is is! //类型判断
b??=value //b为空时将value赋给b
expr1 ?? expr2 // 如果expr1为空，则返回其值，否则计算并返回expr2的值 
querySelector('#btn')
  ..text = 'OK'
  ..onClick.listen( (e) => {}) // 级联操作
```

## 流程控制语句

同其他语言
- if else
- for
- while do-while
- break 
- continue
- switch case
- assert

## 异常
可以抛出异常或者任何非空对象
```dart
throw FormatException('An Exception');
throw '数据非法';捕获异常try {

} on OutOfLlamasException {
  // 特定的异常
} on Exception catch(e) {
  // 其它的Exception
} catch (e, s) { // e是异常 s是堆栈跟踪信息
  // 其它
} finally {
  // 最终都会执行的操作
}
```

## 对象
定义类和产生实例
```dart
class User {
  String name;
  int age;
  User(String name, int age) {
    this.name = name;
    this.age = age;
  }
  //或者简写成User(this.name, this.age)

  //命名的构造函数，从另一类现有数据中快速实现
  User.fromJson(Map json) {
    name = json['name'];
    age = json['age'];
  }
}
var user = new User();
```

Dart 里支持 get( )和set( )
```dart
class Rectangle {
  num left;
  num top;
  num width;
  num height;
  Rectangle(this.left, this.top, this.width, this.height);

  num get right => left + width;
  set right(num value) => left = value - width;
  
  num get bottom => top + height;
  set bottom(num value) => top = value - height;  
}
```
Dart 里支持运算符重载, 函数式编程（挖坑）

类的继承，Dart 里支持抽象类的定义
```dart
class Human extends Animal {
  void say() {
  }
}
abstract class DateBaseOperate {
  void insert();
  void delete();
  void update();
  void query(); 
}
```

Dart 支持枚举类型的声明
```dart
enum Color {
  red,
  green,
  blue
}
List<Color> colors = Color.values; // 获取枚举类中所有的值
Color aColor = Color.blue;
```

Dart 支持Mixins
```dart
class S {
  a() { print("S.a"); }
}
class A {
  a() { print("A.a"); }
  b() { print("A.b"); }
}
class T = A with S;
T t = new T();
t.a(); // S.a
t.b(); // A.b
```
Dart 也支持泛型

## 库的使用
```dart
//引用库
import 'dart:io';
import 'package:mylib/mylib.dart';
//指定一个库的前缀
import 'package:lib1/lib1.dart' as lib2;
lib2.Element element2 = new lib2.Element();
//引用库的一部分
import 'package:lib1/lib1.dart' show foo; //只引用foo函数
import 'package:lib2/lib2.dart' hide foo; //引用除了foo函数的其他内容
```

## 异步
Dart支持async / await
```dart
readFile( ) async {
  //返回异步对象
}
await readFile()
```

## 元数据
元数据就是 Java 里的注解，目前支持三个修饰符
- @deprecated 被弃用的
- @override 重写
- @proxy 代理

## 想知道更多？
- [Dart 中文网](http://dart.goodev.org/guides/get-started)
- [Dart 官方网站](https://www.dartlang.org/)