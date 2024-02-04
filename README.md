# 后端代码规范（TODO）

## 使用CheckStyle插件进行检测

### 在IDEA中安装插件

https://plugins.jetbrains.com/plugin/1065-checkstyle-idea

[IDEA check-style插件]: https://plugins.jetbrains.com/plugin/1065-checkstyle-idea	"IDEA check-style插件"

### 在Maven中使用checkStyle插件

```xml
<build>
<plugins>
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-checkstyle-plugin</artifactId>
        <version>3.3.1</version>
        <configuration>
            <configLocation>https://raw.githubusercontent.com/WeUsuallyEatBeafOnFriday/check-style/master/checkstyle.xml</configLocation>
            <consoleOutput>true</consoleOutput>
            <failsOnError>true</failsOnError>
            <linkXRef>false</linkXRef>
        </configuration>
        <executions>
            <execution>
                <id>validate</id>
                <phase>validate</phase>
                <goals>
                    <goal>check</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
</plugins>
</build>
```

## 具体规范

### 不用的代码段直接删除,不要注释掉

### 变量名字长度不能超过64个字符

### 类注释规范

```java
/**
 * BoilingWater
 *
 * @author Benana
 * @since 2024-01-30
 */
public class BoilingWater {
	// doSomething
}
```

### 使用空格进行缩进，每次缩进4个空格: 不允许用Tab

在编译器中配置tab为4个空格即可

### 布尔变量名或方法以is开头

> 正确示范

```Java
private boolean isEmpty;
private Boolean isEmpty;
```

### 单行注释符与注释内容间以空格分割

> 正确示范

```Java
public void boilingWater(){// 我是滚水科技方法
    // 我是滚水科技方法
}
```

> 错误示范

```java
public void boilingWater(){//我是滚水科技方法
    //我是滚水科技方法
}
```

### 行末或空行不能有多余空格

> 错误示范

```Java
public void boilingWater(){ // 我是滚水科技方法 “空格”
}
```

### 不能使用浮点数做循环变量

> 错误示范

```Java
double size = 10;
for (double i = 0; i < size; i++) {
    
}
```

### 谨慎使用可变数量参数的方法

> 错误示范

```Java
public void doSomething(int... numbers) {
    for (int number : numbers) {
        // doSomething
    }
}
```

### 避免枚举常量序号的产生依赖于ordinal()方法

```Java
public enum MyEnum {
    APP(1);

    private final int serial;

    MyEnum(int serial) {
        this.serial = serial;
    }

    public int getSerial() {
        return serial;
    }

}
```

> 错误示范

```Java
int serial = MyEnum.APP.ordinal();
```

> 正确示范

```Java
int serial = MyEnum.APP.getSerial();
```



### 莫名其妙的判断

> 错误示范

```Java
boolean flag = false;
if (flag != true) {
    // doSomething
}
```

### 将集合转为数组时使用toArray()方法且不带参数或者参数是类型相同零长度的数组

> 正确示范

```Java
List<String> strings = new ArrayList<>();
strings.add("boilingWater");
Object[] array = strings.toArray();
strings.toArray(new String[0]);
```

### 不要通过一个空的catch块忽略异常

> 错误示范

```Java
try {
}catch (Exception ignored){
}
```

### 日志使用条件形式或者使用占位符的方式

> 错误示范

```Java
logger.info("boilingWater=" + 1);
```

> 正确示范

```Java
logger.info("boilingWater={}", 1);
```

### LoggerFactory命名规范

> 正确示范

```Java
private static final Logger logger = LoggerFactory.getLogger(BoilingWater.class);
```

### 表达式的比较,应当遵循左侧倾向于变化、右侧倾向于不变的原则

> 错误示范

```Java
if (null != boilingWater) {
	// doSomething
}
```

> 正确示范

```Java
if (boilingWater != null) {
	// doSomething
}
```

### 禁止C风格的数组声明

> 例如:int num[]是c风格

### case语句块结束时如果不加break,需要有注释说明

> 正确示范

```java
public void fallthrough(String str) {
    switch (str) {
        case "1":
            logger.info("1");
            break;
        case "2":
            logger.info("2");// fall through
        case "3":
            logger.info("3");
            break;
        default:
    }
}

@SuppressWarnings("fallthrough")
public void fallthrough(String str) {
    switch (str) {
        case "1":
            logger.info("1");
            break;
        case "2":
            logger.info("2");
            break;
        case "3":
            logger.info("3");
        case "4":
            logger.info("4");
            break;
        default:
    }
}
```

### 不允许对参数进行赋值

> 错误示范

```Java
public int doSomething(int flag) {
  flag = 6;
  return flag;
}
```

