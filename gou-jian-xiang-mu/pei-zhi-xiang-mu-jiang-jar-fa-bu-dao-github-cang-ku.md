# 配置项目，将jar发布到github仓库

在pom文件中添加以下依赖

```text
<build>
    <finalName>项目名</finalName><!-- 改成自己的项目名 -->
    <plugins>
        <plugin>
            <artifactId>maven-deploy-plugin</artifactId>
            <version>2.8.2</version>
            <configuration>
                <!--<packaging>jar</packaging>-->
                <altDeploymentRepository>  <!-- deploy后在对应的本地target目录下 会有mvn-repo子文件夹 -->
                    internal.repo::default::file://${project.build.directory}/仓库名
                </altDeploymentRepository>
            </configuration>
        </plugin>

        <plugin>
            <groupId>com.github.github</groupId>
            <artifactId>site-maven-plugin</artifactId>
            <version>0.12</version>
            <configuration>
                <message>Maven artifacts for ${project.version}</message>
                <noJekyll>true</noJekyll>
                <outputDirectory>${project.build.directory}/mvn-repo</outputDirectory>
                <branch>refs/heads/master</branch>
                <merge>true</merge>
                <includes>
                    <include>**/*</include>
                </includes>
                <repositoryName>github仓库名</repositoryName> <!-- 对应github上创建的仓库名称 name -->
                <repositoryOwner>github账号</repositoryOwner> <!-- 你的用户名 , github 仓库所有者 -->
            </configuration>
            <executions>
                <execution>
                    <goals>
                        <goal>site</goal>
                    </goals>
                    <phase>deploy</phase>
                </execution>
            </executions>
        </plugin>

        <plugin>
            <artifactId>maven-source-plugin</artifactId>
            <version>3.0.1</version>
            <configuration>
                <attach>true</attach>
            </configuration>
            <executions>
                <execution>
                    <phase>compile</phase>
                    <goals>
                        <goal>jar</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>

        <plugin>
            <artifactId>maven-javadoc-plugin</artifactId>
            <version>3.1.0</version>
            <executions>
                <execution>
                    <id>attach-javadocs</id>
                    <phase>deploy</phase>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

