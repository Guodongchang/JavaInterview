# Mybatis

# 一.Mybatis

# 1:Mybatis入门案例2

![](../media/pictures/Mybatis.assets/28ece45410fbf7d17f27d1ec0e7c350a.png)

写单元测试的时候，可以直接通过SqlSession获得dao层接口的实例

![](../media/pictures/Mybatis.assets/07abbc5e21e0462b1b2b74fabb35b645.png)

当我们去写一个接口中的方法，一定要有对应的标签与之对应

通过，如果新增标签可以不写对应的接口中的方法

# Mybatis配置文件

## Properties

![](../media/pictures/Mybatis.assets/609b43213c289be20ad486b7f59a9aab.png)

## Setting

缓存

懒加载→多表查询

## typeAliases（别名→小名）

com.cskaoyan.bean.User→user

resultType、parameterType（不写）

![](../media/pictures/Mybatis.assets/c7c61d3c0288b956d84059be94f0dc33.png)

![](../media/pictures/Mybatis.assets/a31f6e293881fa06826ef6a64006cc1a.png)

## typeHandler（类型转换）

## plugins(插件)

pageHelper分页的插件

## mappers的配置

![](../media/pictures/Mybatis.assets/1bb3eafcc70899559d13b54797db7054.png)

# 2:log4j

springboot日志

日志级别

格式

1. 导包2、引入日志的配置文件

## 导包

![](../media/pictures/Mybatis.assets/f0f0daeabd97d1af29ce03e509eba810.png)

## 引入配置文件

![](../media/pictures/Mybatis.assets/907147e6f24cbfdad6393ed0f4c9e151.png)

![](../media/pictures/Mybatis.assets/e9dade919d4c54288f1a44ec08ceb3d8.png)

![](../media/pictures/Mybatis.assets/d3afe2d67e9dc6f6fb2cdff8f801968a.png)

其中他们之间的优先级是有一个等级划分的!如果输出的是优先级为7的debug,则,控制台会输出他和他以下优先级的所有日志! 下面的优先级来自互联网,和上面的优先级有出入!以后看书学习正确的!......

![log4j配置详解 - stone - stonexmx 的博客](../media/pictures/Mybatis.assets/None.gif)FATAL       0 
![log4j配置详解 - stone - stonexmx 的博客](../media/pictures/Mybatis.assets/None.gif)ERROR     3 
![log4j配置详解 - stone - stonexmx 的博客](../media/pictures/Mybatis.assets/None.gif)WARN      4 
![log4j配置详解 - stone - stonexmx 的博客](../media/pictures/Mybatis.assets/None.gif)INFO         6 
![log4j配置详解 - stone - stonexmx 的博客](../media/pictures/Mybatis.assets/None.gif)DEBUG     7 

## 格式

![](../media/pictures/Mybatis.assets/244de120464061b43dbcdf17b45e2b7b.png)

%d 日期（date）ABSOLUTE(这是一个格式名)

%5p 优先级（privilege）5代表使用5个占位符

%c{1}+方法名 顺序从后往前取

%L 行号

%m 消息 输出的日志信息

%n 换行

## 输出自定义的日志

Logger

![](../media/pictures/Mybatis.assets/a6e9a9d169cee645ce576cb5bf107158.png)

# 输入映射（重点）

## 没有注解

### 基本类型

![](../media/pictures/Mybatis.assets/83a1b468fd392ccecf45acaa8879f41f.png)

### Javabean

![](../media/pictures/Mybatis.assets/37312c9c3f613393976da42d00ec722e.png)

### Map

![](../media/pictures/Mybatis.assets/c0687928338743ade3cc064fe332d5e9.png)

### 多个参数

![](../media/pictures/Mybatis.assets/f9826a60fa8f8a4028020ce77a40519c.png)

![](../media/pictures/Mybatis.assets/07e93ba9c8453a42468f50aeb3fbe90e.png)

### List或数组（讲sql标签的时候补充这一部分）

## 使用注解来输入映射

\@Param 出现在dao层，在方法对应的参数前

![](../media/pictures/Mybatis.assets/e94e381542ce6a5276cf2d2389bb664d.png)

在@param注解里面写了什么,在映射文件中就可以用什么

# 输出映射（重点）

## 简单类型

## Pojo类型

![](../media/pictures/Mybatis.assets/4e6420072e38bee4e048ade8b96570e2.png)

