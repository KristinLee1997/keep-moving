# 配置Mybatis

### 背景：

只配置了Mybatis，没有配置Spring。 

然而Mybatis期望mapper.java和mapper.xml是在同一目录。

但是我期望的是java文件放在src/main目录下，XML文件放在resources/。

 所以进行以下的配置，通过maven插件编译时扫描将不在同一目录的java文件和xml文件。

### 1.在pom.xml中添加依赖

```text
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>

<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
</dependency>
```

###  2.添加conf.properties,数据库的配置信息 

```text
datasource.url=jdbc:mysql://localhost:3306/usercenter?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8&useSSL=true
datasource.username=root
datasource.password=121212
datasource.driver-class-name=com.mysql.cj.jdbc.Driver

#Mybatis Generator configuration
#dao类和实体类的位置
mybatis.project =src/main/java
#mapper文件的位置
mybatis.resources=src/main/resources
```

###  3.添加mybatis-config.xml

```text
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <properties resource="conf.properties"/>
    <typeAliases>
        <typeAlias alias="Integer" type="java.lang.Integer"/>
        <typeAlias alias="Long" type="java.lang.Long"/>
        <typeAlias alias="HashMap" type="java.util.HashMap"/>
        <typeAlias alias="LinkedHashMap" type="java.util.LinkedHashMap"/>
        <typeAlias alias="ArrayList" type="java.util.ArrayList"/>
        <typeAlias alias="LinkedList" type="java.util.LinkedList"/>
        <typeAlias alias="Hello" type="com.aries.user.gaea.model.Hello"/>
        <typeAlias alias="HelloExample" type="com.aries.user.gaea.model.HelloExample"/>
    </typeAliases>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <!-- 配置数据库连接信息 -->
            <dataSource type="POOLED">
                <property name="driver" value="${datasource.driver-class-name}"/>
                <property name="url" value="${datasource.url}"/>
                <property name="username" value="${datasource.username}"/>
                <property name="password" value="${datasource.password}"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <package name="com.aries.user.gaea.mapper"/>
    </mappers>

</configuration>
```

###  4.在pom.xml中添加maven-resource-plugin插件扫描mapper.xml

```text
<plugin>
    <artifactId>maven-resources-plugin</artifactId>
    <version>2.5</version>
    <executions>
        <execution>
            <id>copy-xmls</id>
            <phase>process-sources</phase>
            <goals>
                <goal>copy-resources</goal>
            </goals>
            <configuration>
                <outputDirectory>${basedir}/target/classes/com/aries/user/gaea/mapper</outputDirectory>
                <resources>
                    <resource>
                        <directory>${basedir}/src/main/resources/mapper</directory>
                        <includes>
                            <include>**/*Mapper.xml</include>
                        </includes>
                    </resource>
                </resources>
            </configuration>
        </execution>
    </executions>
</plugin>
```

### 5.勾选idea配置，项目编译时跑一遍maven插件 

![](../.gitbook/assets/image%20%285%29.png)

















































































