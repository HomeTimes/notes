# 开启整合的奇妙之旅

### 1.导包

```
<?xml version="1.0" encoding="UTF-8"?>
<!--
  Licensed to the Apache Software Foundation (ASF) under one
  or more contributor license agreements.  See the NOTICE file
  distributed with this work for additional information
  regarding copyright ownership.  The ASF licenses this file
  to you under the Apache License, Version 2.0 (the
  "License"); you may not use this file except in compliance
  with the License.  You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing,
  software distributed under the License is distributed on an
  "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
  KIND, either express or implied.  See the License for the
  specific language governing permissions and limitations
  under the License.
-->
<!-- $Id: pom.xml 642118 2008-03-28 08:04:16Z reinhard $ -->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">

  <modelVersion>4.0.0</modelVersion>
  <packaging>war</packaging>

  <name>ssm</name>
  <groupId>hand</groupId>
  <artifactId>ssm</artifactId>
  <version>1.0-SNAPSHOT</version>

  <dependencies>
<!--    spring -->
      <dependency>
          <groupId>org.aspectj</groupId>
          <artifactId>aspectjweaver</artifactId>
          <version>1.9.6</version>
      </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>5.3.6</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.3.6</version>
    </dependency>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-web</artifactId>
          <version>5.3.6</version>
      </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.3.6</version>
    </dependency>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-jdbc</artifactId>
          <version>5.2.9.RELEASE</version>
      </dependency>
      
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-tx</artifactId>
          <version>5.2.12.RELEASE</version>
      </dependency>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-test</artifactId>
          <version>5.3.6</version>
      </dependency>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-aspects</artifactId>
          <version>5.3.1</version>
      </dependency>
      <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>servlet-api</artifactId>
          <version>2.5</version>
      </dependency>
<!--     jsp api -->
      <dependency>
          <groupId>javax.servlet.jsp</groupId>
          <artifactId>jsp-api</artifactId>
          <version>2.1</version>
      </dependency>
<!--      jstl表达式-->
      <dependency>
          <groupId>javax.servlet.jsp.jstl</groupId>
          <artifactId>jstl-api</artifactId>
          <version>1.2</version>
      </dependency>
<!--      mybatis-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.4.6</version>
    </dependency>
<!--      整合spring 和mybatis-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>2.0.4</version>
    </dependency>
<!-- 连接池-->
    <dependency>
      <groupId>com.mchange</groupId>
      <artifactId>c3p0</artifactId>
      <version>0.9.5.2</version>
    </dependency>
<!--      数据库连接驱动-->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.18</version>
    </dependency>
<!-- 单元测试-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13</version>
        <scope>compile</scope>
    </dependency>

<!--json-->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.12.3</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-core</artifactId>
      <version>2.12.3</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-annotations</artifactId>
      <version>2.12.3</version>
    </dependency>
  </dependencies>
  <build>
    <plugins>
        <plugin>
                      <groupId>org.apache.tomcat.maven</groupId>
                       <artifactId>tomcat7-maven-plugin</artifactId>
                       <configuration>
                          <path>/</path>
                          <port>8080</port>
                       </configuration>
        </plugin>
    </plugins>
  </build>
</project>
```

### 2.建立好三层架构的package

### 3.整合spring

###### 测试service层，看能不能整合成功

```
@Service("bookImpl")
public class bookImpl implements bookSdao {
  public void test() {
        System.out.println("ssssssss");
    }
}
```

###### 编写spring的配置文件：类路径下

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans.xsd
   http://www.springframework.org/schema/context
   http://www.springframework.org/schema/context/spring-context.xsd
   http://www.springframework.org/schema/aop
   http://www.springframework.org/schema/aop/spring-aop.xsd
   http://www.springframework.org/schema/tx
   http://www.springframework.org/schema/tx/spring-tx.xsd">
   
<!--    开始注解扫描,希望处理service和dao层，不处理controller层-->
    <context:component-scan base-package="cn">
<!--        配置那些注解不扫描-->
        <context:exclude-filter type="annotation" 						     expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
    
</beans>
```

###### 编写测试test

```
public void testSevice(){
     ApplicationContext  ac=new ClassPathXmlApplicationContext("classpath:application.xml");
     bookImpl bookImpl =(bookImpl) ac.getBean("bookImpl");
     bookImpl.test();

 }