查询结果的列名,(而不是表的列名),和javabean的成员变量名对应

## List或者数组

### 基本类型 list或array

![](../media/pictures/Mybatis.assets/947889ffe1930948f992d26b0a0130c7.png)

### Javabean list或array

![](../media/pictures/Mybatis.assets/eb9964748b317c1a37fce090209214c5.png)

## resultMap

输出结果的封装

将查询结果的列名和javabean的成员变量名建立联系

![](../media/pictures/Mybatis.assets/f582a299b13c116d463544dd6b29ae19.png)

# 3:Sql标签以及动态sql

## Where标签

成对存在，两个标签之间放条件

![](../media/pictures/Mybatis.assets/7915434e572267fbdd05dfda7616849a.png)

Where标签可以帮我们去掉他紧跟着的第一个关系词

![](../media/pictures/Mybatis.assets/9431ff5ca80dbd4b2fde230f4778ec58.png)

## If

这个标签中,如果if不成立,前面的and,标签会自动维护,就会取消的!不会出现异常!

如果写在标签中,&gt;

```xml
&gt; 表示>
```

![](../media/pictures/Mybatis.assets/78cacd391dd0f8b386b0488b2ef714be.png)

## Trim

![](../media/pictures/Mybatis.assets/55a5a5ab34a1c18b13c2c18499f1dc05.png)

## Choose when

If和else

![](../media/pictures/Mybatis.assets/9d2ff7a2dd1f6a76a6257a943be86343.png)

## Sql

![](../media/pictures/Mybatis.assets/f3d6d4a17da3d855d8a8d438810b96c3.png)

## SelectKey

主要做的是赋值的操作   怎么找到返回来的这个id在?????

![](../media/pictures/Mybatis.assets/1d00ae35bb5bc44f2cd85a2750f73703.png)

上面是以前学习的时候的笔记



下面是代码中的具体使用 : 有效

1.mapper.xml层是这么写的没有问题

![image-20191216174837924](../media/pictures/Mybatis.assets/image-20191216174837924.png)

返回来怎么用呢?

返回结果是直接不是返回给id  而是将id 直接赋值给了goods里面的id,你在使用的时候直接从goods里面拿出来就可以啦.

![image-20191216174946253](../media/pictures/Mybatis.assets/image-20191216174946253.png)

测试结果:是有效的

![image-20191216175119454](../media/pictures/Mybatis.assets/image-20191216175119454.png)

## Foreach

![](../media/pictures/Mybatis.assets/6e0394a9103c568b3fb0075524f22d51.png)

![](../media/pictures/Mybatis.assets/4355909065f11967e9ab248791a726e9.png)

# 多表查询

## 一对一

### Javabean关系维护

![](../media/pictures/Mybatis.assets/ae945170f5b70dfbf4968e6d57d39ba8.png)

### 表关系维护

![](../media/pictures/Mybatis.assets/c253afc16472579d6a348f02beb754b7.png)

### 执行查询

#### 分次查询

![](../media/pictures/Mybatis.assets/0ecfc7ec550d8290c38976c8db02f11c.png)

#### 连接查询

![](../media/pictures/Mybatis.assets/5b971953fb4207d0ad9f52848df12626.png)

## 一对多

### Javabean关系维护

![](../media/pictures/Mybatis.assets/b6a4beebca70bf67b560101339a2f39d.png)

### 表关系维护

![](../media/pictures/Mybatis.assets/4055431d51a31460cbf19c85e5905a9d.png)

### 执行查询

#### 分次查询

![](../media/pictures/Mybatis.assets/907dd4724c1663afba2cf56003d7810d.png)

#### 连接查询

首先查出全部的数据，接着进行封装

![](../media/pictures/Mybatis.assets/9990ab27686737fc6052494f7957453d.png)

![](../media/pictures/Mybatis.assets/932464a4c36a81623230e35c8bc60fdb.png)

## 多对多

双向的一对多

### Javabean关系维护

维护双向一对多，在各自bean中维护另一个bean的list

![](../media/pictures/Mybatis.assets/2175527c4b42f78cde1317a577cb28e5.png)

### 表关系的维护

通过一张中间表维护互相之间的关系

![](../media/pictures/Mybatis.assets/72bd009f2bb1a62911d758c9484da5e2.png)

### 执行查询

#### 分次查询

![](../media/pictures/Mybatis.assets/002e4fd10a98b6dcd662f4f31e0a217e.png)

