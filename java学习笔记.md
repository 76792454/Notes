在Double和Float类中都有这两个方法，用于判断是否是无穷大及是否为非数字 

public boolean isInfinite()
如果此对象表示的值是正无穷大或负无穷大，则返回 true；否则返回
false。
public boolean isNaN()

如果此值是一个非数字 (NaN) 值，则返回 true，否则返回
false。



实例代码：

if (Double.isInfinite(val) || Double.isNaN(val)){
　　　　throw new NumberFormatException("Infinite or NaN");

}



关于boolean占几个字节，众说纷纭，虽然boolean表现出非0即1的“位”特性，但是存储空间的基本计量单位是字节，不是位。所以boolean至少占一个字节。 
JVM规范中，boolean变量作为int处理，也就是4字节；boolean数组当做byte数组处理。

关于静态方法的调用：

不用在代码中写Math.pow()

在源文件上引入 import static java.lang.Math.*



跳出多层循环（不加tag 和break后的tag 表示跳出当前循环）

```java
tag:
for (int i = 0; i < 10; i++) {
    System.out.println("i:"+i);
    for (int j = 0; j < 10; j++) {
        if(j==3){
            break tag;
        }
    }
}
```

**基础知识：**Java中的继承机制使得一个类可以继承另一个类，继承的类称为子类，被继承的类称为父类。**在一个子类被创建的时候，首先会在内存中创建一个父类对象，然后在父类对象外部放上子类独有的属性，两者合起来形成一个子类的对象，所以子类可以继承父类中所有的属性和方法，包括private修饰的属性和方法，但是子类只是拥有父类private修饰的属性和方法，却不能直接使用它，也就是无法直接访问到它（子类可以通过调用父类的public声明的get方法来获取父类的private属性，但无法访问父类的private方法）**。同时子类可以对继承的方法进行重写（@Override），并且新建自己独有的方法。

arthars

1、获取需要进入的服务进程号
ps -ef | grep java_tomcat | grep -v grep | awk '{print $2}'

2、挂载arthas 
/opt/apache-tomcat/jre/bin/java -jar arthas-boot.jar  tomcat的pId

查看时间trace  com.tiandy.object.management.core.service.impl.PoliticalPersonServiceImpl queryPersonList
查看参数 watch com.tiandy.object.management.core.service.impl.PoliticalPersonServiceImpl



trace  com.tiandy.roommanage.core.service.impl.RoomManageServiceImpl queryRoomMessages
http://10.30.23.142:7000/pangu/roomManage/queryRoomMessages
9   	1.61s
18	2.41s
27	5.62s
36	11.97s
45 	22.34s

当需要强制类型转换时，建议用instanceof来判断一下能否进行转换

instanceof是Java中的二元运算符，左边是对象，右边是类；当对象是右边类或子类所创建对象时，返回true；否则，返回false。

json和bean之间的转换
https://www.cnblogs.com/cdf-opensource-007/p/7106018.html