```

### 4.整合springmvc

###### controller文件

```
@RestController
@RequestMapping(value = "/demo1")
@CrossOrigin
public class controller {
    @RequestMapping("/find")
    public  String find(){
        System.out.println("点击了");
        return  "sucessul";
    }
}
```

###### web文件

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.4"
         xmlns="http://java.sun.com/xml/ns/j2ee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">
  <!--       配置情断控制器-->
  <!--  第一步-->

  <servlet>
    <servlet-name>DispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
<!--    加载配置mvc的文件-->
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:springMVC.xml</param-value>
    </init-param>
<!--    启动该服务器时，就创建该servlet-->
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>DispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
<!--  第一步-->

<!--  配置解决中文乱码的过滤器-->
<!--  第二步-->
  <filter>
    <filter-name>CharacterEncodingFilter</filter-name>

    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
<!--      配置编码-->
      <!--    如果点进CharacterEncodingFilter里会有encoding的参数-->
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
  </filter>
   <filter-mapping>
     <filter-name>CharacterEncodingFilter</filter-name>
     <url-pattern>/*</url-pattern>
   </filter-mapping>
  <!--  第二步-->


</web-app>
        
```

###### 启动测试

默认会启动index.jsp

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<a href="/demo1/find">点击一下</a>
</body>
</html>
```

### 5问题

我们没有将spring和springmvc相关联起来，

希望能在tomcat服务器启动的时候加载spring配置文件，

### 6.整合spring和springmvc在一起

###### servletContent域对象

1.服务器一启动的时候就会创建servletContent域对象，关闭才会销毁 

2.一类监听器，监听servletContent域对象的创建和销毁

3.可以利用监听器去加载spring的配置文件,创建web版本工厂，存储servletContext对象

 4.spring-web包提供了servletContent的监听器

在web.xml里添加

```
<!--  配置加载spring的配置文件的监听器-->
<!--  ctr+n 查找ContextLoaderListener类-->
<!--  默认加载web-inf下的配置文件-->
 <listener>
   <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
 </listener>
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:application.xml</param-value>
  </context-param>
```

controller测试

```
@RestController
@RequestMapping(value = "/demo1")
@CrossOrigin
public class controller {
    @Autowired
    private  bookSdao bookSdao;
    @RequestMapping("/find")
    public  String find(){
        System.out.println("点击了");
        return  "sucessul";
    }

    @RequestMapping("/finden")
    public  void finden(){
        bookSdao.test();
    }
}

```

### 7.没有整合mybatis

不过没有和spring和springmvc联系在一起

###### dao层：没有映射文件的情况

```
public interface bookDao {
   @Select("select * from book where id = #{id}")
   public book findID(int id);
//   public void  updatebook ( book bookname);
}
```

类路径下

###### sqlMaperConfig.xml

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!-- 这里写配置内容 -->
    <environments default="mysql">
        <environment id="mysql">
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="password" value="123456"/>
                <property name="username" value="root"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <!--    假如有配置映射文件-->
<!--        <mapper resource="cn/xxx/xxx.xml"></mapper>-->
<!--        接口的全路径地址-->
<!--        <mapper class="cn.dao.bookDao"></mapper>-->
<!--        为了以后能偷懒，少写多个接口的全路径，推荐写-->
<!--        -->
        <package name="cn.dao"/>
    </mappers>
</configuration>
```

###### test

```
package cn.test;

import cn.dao.bookDao;
import cn.domain.book;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.InputStream;

public class testMapping {
    @Test
  public void run() throws Exception {
//       加载配置文件
        InputStream in = Resources.getResourceAsStream("SqlMaperConfig.xml");
//        创建SqlSessionFactory对象
        SqlSessionFactory build = new SqlSessionFactoryBuilder().build(in);
//        获取sqlSession对象
        SqlSession sqlSession = build.openSession();
//        获取接口的代理对象
        bookDao mapper = sqlSession.getMapper(bookDao.class);
//        调用方法
        book bookid = mapper.findID(1);
//        关闭资源
        sqlSession.close();
        in.close();
        System.out.println(bookid);
        //        注意：增删改，要提交事务 sqlSession.commit();
    }
}
```

#### 整合一起

###### application.xml



```xml
<!--    第二步-->
<!--   spring整合mybatis-->
<!--    1    111111111-->
<!--   配置连接池 -->
    <bean id="dataSource"  class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="com.mysql.cj.jdbc.Driver"></property>
        <property name="user" value="root"></property>
        <property name="password" value="123456"></property>
        <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC"></property>
    </bean>
<!--    配置sqlSessionFactory工厂-->
    <bean id="SqlSessionFactory"  class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource"  ref="dataSource"></property>
<!--        maper映射文件的domain的别名处理-->
        <property name="typeAliasesPackage" value="cn.domain"></property>
    </bean>
<!--    配置dao接口所在的包：告诉sqlSessionFactory工厂接口在哪，生产代理对象，存在IOC中-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
    <!--   记住：在cn.dao包加注解@Repository-->
        <property name="basePackage" value="cn.dao"></property>
    </bean>
```

记住：在cn.dao包加注解@Repository

###### test

controller层调用sevice层，sevice层调用dao层