![](../media/pictures/Mybatis.assets/637b5afe7e505750a622a17ed54c2701.png)

#### 连接查询

![](../media/pictures/Mybatis.assets/79f8d130e00c3f6823ff3919ae5f2b03.png)

![](../media/pictures/Mybatis.assets/2d7102052a7edb398b3155ee7fa0f647.png)

## 分次和连接查询的limit

一对多查询中

分次查询limit限制的是左一的数据数

连接查询limit限制的是右多的数据数

# 4:Orm层的优化

## 懒加载

分次查询的使用场景、默认没有开启懒加载、需要手动开启

当setting中lazyLoadingEnabled= true时，分次查询已经开启了懒加载

![](../media/pictures/Mybatis.assets/e33537b9eed9d9df7fcaa6e766f20d18.png)

开启懒加载开关后，默认分次查询都为懒加载；如果需要开启立即加载，需要让association或collection标签的fetchType属性为eager

![](../media/pictures/Mybatis.assets/f95c474594476e754aff3a8baa86a31f.png)

## 缓存

### 一级缓存

会话级别：同一个sqlSession

默认开启一级缓存

![](../media/pictures/Mybatis.assets/481fd8a8a889846fe082b60045554ce4.png)

![](../media/pictures/Mybatis.assets/e6223b2cf07ed10cb80c4ed2bd04f615.png)

### 二级缓存

3件事情：

1. 开启缓存开关
2. Javabean增加序列化的接口
3. 映射文件中增加缓存标签

![](../media/pictures/Mybatis.assets/3d3dd59f92df2f503a91242f244843a1.png)

> sqlSession.commit时存入二级缓存

> 执行cud操作时，清空二级缓存

# Alias

在类上出现定义别名

![](../media/pictures/Mybatis.assets/df734a7802b24ace9ba7d5a20627ae9b.png)

# 使用注解替代部分标签

CRUD

# 5.逆向工程mybatis generator

数据库中的表→Bean mapper mapper.xml

![](../media/pictures/Mybatis.assets/9df4ce47122f68305de1ac5ad7acaccd.png)

要想用mybatis代码生成器生成对象  要导入这两个依赖

```xml
<dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
</dependency>

<dependency>
            <groupId>org.mybatis.generator</groupId>
            <artifactId>mybatis-generator-core</artifactId>
            <version>1.3.7</version>
</dependency>
```

