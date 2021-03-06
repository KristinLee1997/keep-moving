# Mybatis-Generator插件使用方式

## 1.在pom.xml中添加依赖

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

##  2.添加conf.properties 

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

## 3.配置generatorConfig.xml文件

```text
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <properties resource="conf.properties"/>
    <!-- 数据库驱动:选择你的本地硬盘上面的数据库驱动包，可以选择不写-->
    <classPathEntry
            location="/Users/xxx/.m2/repository/mysql/mysql-connector-java/8.0.15/mysql-connector-java-8.0.15.jar"/>
    <context id="MysqlTables" targetRuntime="MyBatis3">
        <commentGenerator>
            <property name="suppressDate" value="true"/>
            <!-- 是否去除自动生成的注释 true：是 ： false:否 -->
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>

        <!--数据库链接URL，用户名、密码 -->
        <jdbcConnection driverClass="${datasource.driver-class-name}" connectionURL="${datasource.url}"
                        userId="${datasource.username}" password="${datasource.password}">
            <property name="nullCatalogMeansCurrent" value="true"/>
            <!--添加nullCatalogMeansCurrent代表只生成当前数据库中的表，不会生成其他数据库中的同名表-->
        </jdbcConnection>

        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>

        <!-- 生成模型的包名和位置-->
        <javaModelGenerator targetPackage="com.aries.user.gaea.model" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>

        <!-- 生成映射文件的包名和位置-->
        <sqlMapGenerator targetPackage="mapper" targetProject="MAVEN">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>

        <!-- 生成DAO的包名和位置-->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.aries.user.gaea.mapper" targetProject="MAVEN">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>

        <!-- 要生成的表 tableName是数据库中的表名或视图名 domainObjectName是实体类名-->
        <table tableName="hello" domainObjectName="Hello" enableCountByExample="true" enableUpdateByExample="true"
               enableDeleteByExample="true" enableSelectByExample="true" selectByExampleQueryId="true">
            <generatedKey column="id" sqlStatement="MySql" identity="true"/>
        </table>
    </context>
</generatorConfiguration>
```

## 4.在pom.xml中添加mybatis-generator-maven-plugin  ，generatorConfig.xml的路径记得要改成自己的路径

```text
<!-- mybatis generator 自动生成代码插件 -->
<plugin>
    <groupId>org.mybatis.generator</groupId>
    <artifactId>mybatis-generator-maven-plugin</artifactId>
    <version>1.3.2</version>
    <configuration>
        <configurationFile>${basedir}/src/main/resources/mybatis/generatorConfig.xml</configurationFile>
        <overwrite>true</overwrite>
        <verbose>true</verbose>
    </configuration>
</plugin>
```

