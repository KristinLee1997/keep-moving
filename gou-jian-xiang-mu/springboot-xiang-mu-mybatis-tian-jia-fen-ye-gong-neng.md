# Springboot项目Mybatis添加分页功能

1.项目已配置好Springboot和Mybatis

2.在pom中导入以下依赖

```text
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.2.10</version>
</dependency>
```

3.使用方法    

```text
PageHelper.startPage(1, 5);
List<Question> questionList = questionMapper.selectByExample(new QuestionExample());
System.out.println(JSON.toJSONString(questionList));
```