需要注意的点为:逆向工程生成器,所指定的generatorConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>
    <context id="testTables" targetRuntime="MyBatis3">
        <commentGenerator>
            <!-- 是否去除自动生成的注释 true：是 ： false:否 -->
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>
        <!--数据库连接的信息：驱动类、连接地址、用户名、密码 -->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://192.168.3.200:3306/litemalltest"
                        userId="root"
                        password="123456">
            <!--是否去除同名表  这句话一定要加上-->
            <property name="nullCatalogMeansCurrent" value="true"/>
        </jdbcConnection>
        <!--下面这些是oracle中用的配置-->
        <!--&lt;!&ndash;
            for oracle
           &ndash;&gt;
        <jdbcConnection driverClass="oracle.jdbc.OracleDriver"
            connectionURL="jdbc:oracle:thin:@127.0.0.1:1521:yycg"
            userId="yycg"
            password="yycg">
        </jdbcConnection>-->

        <!-- 默认false，
            为false把JDBC DECIMAL 和 NUMERIC 类型解析为Integer，
            为 true把JDBC DECIMAL 和 NUMERIC 类型解析为java.math.BigDecimal -->
        <!--<javaTypeResolver>
            <property name="forceBigDecimals" value="false" />
        </javaTypeResolver>-->

        <!-- javaModelGenerator javaBean生成的配置信息
             targetProject:生成PO类的位置
             targetPackage：生成PO类的类名-->
        <javaModelGenerator targetPackage="com.cskaoyan.bean"
                            targetProject=".\src\main\java">
            <!-- enableSubPackages:是否允许子包,是否让schema作为包的后缀
                 即targetPackage.schemaName.tableName -->
            <property name="enableSubPackages" value="true"/>
            <!-- 从数据库返回的值是否清理前后的空格 -->
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>

        <!--sqlMapGenerator Mapper映射文件的配置信息
            targetProject:mapper映射文件生成的位置
            targetPackage:生成mapper映射文件放在哪个包下-->
        <sqlMapGenerator targetPackage="com.cskaoyan.mapper"
                         targetProject=".\src\main\resources">
            <!-- enableSubPackages:是否让schema作为包的后缀 -->
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>

        <!--javaClientGenerator 生成 Model对象(JavaBean)和 mapper XML配置文件 对应的Dao代码
           targetProject:mapper接口生成的位置
           targetPackage:生成mapper接口放在哪个包下

           ANNOTATEDMAPPER
           XMLMAPPER
           MIXEDMAPPER
           -->

        <javaClientGenerator type="XMLMAPPER"
                             targetPackage="com.cskaoyan.mapper"
                             targetProject=".\src\main\java">
            <!-- enableSubPackages:是否让schema作为包的后缀 -->
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator><!---->
        <!-- 指定数据库表 -->
        <!-- 指定所有数据库表 -->
        <!--<table tableName="%"
               enableCountByExample="false"
               enableUpdateByExample="false"
               enableDeleteByExample="false"
               enableSelectByExample="false"
               enableInsert="false"
               enableDeleteByPrimaryKey="true"
               enableSelectByPrimaryKey="true"
               selectByExampleQueryId="false" ></table>-->

        <!-- 指定数据库表，要生成哪些表，就写哪些表，要和数据库中对应，不能写错！ -->
        
        //这下面 如果将ByExample全部false，那么生成的代码，就没有example 
        <!--<table tableName="j16_user_t"
               enableCountByExample="false"
               enableUpdateByExample="false"
               enableDeleteByExample="false"
               enableSelectByExample="false"
               enableInsert="true"
               enableDeleteByPrimaryKey="true"
               enableSelectByPrimaryKey="true"
               selectByExampleQueryId="false"
               domainObjectName="User"
        ></table>
        <table tableName="j16_student_t" domainObjectName="Studentz"/>-->
        <table tableName="litemall_goods" domainObjectName="LitemallGoods"/>
        <table tableName="litemall_admin_store" domainObjectName="LitemallAdminStore"/>

        <!--<table schema="" tableName="orders"></table>
             <table schema="" tableName="items"></table>
             <table schema="" tableName="orderdetail"></table>
      -->
        <!-- 有些表的字段需要指定java类型
         <table schema="" tableName="">
            <columnOverride column="" javaType="" />
        </table> -->
    </context>
</generatorConfiguration>

```

![1589373999929](../media/pictures/Mybatis.assets/1589373999929.png)

生成的bean对象是这个样子的，没有example。

![1589374030409](../media/pictures/Mybatis.assets/1589374030409.png)

只写了一个相对路径,这里要将下面的项目配置改成 如下: 

![image-20191214111544826](../media/pictures/Mybatis.assets/image-20191214111544826.png)

![1569397723500](../media/pictures/Mybatis.assets/1569397723500.png)

generatorConfig.xml放在module下面就可以,配置里面,要将工作路径设置成module目录下面!

然后运行Generator中的main方法就可以啦!就可以啦!



//下面这是Mybatis-plus 代码逆向工程:

```java
package com.cskaoyan;
import org.mybatis.generator.api.MyBatisGenerator;
import org.mybatis.generator.config.Configuration;
import org.mybatis.generator.config.xml.ConfigurationParser;
import org.mybatis.generator.internal.DefaultShellCallback;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

public class Generator {
    public void generator() throws Exception{
        List<String> warnings = new ArrayList<String>();
        boolean overwrite = true; //指向逆向工程配置文件
        File configFile = new File("generatorConfig.xml");
        System.out.println(configFile.getAbsolutePath());
        ConfigurationParser cp = new ConfigurationParser(warnings);
        Configuration config = cp.parseConfiguration(configFile);
        DefaultShellCallback callback = new DefaultShellCallback(overwrite);
        MyBatisGenerator myBatisGenerator =
                new MyBatisGenerator(config, callback, warnings);

        myBatisGenerator.generate(null);
    }

    public static void main(String[] args) throws Exception {
        try {
            Generator generatorSqlmap = new Generator();
            generatorSqlmap.generator();
        }
        catch (Exception e) {
            e.printStackTrace();
        }

    }
}

