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

### 不用的代码段直接删除,不要注释掉

### 行末或空行不能有多余空格

> 错误示范

```Java
public void boilingWater(){ // 我是滚水科技方法
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

### 名字长度不能超过64个字符

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