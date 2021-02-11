# 垃圾代码书写准则-Java

这是基于垃圾代码准则的([state-of-the-art-shitcode](https://github.com/trekhleb/state-of-the-art-shitcode))Java 垃圾代码准则

![qkmango 芒果小洛](README/logo_color.png)

![作者](https://img.shields.io/badge/Author-qkmango-28a9f7.svg)
![Gitee](https://img.shields.io/badge/Gitee-qkmango-c71d23.svg)
![版本](https://img.shields.io/badge/Version-v1.0-28a9f7.svg)
![垃圾代码徽章](https://img.shields.io/badge/State%20of%20the%20art-Shitcode-7B5804.svg)

↑↑↑ 这是一个你的项目应该遵循的垃圾代码书写准则的列表，遵循此准则的称为垃圾代码

## 徽章

如果您的存储库遵循最新的shitcode原则，你应当使用此徽章来表示这个项目是一个遵循了垃圾代码的项目，使用以下标志：

[![垃圾代码徽章](https://img.shields.io/badge/State%20of%20the%20art-Shitcode-7B5804.svg)](https://gitee.com/qkmango/state-of-the-art-shitcode-java)

徽章的Markdown源代码：

```md
![垃圾代码徽章](https://img.shields.io/badge/State%20of%20the%20art-Shitcode-7B5804.svg)
```



## 准则

### 💩 变量名不要见名知意

当我们输入的代码越少，那么我们就有越多的时间去思考代码的逻辑性等一些问题

*Good 👍🏻*

```
int a = 42;
```

*Bad 👎🏻*

```
int age = 42;
```



### 💩 类名/变量/函数 混合命名风格

为不同庆祝一下。

_Good 👍🏻_

```java
int wWidth = 640;
int w_height = 480;
int WLength = 200;
```

_Bad 👎🏻_

```java
int windowWidth = 640;
int windowHeight = 480;
int wLength = 200;
```



### 💩 不要写注释

反正没人会读你的代码，而且写注释很费时间。

_Good 👍🏻_

```java
String path = request.getServletPath();
if (session != null ||
    "/login.jsp".equals(path)||
    "/settings/user/login.do".equals(path)) {
    chain.doFilter(req,resp);
}
```

_Bad 👎🏻_

```javascript
/*如果session ！= null
  或 访问的路径是 登录页/登陆请求
  则放行*/
String path = request.getServletPath();
if (session != null ||
    "/login.jsp".equals(path)||
    "/settings/user/login.do".equals(path)) {
    chain.doFilter(req,resp);
}
```



### 💩 使用非母语写注释

如果您违反了“不写注释”原则，那么至少尝试用一种不同于您用来编写代码的语言来编写注释，这样显得更加高大上。

_Good 👍🏻_

```javascript
//リリースリクエスト
chain.doFilter(req,resp);
```

_Bad 👎🏻_

```javascript
//将请求放行
chain.doFilter(req,resp);
```



### 💩 已经确定数据类型的集合不要指定泛型类型

这样这个集合可以放入更多类型的数据，岂不美哉

_Good 👍🏻_

```javascript
ArrayList a = new ArrayList<>();
ArrayList n = new ArrayList<>();
```

_Bad 👎🏻_

```javascript
ArrayList<Integer> ageList = new ArrayList<>();
ArrayList<String> nameList = new ArrayList<>();
```



### 💩 尽可能把代码写成一行

_Good 👍🏻_

```java
byte[] textBytes = request.getParameter("user").getRemark().replace("\n","<br>").toLowerCase().getBytes();
```

_Bad 👎🏻_

```java
String user = request.getParameter("user");
String remark = user.getRemark();
remark = remark.replace("\n", "<br>");
remark = remark.toLowerCase();
byte[] textBytes = remark.getBytes();
```



### 💩 不要处理错误

无论何时发现错误，都没有必要让任何人知道它。没有日志，没有控制台错误消息。

_Good 👍🏻_

```javascript
try {
    //意料之外的情况
} catch (Exception e) {
    //什么都不要做... 🤫
}
```

_Bad 👎🏻_

```javascript
try {
    //意料之外的情况
} catch (Exception e) {
    e.printStackTrace();
}
```



### 💩 广泛使用全局变量

全球化的原则。

_Good 👍🏻_

```javascript
static int x = 5;

public static int square() {
    return x *= x;
}

public static void main(String[] args) {
    square();   //现在是25
}
```

_Bad 👎🏻_

```java
public static int square(int x) {
    return x *= x;
}

public static void main(String[] args) {
    square();   //现在是25
}
```



### 💩 创建你不使用的变量

以防万一，我们并不知道什么时候会需要使用这些多余的变量

_Good 👍🏻_

```java
int sum(int x, int y, int z) {
    int result = x + y;
    return x + y;
}
```

_Bad 👎🏻_

```java
int sum(int x, int y) {
    return x + y;
}
```



### 💩 不要执行类型检查

_Good 👍🏻_

```javascript
Student stu = (Student)object;
int id = stu.getId();	//如果object不是Student类型，那么强转就会抛异常
```

_Bad 👎🏻_

```java
if (object instanceof Student) {
    Student stu = (Student)object;
    int id = stu.getId();
}
```



### 💩 你应该有不能到达的代码

不能到达的代码，我们称为计划，这是你的 "Plan B".

_Good 👍🏻_

```javascript
if (true) {
    return "{success:true}";
} 
return "{success:false}";	//这是不可达代码，也就是Plan B
```

_Bad 👎🏻_

```javascript
return "{success:true}";
```



### 💩 三角法则

一个条件一个坑，何必将多个条件放在一起呢

_Good 👍🏻_

```javascript
if (object != null) {
    if (object instanceof Student) {
        Student stu = (Student) object;
        if (stu.getAge() < 18) {
            if (stu.getId() < 1001) {
                if (stu.getClassRoom().getRoomId() < 502) {
					//do some
                }
            }
        }
    }
}
```

_Bad 👎🏻_

```javascript
if (object == null || !(object instanceof Student)) {
    return;
}
Student stu = (Student) object;
if (stu.getAge() >= 18 &&
    stu.getId() >= 1001 &&
    stu.getClassRoom().getRoomId() >= 502) {
    return;
}
//do some
```



### 💩 混合缩进

避免缩进，因为它们会使复杂的代码在编辑器中占用更多的空间。如果你不喜欢回避他们，那就和他们捣乱。

_Good 👍🏻_

```java
String[] fruits = {"apple",
                   "orange", "grape",
                   "pineapple"};
String[] toppings = {"syrup", "cream",
                     "jam", "chocolate"};
ArrayList<String> desserts = new ArrayList<>();

for (String fruit : fruits) {
    for (String topping : toppings) 
    {
        desserts.add(
            fruit + topping);
    }
}
```

_Bad 👎🏻_

```java
String[] fruits = {"apple", "orange", "grape", "pineapple"};
String[] toppings = {"syrup", "cream", "jam", "chocolate"};
ArrayList<String> desserts = new ArrayList<>();

for (String fruit : fruits) {
    for (String topping : toppings) {
        desserts.add(fruit + topping);
    }
}
```



### 💩 字符串比较时变量在前

前后都是字符串，为什么要特别关心哪个在前呢？

_Good 👍🏻_

```java
if (name.equals("qkmango")) {
	//do some
}
```

_Bad 👎🏻_

```java
if ("qkmango".equals(name)) {
    //do some
}
```



### 💩 方法体长的比短的好

不要将一个方法写的具有可读性，不要将一个事情模块化，尽量将一个方法内写如更多的代码，即使这个方法实现了很多功能，让它具有高度耦合

- 你尽管将一个需求尽量写到一个方法里面，不要将需求拆分为多个模块，使用多个方法来完成
- 你可以重复去造轮子，虽然你造的轮子可能并不如原版，例如你可以自己去完成一个集合功能的实现，或者是像Mybatis这样的框架



### 💩 不要测试你的代码

这是重复且不需要的工作，所以你应该不去使用 junit 单元测试



### 💩 避免代码风格统一

在多人团队开发的过程中，不要将你的代码风格统一，尽量经常更换你的代码风格



### 💩 构建新项目不需要 README 文档

一开始我们就应该保持，就如同注释一样，可能并没有人去读。



### 💩 保存不必要的代码

不要删除不用的代码，最多注释掉，这些不用废弃的代码可能在后来还会使用，即使有一大片的代码都不用了，也不要去删除。