```

在实际项目开发中,不要在当前项目中使用逆向工程,会报错.

在其他项目中用逆向工程生成代码,然后拷进来

拷进来要注意:

1.修改包名和导入的包名等:

![image-20191214114937228](../media/pictures/Mybatis.assets/image-20191214114937228.png)

2.正确的mapper是这样的:

![image-20191214115029500](../media/pictures/Mybatis.assets/image-20191214115029500.png)

如果下面买有画红线,说明正确.

如果错误:

需要修改mapper.xml中的命名空间:

![image-20191214115204849](../media/pictures/Mybatis.assets/image-20191214115204849.png)

这些地方都修改好,修改好的标志是:

![image-20191214115246938](../media/pictures/Mybatis.assets/image-20191214115246938.png)

对应mapper的接口不是红色 说明正确.



## 逆向工程中的example(牛皮)

![1569844094508](../media/pictures/Mybatis.assets/1569844094508.png)

### 二:example实例解析

mybatis的逆向工程中会生成实例及实例对应的example，example用于添加条件，相当where后面的部分 
xxxExample example = new xxxExample(); 
Criteria criteria = new Example().createCriteria();

![1569844136788](../media/pictures/Mybatis.assets/1569844136788.png)

### 三:应用举例:

#### 1.查询

1.selectByPrimaryKey()

```java
User user = XxxMapper.selectByPrimaryKey(100); //相当于select * from user where id = 100
```

2.selectByExample() 和 selectByExampleWithBLOGs()

```java
UserExample example = new UserExample();
Criteria criteria = example.createCriteria();
criteria.andUsernameEqualTo("wyw");
criteria.andUsernameIsNull();
example.setOrderByClause("username asc,email desc");
List<?>list = XxxMapper.selectByExample(example);
//相当于：select * from user where username = 'wyw' and  username is null order by username asc,email desc
```

注：在iBator逆向工程生成的文件XxxExample.java中包含一个static的内部类Criteria，Criteria中的方法是定义SQL 语句where后的查询条件。

#### 2.插入数据

1.insert()

```java
User user = new User();
user.setId("dsfgsdfgdsfgds");
user.setUsername("admin");
user.setPassword("admin")
user.setEmail("wyw@163.com");
XxxMapper.insert(user);
//相当于：insert into user(ID,username,password,email) values ('dsfgsdfgdsfgds','admin','admin','wyw@126.com');
```

#### 3.更新数据

1.updateByPrimaryKey()

```java
User user =new User();
user.setId("dsfgsdfgdsfgds");
user.setUsername("wyw");
user.setPassword("wyw");
user.setEmail("wyw@163.com");
XxxMapper.updateByPrimaryKey(user);
//相当于：update user set username='wyw', password='wyw', email='wyw@163.com' where id='dsfgsdfgdsfgds'

```

2.updateByPrimaryKeySelective()

```java
User user = new User();
user.setId("dsfgsdfgdsfgds");
user.setPassword("wyw");
XxxMapper.updateByPrimaryKey(user);
//相当于：update user set password='wyw' where id='dsfgsdfgdsfgds'

```

3.updateByExample() 和 updateByExampleSelective()

```java
UserExample example = new UserExample();
Criteria criteria = example.createCriteria();
criteria.andUsernameEqualTo("admin");
User user = new User();
user.setPassword("wyw");
XxxMapper.updateByPrimaryKeySelective(user,example);
//相当于：update user set password='wyw' where username='admin'

```

updateByExample()更新所有的字段，包括字段为null的也更新，建议使用 updateByExampleSelective()更新想更新的字段

#### 4.删除数据

1.deleteByPrimaryKey()

```java
XxxMapper.deleteByPrimaryKey(1);  //相当于：delete from user where id=1

```

2.deleteByExample()

```java
UserExample example = new UserExample();
Criteria criteria = example.createCriteria();
criteria.andUsernameEqualTo("admin");
XxxMapper.deleteByExample(example);
//相当于：delete from user where username='admin'
```

#### 5.查询数据数量

1.countByExample()

```java
UserExample example = new UserExample();
Criteria criteria = example.createCriteria();
criteria.andUsernameEqualTo("wyw");
int count = XxxMapper.countByExample(example);
//相当于：select count(*) from user where username='wyw'
```



# 二.Mybatis-plus

## 1.分页:

```java
 //Mybatis-plus 自带分页查询
 IPage<ActivityEntity> ipage = new Page<>(dto.getPageNum(),dto.getPageSize());
 IPage<ActivityEntity> activityPage = activityService.page(ipage);
