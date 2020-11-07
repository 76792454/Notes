MyBaitis-Plus文档

https://baomidou.com/guide/

注意:

1引入Mybatis-Plus不要引入依赖,容易造成版本问题

2如果数据库连接不上,在Mysql的my.ini的最后加上skip-grant-tables

3引入依赖在代码生成器的文档里

Wrapper条件构造器的使用

```java
UpdateWrapper<User> updateWrapper = new UpdateWrapper<>();
updateWrapper.eq("name","admin");
User user = new User();
user.setId("1");
user.setName("haha");
userService.saveOrUpdate(user,updateWrapper);
```

 Wrapper的条件

| setSqlSelect | 设置 SELECT 查询字段              |
| ------------ | --------------------------------- |
| where        | WHERE 语句，拼接 + `WHERE 条件`   |
| and          | AND 语句，拼接 + `AND 字段=值`    |
| andNew       | AND 语句，拼接 + `AND (字段=值)`  |
| or           | OR 语句，拼接 + `OR 字段=值`      |
| orNew        | OR 语句，拼接 + `OR (字段=值)`    |
| eq           | 等于=                             |
| allEq        | 基于 map 内容等于=                |
| ne           | 不等于<>                          |
| gt           | 大于>                             |
| ge           | 大于等于>=                        |
| lt           | 小于<                             |
| le           | 小于等于<=                        |
| like         | 模糊查询 LIKE                     |
| notLike      | 模糊查询 NOT LIKE                 |
| in           | IN 查询                           |
| notIn        | NOT IN 查询                       |
| isNull       | NULL 值查询                       |
| isNotNull    | IS NOT NULL                       |
| groupBy      | 分组 GROUP BY                     |
| having       | HAVING 关键词                     |
| orderBy      | 排序 ORDER BY                     |
| orderAsc     | ASC 排序 ORDER BY                 |
| orderDesc    | DESC 排序 ORDER BY                |
| exists       | EXISTS 条件语句                   |
| notExists    | NOT EXISTS 条件语句               |
| between      | BETWEEN 条件语句                  |
| notBetween   | NOT BETWEEN 条件语句              |
| addFilter    | 自由拼接 SQL                      |
| last         | 拼接在最后，例如：last("LIMIT 1") |

MyBatis-Plus查询分页显示所有记录 配置分页拦截器

```java
package com.example.demo.demo1.sys.config;

import com.baomidou.mybatisplus.annotation.DbType;
import com.baomidou.mybatisplus.autoconfigure.ConfigurationCustomizer;
import com.baomidou.mybatisplus.extension.plugins.MybatisPlusInterceptor;
import com.baomidou.mybatisplus.extension.plugins.PaginationInterceptor;
import com.baomidou.mybatisplus.extension.plugins.inner.PaginationInnerInterceptor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class mybatisPlusConfig {
    //过时方法
//    @Bean
//    public PaginationInterceptor paginationInterceptor(){
//        return new PaginationInterceptor();
//    }

    //新的方法
    /**
     * 新的分页插件,一缓和二缓遵循mybatis的规则,需要设置 MybatisConfiguration#useDeprecatedExecutor = false 避免缓存出现问题(该属性会在旧插件移除后一同移除)
     */
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor() {
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        interceptor.addInnerInterceptor(new PaginationInnerInterceptor(DbType.H2));
        return interceptor;
    }

    @Bean
    public ConfigurationCustomizer configurationCustomizer() {
        return configuration -> configuration.setUseDeprecatedExecutor(false);
    }
}


```

## 使用 Wrapper 自定义SQL

参考网站

https://blog.csdn.net/weixin_38111957/article/details/91539019

使用注解

```java
@Select("SELECT * FROM USER ${ew.customSqlSegment}")
List<User> selectByMyWrapper(@Param(Constants.WRAPPER) Wrapper<User> userWrapper);
@Select("SELECT * FROM USER WHERE NAME = #{name}")
List<User> selectByName(@Param("name") String name);
```

使用xml配置文件还要写xml配置文件

```java
List<User> selectByMyWrapper(@Param(Constants.WRAPPER) Wrapper<User> userWrapper);
List<User> selectByName(@Param("name") String name);
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.example.demo.demo1.sys.mapper.UserMapper">
    <select id="selectByMyWrapper" resultType="com.example.demo.demo1.sys.entity.User">
        SELECT * FROM USER ${ew.customSqlSegment}
    </select>
    <select id = "selectByName" resultType="com.example.demo.demo1.sys.entity.User">
        SELECT * FROM USER WHERE name = #{name}
    </select>
</mapper>
```

测试类

```java
List<User> users = userMapper.selectByName("haha");
users.forEach(System.out::println);
QueryWrapper queryWrapper = new QueryWrapper();
queryWrapper.eq("name","haha");
List<User> users = userMapper.selectByMyWrapper(queryWrapper);
users.forEach(System.out::println);
```

MybatisPlus 自动填充功能

https://blog.csdn.net/qq_38225558/article/details/100054690

MybatisPlus配置多数据源

https://www.cnblogs.com/angel-devil/p/12557836.html



数据库乐观锁和悲观锁

https://www.jianshu.com/p/d2ac26ca6525

