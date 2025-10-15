[合集 - java学习(29)](https://github.com)

[1.Markdown学习笔记06-04](https://github.com/gyg9006/p/18909532)[2.JAVA的版本及JDK的安装和卸载06-12](https://github.com/gyg9006/p/18912025)[3.第一个程序HelloWorld06-13](https://github.com/gyg9006/p/18925608)[4.IDEA的安装与卸载06-13](https://github.com/gyg9006/p/18927694)[5.01Java基础语法之注释、标识符、关键字、数据类型及拓展06-17](https://github.com/gyg9006/p/18930876)[6.02Java基础语法之类型转换、变量、常量06-18](https://github.com/gyg9006/p/18934194)[7.03Java基础语法之运算符06-19](https://github.com/gyg9006/p/18936710)[8.04Java基础语法之包机制07-01](https://github.com/gyg9006/p/18957375)[9.05Java基础语法之流程控制07-07](https://github.com/gyg9006/p/18963061)[10.06Java基础之方法07-08](https://github.com/gyg9006/p/18970740)[11.07Java基础之数组07-14](https://github.com/gyg9006/p/18973244)[12.08Java基础之面向对象07-21](https://github.com/gyg9006/p/18984330)[13.09Java基础之封装07-24](https://github.com/gyg9006/p/18996640)[14.10Java基础之static07-22](https://github.com/gyg9006/p/18996649)[15.11Java基础之继承07-23](https://github.com/gyg9006/p/18996637)[16.12Java基础之多态07-24](https://github.com/gyg9006/p/19000398):[虎跃加速](https://huyuejiasu.com)[17.13Java基础之final关键字、常量详解07-24](https://github.com/gyg9006/p/19002054)[18.14Java基础之抽象类、接口07-25](https://github.com/gyg9006/p/19002048)[19.15Java基础之内部类07-27](https://github.com/gyg9006/p/19004098)[20.16Java基础之枚举、泛型、API、Objects类、包装类07-29](https://github.com/gyg9006/p/19007839)[21.17Java基础之常用API08-01](https://github.com/gyg9006/p/19011026)[22.18Java基础之API（二）08-05](https://github.com/gyg9006/p/19017194)[23.19Java基础之异常08-06](https://github.com/gyg9006/p/19024047)[24.20Java基础之集合进阶08-11](https://github.com/gyg9006/p/19025139)[25.21Java基础之集合进阶(二)08-14](https://github.com/gyg9006/p/19032088)[26.23Java基础之File09-10](https://github.com/gyg9006/p/19074316)[27.24Java基础之IO09-12](https://github.com/gyg9006/p/19083298)[28.25Java基础之IO(二)09-24](https://github.com/gyg9006/p/19087385)

29.26Java基础之特殊文本文件、日志技术10-15

收起

# 特殊文件

**为什么要用这些特殊文件？**

* 存储多个用户的：用户名、密码

## **Rroperties**

![image](https://img2024.cnblogs.com/blog/3656114/202509/3656114-20250925092928048-2092535694.png)

* 是一个Map集合(键值对集合)，但是我们一般不会当集合使用。
* **核心作用：Properties是用来代表属性文件的，通过Properties可以读写属性文件里的内容。**

**使用Properties读取属性文件的键值对数据**
![image](https://img2024.cnblogs.com/blog/3656114/202509/3656114-20250925093849404-1843425406.png)
**案例**

```
users.properties内容如下:
admin=123456
赵敏=wuji
张无忌=zhaomin
灰太狼=xiyangyang

测试文件：
//目标：Properties读取属性文件中的键值对数据
public class PropertiesDemo01 {
    public static void main(String[] args) throws Exception {
        //1.创建属性集对象，代表一个属性文件
        Properties prop = new Properties();

        //2. 加载属性文件信息到属性集对象中去
        prop.load(new FileReader("day11-special-file-log-code\\src\\com\\javabase\\d1_properties\\users.properties"));
        System.out.println(prop);

        //根据键取值
        System.out.println(prop.getProperty("admin"));
        Set keys = prop.stringPropertyNames();

        for (String key : keys) {
            String value = prop.getProperty(key);
            System.out.println(key + "=" + value);
        }
        
        //3.遍历数据
        prop.forEach((k,v)-> System.out.println(k + "====>" + v));

    }
}
```

---

**使用Properties把键值对数据写出到属性文件里去**
![image]()
**案例**

```
//目标：Properties写入属性文件中的键值对数据
public class PropertiesDemo02 {
    public static void main(String[] args) throws Exception {
        //1. 创建属性集对象
        Properties prop = new Properties();

        prop.setProperty("玄冥二老", "wangfei");
        prop.setProperty("tom", "jay");
        prop.setProperty("金毛狮王", "成昆");
        System.out.println(prop);

        //2. 存储文件
        prop.store(new FileWriter("day11-special-file-log-code\\src\\com\\javabase\\d1_properties\\users1.properties"),"lots of users");
    }
}
```

---

**案例：把文件中某个键值对中的值修改，改完后重新写回文件**

```
people.txt文件内容如下：
张三=45
张全蛋=24
李二狗=24
李四=23
李芳=35
王麻子=13

测试文件：
public class PropertiesTest {
    public static void main(String[] args) throws Exception {
        //1.创建Properties对象
        Properties prop = new Properties();

        //2.加载文件
        prop.load(new FileReader("day11-special-file-log-code\\src\\com\\javabase\\d1_properties\\people.txt"));
        //3.判断是否存在“李芳”
        if(prop.containsKey("李芳")){
            prop.setProperty("李芳", Integer.toString(18));
        }

        //4. 把属性文件对象，重新存入到属性文件中去
        prop.store(new FileWriter("day11-special-file-log-code\\src\\com\\javabase\\d1_properties\\people.txt"), "");

    }
}
```

---

## XML(全称EXtensible Markup Language，可拓展标记语言)

* 本质是一种数据的格式，可以用来存储复杂的数据结构和数据关系。

**XML的特点**

* XML中的"<标签名>"称为一个标签或一个元素，一般是成对出现的。
* XML中的标签名可以自己定义(可拓展)，但必须要正确的嵌套。
* XML中只能有一个根标签。
* XML中的标签可以有属性。
* 如果一个文件中放置的是XML格式的数据，这个文件就是XML文件，后缀一般要写成.xml。

**XML的创建**

* 就是创建一个XML类型的文件，要求文件的后缀必须使用xml，如hello\_world.xml。
  ![image]()

**XML语法规则**

* XML文件的后缀名为：xml，文档声明必须是第一行。
  ![image]()
* XML中可以定义注释信息：
* **XML中书写"<"、"&"等，可能会出现冲突，导致报错，因此可以用如下热熟字符代替。**
  ![image]()
* XML中可以写一个叫CDATA的数据区：，里面的内容可以随便写。

**XML的作用和应用场景**

* 本质是一种数据格式，可以存储复杂的数据结构和数据关系。
* **应用场景**：经常用来作为系统的配置文件；或者作为一种特殊的数据结构，在网络中进行传输。

**案例**

```
xml version="1.0" encoding="utf-8" ?

<users>
    <user>
        <name>张全蛋name>
        <age>32age>
        <gender>男gender>
        <hobby>炸机hobby>
        <sql>
                select * from tb_student where age &gt;=18 &amp;&amp; age &lt;= 35
        sql>
    user>
    <user>
        <name>何广智name>
        <age>28age>
        <gender>男gender>
        <hobby>脱口秀hobby>
        
            select * from tb_student where age >=18 &amp;&amp; age <= 35
        
    user>
users>
```

---

**解析XML文件**

* 使用程序读取XML文件中的数据
* **注意：程序员并不需要自己写原始的IO流代码来解析XML，难度较大，也相当繁琐。**
* 其实，有很多开源的，好用的解析XML的框架，最知名的是：dom4j(第三方研发的)

**使用Dom4J解析出XML文件**

1. 需求：使用Dom4J把一个XML文件的数据进行解析
2. 分析：
3. 下载Dom4J框架，官网下载。

* 地址：[https://dom4j.github.io/](https://github.com)

2. 在项目中创建一个文件夹：lib
3. 将dom4j-2.1.3.jar文件复制到lib文件夹
4. 在jar文件上点右键，选择Add as Library->点击OK。
5. 在类中导包使用

**DOM4J解析XML文件的思想：文档对象模型**
![image]()

**Dom4j解析XML-得到Document对象**

* SAXReader：Dom4j提供的解析器，可以认为是代表整个Dom4j框架
  ![image]()
* Document
  ![image]()
* **Element提供的方法**
  ![image]()

**案例**
XML文件，Contact.xml：

潘金莲
女
panpan@itcast.cn

武松
男
wusong@itcast.cn

武大郎
男
kuzhu@itcast.cn

武大郎

测试：

```
// 目标：解析XML文件，使用Dom4j框架
public class Dom4jTest01 {
    public static void main(String[] args) throws Exception {
        //1. 创建SAXReader解析器对象
        SAXReader saxReader = new SAXReader();

        //2. 把xml文件读成一个Document文档对象。
        Document doc = saxReader.read("day11-special-file-log-code\\src\\Contact.xml");

        // 3. 文档对象中包含了XML的全部数据，提供了方法获取数据
        Element rootElement = doc.getRootElement();
        System.out.println(rootElement.getName());

        //4. 提取子元素对象
//        List soneles = rootElement.elements();
        List soneles = rootElement.elements("contact");

        for (Element sonele : soneles) {
            System.out.println(sonele.getName());
        }

        // 指定获取单个子元素对象
        Element userEle = rootElement.element("user");
        System.out.println(userEle.elementText("name"));
        Element contactEle = rootElement.element("contact");//默认取第一个contact
        System.out.println(contactEle.elementText("name"));

        // 5. 提取子元素的属性对象
        Attribute idAttr = contactEle.attribute("id");
        System.out.println(idAttr.getName());
        System.out.println(idAttr.getValue());

        //直接拿属性值
        System.out.println(contactEle.attributeValue("id"));

        //6. 文本值
        // 通过父元素拿到子元素文本值
        System.out.println(contactEle.elementText("name"));
        System.out.println(contactEle.elementTextTrim("name"));//去除内容两边的空
    }
}

输出结果：
contactList
contact
contact
contact
武大郎
潘金莲
id
1
1
潘金莲
潘金莲
```

---

**案例：XML解析案例**

* 需求：利用Dom4j框架，将contact.xml文件中的联系人数据解析出来，封装成list集合，并遍历输出。

```
Contacts.xml文件
xml version=<span class="hljs-string""1.0" encoding="UTF-8"?>

    "1" vip="true">
        张无忌
        男
        wuji@itcast.cn
    
    "2" vip="false">
        小昭
        女
        xiaozhao@itcast.cn
    
    "3" vip="false">
        灭绝师太
        女
        miejue@itcast.cn
    
 

Contact类：
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Contact {
    private String name;
    private int id;
    private String email;
    private char gender;
}

测试代码：
//目标：解析XML文件，使用dom4框架
public class Dom4JTest02 {
    public static void main(String[] args) throws Exception {
        //1. 创建一个saxReader对象
        SAXReader saxReader = new SAXReader();

        //2. 把xml文件读成一个document对象
        Document doc = saxReader.read("day11-special-file-log-code\\src\\Contacts.xml");

        //3. 文档中包含了XML的全部数据，提供了方法获取数据
        Element rootElement = doc.getRootElement();

        //4. 准备一个联系人集合存储联系人对象
        List names = new ArrayList<>();

        //5. 提取全部全部一级联系人对象
        List sonEles = rootElement.elements("contact");

        //6. 遍历每个元素对象
        for (Element sonEle : sonEles) {
            //7.每个元素是一个联系人对象，创建联系人对象，封装数据。
            Contact contact = new Contact();
            // 注入数据
            contact.setId(Integer.valueOf(sonEle.attributeValue("id")));
            contact.setName(sonEle.elementTextTrim("name"));
            contact.setEmail(sonEle.elementTextTrim("email"));
            contact.setGender(sonEle.elementTextTrim("gender").charAt(0));

            //8. 把联系人对象存入集合中
            names.add(contact);
        }
        System.out.println(names);
    }
}
```

---

**如何使用程序吧数据写出到xml文件中去？**
不建议使用都dom4j做，**推荐直接把程序里的数据拼接成xml格式，然后用IO流写出去。**

**案例**

```
//目标：写一个xml的数据出去
public class Dom4JTest03 {
    public static void main(String[] args) throws Exception {
        StringBuilder sb = new StringBuilder();
        sb.append("xml version=\"1.0\" encoding=\"UTF-8\"?\r\n");
        sb.append("\r\n");
        sb.append("").append("张无忌").append("\r\n");
        sb.append("").append("男").append("\r\n");
        sb.append("").append("wuji@itcast.cn").append("\r\n");
        sb.append("\r\n");

        PrintStream out = new PrintStream("day11-special-file-log-code\\src\\Contacts1.xml");
        out.println(sb);
        
        out.close();
    }
}
```

---

**约束XML文件的书写**

* 就是限制XML文件只能按照某种格式进行书写。

**约束文档**

* 专门用来限制XML书写格式的文档，比如：限制标签、属性应该怎么写。

**约束文档的分类**

* DTD文档
* Schema文档

**案例**

* XML文档约束-DTD的使用(了解)
  需求：利用DTD约束文档，约束一个XML文件的编写。
  1. 编写DTD约束文档，后缀必须是.dtd
     ![image]()
  2. 在需要编写的XML文件中导入该DTD约束文档
  3. 然后XML文件，就必须按照DTD约束文档指定的格式进行编写，否则报错。

注意：DTD**可以约束XML文件的编写，不能约束具体的数据类型。**

* XML文档约束-schema的使用(了解)
  需求：利用schema文档约束，约束一个xml文件的编写。
  ![image]()
  1. 编写schema约束文档，后缀必须是.xsd，具体的形式到代码中查看。
  2. 在需要编写的xml文档中导入该schema约束文档。
  3. **按照约束内容编写xml文件的标签**。

---

## 日志技术

**什么是日志？**

* 希望系统能记住某些数据是被谁操作的，比如被删除了。
* 想分析用户浏览系统的具体情况，以便挖掘用户的具体喜好。
* 当系统在开发中或者上线后出现了bug，崩溃了，该通过什么去分析、定位问题。

**目前记录日志的方法**
![image]()
**输出语句的弊端**

* 日志会展示在控制台
* 不能更方便的将日志记录到其他的位置(文件，数据库)
* 想取消日志，需要修改源代码才可以完成

**日志技术**

* 可以将系统执行的信息，方便的记录到指定的位置(控制台、文件中、数据库中)
* 可以随时以开关的形式控制日志的启停，无需侵入到源代码中去修改。

**日志技术的体系结构**
![image]()

* 日志框架：牛人或者第三方公司已经做好的实现代码，后来者直接可以拿来使用。
* 日志接口：设计日志框架的一套标准，日志框架需要实现这些接口。
  ![image]()
  **注意：**
  1. 因为对Commons Logging接口不满意，有人就搞了SLF4J。因为对log4j的性能不满意，有人就搞了logback。
  2. Logback是基于slf4j的日志规范实现的框架。

Logback日志框架官方网站：[https://repo1.maven.org/maven2/ch/qos/logback/](https://github.com)
slf4j-api日志框架下载地址：[https://repo1.maven.org/maven2/org/slf4j/slf4j-api/](https://github.com)
Logback日志框架有以下几个模块：
![image]()

## **想使用logback日志框架，至少需要在项目中整合如下三个模块：** image

**Logback快速入门**
**需求**：使用logback日志框架，记录系统运行信息。
**实现步骤**

1. 导入logback框架到项目中去。

* slf4j-api:日志接口
* logback-core
* logback-classic

2. 将Logback框架的核心配置文件Logback.xml直接拷贝到src目录下(必须是src下)。
3. 创建Logback框架提供的logger对象，然后用logger对象调用其提供的方法就可以记录系统的日志信息。

```
public static final logger LOGGER = loggerFactory.getLogger("类名");
```

**案例代码**

```
//目标：使用logback记录日志
public class Test {
    //1. 创建一个logback框架的Logger日志独享，来记录日志。
    public static final Logger LOGGER = LoggerFactory.getLogger("Test.class");
    public static void main(String[] args) {
        try{
            LOGGER.info("除法开始了...");
            chu(0,0);
            LOGGER.info("除法成功了...");
        }
        catch (Exception e){
            LOGGER.error("除法执行失败了：" + e.getMessage());
        }
    }

    public static void chu(int a , int b){
        LOGGER.debug("参数a：" + a);
        LOGGER.debug("参数b：" + b);
        int c = a / b;
        LOGGER.info("结果c：" + c);
    }
}
```

**logback.xml文件内容如下**

```
xml version="1.0" encoding="UTF-8"?
<configuration debug="false">

    
    <property name="LOG_HOME" value="D:/log" />

    
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%npattern>
        encoder>
    appender>

    
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            
            <FileNamePattern>${LOG_HOME}/TestWeb.log.%d{yyyy-MM-dd}.logFileNamePattern>
            
            <MaxHistory>30MaxHistory>
        rollingPolicy>
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%npattern>
        encoder>
        
        <triggeringPolicy class="ch.qos.logback.core.rolling.SizeBasedTriggeringPolicy">
            <MaxFileSize>10MBMaxFileSize>
        triggeringPolicy>
    appender>

    
    <logger name="org.hibernate.type.descriptor.sql.BasicBinder" level="TRACE" />
    <logger name="org.hibernate.type.descriptor.sql.BasicExtractor" level="DEBUG" />
    <logger name="org.hibernate.SQL" level="DEBUG" />
    <logger name="org.hibernate.engine.QueryParameters" level="DEBUG" />
    <logger name="org.hibernate.engine.query.HQLQueryPlan" level="DEBUG" />

    
    <logger name="com.apache.ibatis" level="TRACE"/>
    <logger name="java.sql.Connection" level="DEBUG"/>
    <logger name="java.sql.Statement" level="DEBUG"/>
    <logger name="java.sql.PreparedStatement" level="DEBUG"/>

    
    <root level="DEBUG">
        <appender-ref ref="STDOUT" />
        <appender-ref ref="FILE"/>
    root>
configuration>
```

---

**核心配置文件Logback.xml**

* 对logback日志框架进行控制的。

**日志的输出位置、输出格式的设置**

* 通常可以设置2个输出日志的位置：一个是控制台、一个是系统文件中

```
<appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">

<appender name="FILE" class="ch.gos.logback.core.rolling.RollingFileAppender">
```

**开始日志(ALL)， 取消日志(OFF)**

```
<root level="DEBUG">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE"/>
    root>
```

**什么是日志级别？**

* 日志级别指的是日志信息的类型，日志都会分级别，常见的日志级别如下(优先级依次升高)：
  ![image]()
  **为什么要学习日志级别？**

```
<root level="DEBUG">
        <appender-ref ref="STDOUT" />
        <appender-ref ref="FILE"/>
    root>
```

* 只有日志级别是**大于等于核心配置文件配置的日志级别**，才会被记录，否则不记录。