```



## CRUD接口:

### services CRUD 接口 

好多业务需求中,不需要mapper层东西,直接就可以在controller层用services层的CRUD接口.

项目中用到的 **查询分页**和**模糊查询**结合的情况:

```java
QueryWrapper<ActivityEntity> queryWrapper = new QueryWrapper<>();
queryWrapper.like(SqlConst.TITLE, dto.getTitle())
    .or().
    like(SqlConst.LANG, dto.getLang());
IPage<ActivityEntity> ipage = new Page<>(dto.getPageNum(),dto.getPageSize());
IPage<ActivityEntity> iPage = activityService.page(ipage,queryWrapper);
```

如果需求是返回一个list :

这个方法里面的多数都是返回有所有信息的对象所组成的list\

官方文档:

```java
// 查询所有
List<T> list();
// 查询列表
List<T> list(Wrapper<T> queryWrapper);   //上次用到这个 直接services层调用
// 查询（根据ID 批量查询）
Collection<T> listByIds(Collection<? extends Serializable> idList);
// 查询（根据 columnMap 条件）
Collection<T> listByMap(Map<String, Object> columnMap);
// 查询所有列表
List<Map<String, Object>> listMaps();
// 查询列表
List<Map<String, Object>> listMaps(Wrapper<T> queryWrapper);
// 查询全部记录
List<Object> listObjs();
// 查询全部记录
<V> List<V> listObjs(Function<? super Object, V> mapper);
// 根据 Wrapper 条件，查询全部记录
List<Object> listObjs(Wrapper<T> queryWrapper);
// 根据 Wrapper 条件，查询全部记录
<V> List<V> listObjs(Wrapper<T> queryWrapper, Function<? super Object, V> mapper);
```

##### 参数说明 

|                类型                |    参数名    |              描述               |
| :--------------------------------: | :----------: | :-----------------------------: |
|             Wrapper<T>             | queryWrapper | 实体对象封装操作类 QueryWrapper |
| Collection<? extends Serializable> |    idList    |           主键ID列表            |
|        Map<?String, Object>        |  columnMap   |         表字段 map 对象         |
|    Function<? super Object, V>     |    mapper    |            转换函数             |

需要注意的地方:

```java
QueryWrapper<DictionaryEntity> queryWrapper = new QueryWrapper<>();
            queryWrapper.eq("state", BizConst.BIZ_STATUS_VALID)
                    .eq("type", dto.getType());

            List<DictionaryEntity> dicts = dictService.list(queryWrapper);

```

如果这里想用service默认的方法,原来的service需要继承IService

```java
public interface IDictionaryService extends IService<DictionaryEntity>

```

泛型里面最好指定 Entity ,同时实现类 也要继承基础实现类:

```java
extends ServiceImpl<DictionaryMapper, DictionaryEntity>

```

完整的是这个样子的:

![image-20191213123658159](../media/pictures/Mybatis.assets/image-20191213123658159.png)

这里的Mapper也要继承基础的mapper:

```java
extends BaseMapper<DictionaryEntity>

```

这样的:

![image-20191213123801283](../media/pictures/Mybatis.assets/image-20191213123801283.png)

这些都有了以后,service层才可以用  为什么要mapper????  能不能不指定泛型中的bean 



### mapper CRUD 接口







## 2.MybatisPlus中的注解:

@TableName：数据库表相关
 @TableId：表主键标识
 @TableField：表字段标识
 @TableLogic：表字段逻辑处理注解（逻辑删除）

@TableId(type= IdType.ID_WORKER_STR)

@TableField(exist = false)：表示该属性不为数据库表字段，但又是必须使用的。

@TableField(exist = true)：表示该属性为数据库表字段。

@TableField(condition = SqlCondition.LIKE)：表示该属性可以模糊搜索。

@TableField(fill = FieldFill.INSERT)：注解填充字段 ，生成器策略部分也可以配置！



项目中用到的注解是@TableField(exist = false),表示这个属性不为数据库表字段,但是又是必须使用的,所以这样写.



Mybatis-Plus的基本使用(用法来自于官方文档):

关于**ActiveRecord**的操作,这里搜索一段关于ActiveRecord的说明.

## ActiveRecord介绍

- 是一种领域模型模式
- 特点
  1、作用于模型层
  2、一个模型类对应关系型数据库中的一个表
  3、模型类的一个实例对应表中的一行数据
  4、封装了对数据库的访问，CURD操作
  5、ActiveRecord特别适合web快速开发
- ActiveRecord是JFinal最核心的组成部分之一
- 通过ActiveRecord来操作数据库，将极大地减少代码量，极大地提升开发效率



```java
@TableName("sys_user") // 注解指定表名
public class User extends Model<User> {

