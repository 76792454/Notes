Spring学习笔记

https://blog.csdn.net/java_lyvee/article/details/101793774

IOC容器:

三种注入方式:接口注入,setter注入,构造注入

 @Autowired默认注入ByType如果发现多个bean会根据ByName如果还有多个bean会抛异常

Controller里的对于Service的自动注入 ,程序现在容器内查找到XXXservice的Bean刚好找到XXXservice的实现类所以就把实现类注入到XXXservice中

IOC的两种容器:

BeanFactory和ApplicationContext

BeanDefinition(封装Bean的信息)就是依赖反转中管理对象依赖关系的数据抽象,也是容器实现依赖反转的核心数据结构，ApplicationContext继承了BeanFactory接口

在Spring中所以的Bean都是有beanFactory管理的

Spring中有两种bean一种普通bean另外一种FactoryBean,FactoryBean返回的对象不是指定的一个类的实例,而是该FactoryBean的getObject返回的对象如果要返回FactoryBean本身在id前边加&符号来获取

FileXmlApplication

IOC容器的初始化过程:

```java
super(parent);
this.setConfigLocations(configLocations);
if (refresh) {
    this.refresh();
}
```

IOC容器的初始化由refresh()方法启动,这个启动包括

1Resource定位:找到Bean的资源文件 BeanDefinition对Resource进行了各种封装比如FileSystemResource和ClassPathResource等等一个加载文件bean信息,一个根据Class加载Bean的信息

2载入:把用户定义好的bean表示成IOC容器内部的数据结构（容器内部数据结构就是BeanDefinition）这个BeanDefinition实际上就是POJO在IOC容器中的抽象

3注册：向容器中注入这些BeanDefinition的过程

为什么Spring不能用Class直接建立bean，因为Class无法完成bean的抽象，比如bean的作用域，bean的注入模型，bean是否是懒加载等等信息

Spring实例化Bean的过程

1、实例化一个ApplicationContext

2、调用bean工厂完成后置扫描

3、循环解析扫描出来的类信息

4、实例化一个BeanDefinition对象存储解析出来的信息	

5、把BeanDefinition放到BeanDefinitionMap中方便调用,便于实例化bean

6、再次调用bean工厂后置处理器(实际上就是干预beanFactory的初始化,也就是在BeanFactory初始化之前做一些操作)

7、Spring在实例化bean之前会做一些验证操作,比如验证bean是否单例

8、验证完成Spring在实例化一个bean之前需要的构造方法，Spring实例对象是通过构造反射，所以需要知道哪一个构造方法 AbstractAutowireCapableBeanFactory.createBeanInstance()方法

9、对象已经通过构造实例化出来了，但是属性还没有注入（AbstractApplicationContext的finishBeanFactoryInitialization方法中完成bean的实例化）

10、Spring处理合并后的BeanDefinition

11、判断是否支持循环依赖，如果支持提前把一个工厂存入SingletonFactories-map(判断是否支持循环依赖，如果支持则提前暴露一个工厂对象，注意是工厂对象)注意:Map就在BeanFactory里

12、判断是否需要完成属性注入

13、如果需要注入属性，开始注入属性

14、调用bean类型回调Aware接口

15、调用生命周期回调方法

16、如果需要代理完成代理

17、put到单例池中—bean完成—存在Spring容器中



Spring注解的执行顺序:Constructor构造->@AutoWired->@PostConstruct

@AutoWired在Spring容器初始化话一个空对象后开始注入属性



getBean方法本质上调用的是doGetBean方法





Spring容器初始化的过程中已经把SpringBean(单例)初始化完毕了

SpringBean的懒加载 :在`ApplicationContext`容器中，当容器一启动时，所有的bean（单例的）都会被创建和注入依赖，这也被视为IOC容器启动过程中的一个步骤。那如何让一个bean在需要的时候再被创建，而不是容器一加载的时候呢

Singleton和Prototype的区别就是Singleton会在容器加载的时候加载这个Bean Prototype会在getBean就是需要它的时候去加载这个Bean

Spring扫描类的顺序默认按照字母的顺序



具体扫描方式就是根据@ComponentScan("com.example.demo.test") 

获取本地项目的路径 例如D:\work\target\classes\

把@ComponentScan("com.example.demo.test") 里的字符串拼到路径上D:\work\target\classes\com\example\demo\test

File file = new File("D:\work\target\classes\com\example\demo\test");

file.list();递归去扫描类(假如有类X,Y)

然后通过反射Class.forName("com.example.demo.test.X");去创建对象



 ConfigurationClassPostProcessor的两大作用(主要负责扫描类,处理bdMap) 先执行子类在执行父类

1 BeanDefinitionRegistryPostProcessor（需要在扫描之前做一些事可以扩展当前类）---扫描注解类   生成bd  放到bdmap中

2 BeanFactoryPostProcessor （需要在扫描之后做一些事可以扩展当前类） 修改bdmap

先执行子类BeanDefinitionRegistryPostProcessor-----先执行Spring内部提供然后调用程序员自己实现的.----原理:自己把一个BeanDefinitionRegistryPostProcessor的实现类ConfigurationClassPostProcessor的bd放到bdmap只能中,想要执行先得实例化,从容器中拿,如果有就直接执行,如果没有spring传一个BeanDefinitionRegistryPostProcessor类型给容器,容器会从bdmap（容器加载的时候会会把这个放到bdmap中）当中找到一个ConfigurationClassPostProcessor 执行扫描

在执行父类BeanFactoryPostProcessor  ---先执行spring内部提供在执行程序员自己的



当Spring调用getBean的时候会做两件事:

1会从容器里拿已经实例化好的bean

2如果拿不到他就会从beanDefinition中获取beanDefinition对象 把它实例化成一个bean

Spring事务回滚
TransactionAspectSupport.currentTransactionStatus().setRollbackOnly();