  ... // fields

  ... // getter and setter

  /** 指定主键 */
  @Override
  protected Serializable pkVal() {
      return this.id;
  }
}

```

## 条件构造器:

## [条件参数说明](https://baomidou.gitee.io/mybatis-plus-doc/#/wrapper?id=条件参数说明)

| 查询方式     | 说明                              |
| ------------ | --------------------------------- |
| setSqlSelect | 设置 SELECT 查询字段              |
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

TeamController 中 ,   用的是ne,意思是不等于. 



## 3.Mybatis-plus的代码生成器:

使用之前要导入依赖:

```xml
<!--mybatis-plus 上面这个Mybatis-plus的依赖是包含下面的,如果只用生成器,用下面的即可-->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus</artifactId>
    <version>2.1.9</version>
</dependency>

<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-generator</artifactId>
    <version>3.3.0</version>
</dependency>

<!--生成器放在test中,就要导入这个-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
<!--如果是spring 项目 还需要下面这个依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
<!--如果单独测试 而不是在spring项目中,这里还要这个依赖-->
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-nop</artifactId>
    <version>1.7.24</version>
</dependency>
<!--mysql的依赖也需要-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.47</version>
</dependency>

```

代码生成器:

```java
package generator;

import com.baomidou.mybatisplus.generator.AutoGenerator;
import com.baomidou.mybatisplus.generator.InjectionConfig;
import com.baomidou.mybatisplus.generator.config.DataSourceConfig;
import com.baomidou.mybatisplus.generator.config.GlobalConfig;
import com.baomidou.mybatisplus.generator.config.PackageConfig;
import com.baomidou.mybatisplus.generator.config.StrategyConfig;
import com.baomidou.mybatisplus.generator.config.converts.MySqlTypeConvert;
import com.baomidou.mybatisplus.generator.config.rules.DbColumnType;
import com.baomidou.mybatisplus.generator.config.rules.DbType;
import com.baomidou.mybatisplus.generator.config.rules.NamingStrategy;
import org.junit.Test;

import java.util.HashMap;
import java.util.Map;

/**
 * 实体生成
 *
 * @author fengshuonan
 * @date 2017-08-23 12:15
 */
public class EntityGenerator {

    @Test
    public void entityGenerator() {
        AutoGenerator mpg = new AutoGenerator();

        // 全局配置
        GlobalConfig gc = new GlobalConfig();
        //gc.setOutputDir("/Users/ciggar/cskaoyan/csworkspace/guns/guns-promo/src/main/java");//这里写你自己的java目录
        gc.setOutputDir("D:\\Steve\\Code\\JavaEEWorkPlace\\mybatis4\\demo04_generator\\src\\main\\java");//这里写你自己的java目录
        gc.setFileOverride(true);//是否覆盖
        gc.setActiveRecord(true);
        gc.setEnableCache(false);// XML 二级缓存
        gc.setBaseResultMap(true);// XML ResultMap
        gc.setBaseColumnList(false);// XML columList
        gc.setAuthor("ciggar");
        mpg.setGlobalConfig(gc);

        // 数据源配置
        DataSourceConfig dsc = new DataSourceConfig();
        dsc.setDbType(DbType.MYSQL);
        dsc.setTypeConvert(new MySqlTypeConvert() {
            // 自定义数据库表字段类型转换【可选】
            @Override
            public DbColumnType processTypeConvert(String fieldType) {
                return super.processTypeConvert(fieldType);
            }
        });
        dsc.setDriverName("com.mysql.jdbc.Driver");
        dsc.setUsername("root");
        dsc.setPassword("123456");
        dsc.setUrl("jdbc:mysql://192.168.3.200:3306/litemalltest?autoReconnect=true&useUnicode=true&useSSL=true&characterEncoding=utf8&serverTimezone=GMT%2B8");
        mpg.setDataSource(dsc);

        // 策略配置
        StrategyConfig strategy = new StrategyConfig();
        //strategy.setTablePrefix(new String[]{"_"});// 此处可以修改为您的表前缀
        strategy.setNaming(NamingStrategy.underline_to_camel);// 表名生成策略
        //下面这里是表名  放到数组里面即可
        strategy.setInclude(new String[]{"litemall_store","litemall_user_wallet"});
        mpg.setStrategy(strategy);

        // 包配置
        PackageConfig pc = new PackageConfig();
        pc.setParent(null);
        pc.setEntity("com.cskaoyan.entity");
        pc.setMapper("com.cskaoyan.dao");
        pc.setXml("com.cskaoyan.mapping");
        pc.setService("com.cskaoyan.service");       
        pc.setServiceImpl("com.cskaoyan.service.iml");   
        pc.setController("TTT");    //TTT 一般不生成controller层  生成以后 删除
        mpg.setPackageInfo(pc);

        // 注入自定义配置，可以在 VM 中使用 cfg.abc 设置的值
        InjectionConfig cfg = new InjectionConfig() {
            @Override
            public void initMap() {
                Map<String, Object> map = new HashMap<>();
                map.put("abc", this.getConfig().getGlobalConfig().getAuthor() + "-mp");
                this.setMap(map);
            }
        };
        mpg.setCfg(cfg);

        // 执行生成
        mpg.execute();

        // 打印注入设置
        System.err.println(mpg.getCfg().getMap().get("abc"));
    }
}

```

# 模糊查询

```xml
<resultMap id="BaseResultMapAddSales" type="org.linlinjava.litemall.db.domain.LitemallGoodsForSales">
    <id column="id" jdbcType="INTEGER" property="id" />
    <result column="goods_sn" jdbcType="VARCHAR" property="goodsSn" />
    <result column="store_id" jdbcType="INTEGER" property="storeId" />
    <result column="name" jdbcType="VARCHAR" property="name" />
    <result column="category_id" jdbcType="INTEGER" property="categoryId" />
    <result column="brand_id" jdbcType="INTEGER" property="brandId" />
    <result column="gallery" jdbcType="VARCHAR" property="gallery" typeHandler="org.linlinjava.litemall.db.mybatis.JsonStringArrayTypeHandler" />
    <result column="keywords" jdbcType="VARCHAR" property="keywords" />
    <result column="brief" jdbcType="VARCHAR" property="brief" />
    <result column="is_on_sale" jdbcType="BIT" property="isOnSale" />
    <result column="sort_order" jdbcType="SMALLINT" property="sortOrder" />
    <result column="pic_url" jdbcType="VARCHAR" property="picUrl" />
    <result column="share_url" jdbcType="VARCHAR" property="shareUrl" />
    <result column="is_new" jdbcType="BIT" property="isNew" />
    <result column="is_hot" jdbcType="BIT" property="isHot" />
    <result column="unit" jdbcType="VARCHAR" property="unit" />
    <result column="counter_price" jdbcType="DECIMAL" property="counterPrice" />
    <result column="retail_price" jdbcType="DECIMAL" property="retailPrice" />
    <result column="add_time" jdbcType="TIMESTAMP" property="addTime" />
    <result column="update_time" jdbcType="TIMESTAMP" property="updateTime" />
    <result column="deleted" jdbcType="BIT" property="deleted" />
    <result column="sales" jdbcType="INTEGER" property="sales" />
  </resultMap>
  <select id="saleList"  resultMap="BaseResultMapAddSales">
    SELECT lg.id, lg.goods_sn,lg.store_id,lg.name,lg.category_id,lg.brand_id,lg.gallery,lg.keywords,
			lg.brief,lg.is_on_sale,lg.pic_url,lg.share_url,lg.is_new,lg.is_hot,lg.unit,
			lg.counter_price,lg.retail_price,lg.detail,lg.add_time,lg.update_time,lg.deleted ,lgs.number as sales
        FROM litemall_goods lg
        INNER JOIN litemall_goods_sales lgs ON lg.id = lgs.good_id 
        WHERE lg.deleted = 0 and name like #{name} ORDER BY #{sort} limit #{limit} offset #{page}
  </select>

```



传参数的时候要注意:  name这里拼接一个 page -1  这里要注意

![image-20191225105630546](../media/pictures/Mybatis.assets/image-20191225105630546.png)



# github上面一个开源的mybatis逆向工程生成器

https://github.com/zouzg/mybatis-generator-gui

这是地址 ，测试发现，真好用，真香。

![1591604313901](../media/pictures/Mybatis.assets/1591604313901.png)













