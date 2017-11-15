# maven release

---
## 初始阶段
1. 注册一个JIRA账号：https://issues.sonatype.org/secure/Signup!default.jspa
2. 创建一个新工程的单：https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134
只有当这个jira单的状态我resolved时，才可以提交jar包

## 审查要求

1. 提供javadoc和source
2. 使用gpg或者pgp对文件进行签名
3.  pom.xml文件
4. 正确的坐标：groupId,artifactId,version
```
    <groupId>com.github.fartherp</groupId>
    <artifactId>framework</artifactId>
    <version>1.0-SNAPSHOT</version>
```
5. projectName,description,url等
```
    <name>framework</name>
    <url>https://github.com/fartherp/framework</url>
    <description>framework</description>
```
6.  license 信息
```
    <licenses>
        <license>
            <name>The Apache Software License, Version 2.0</name>
            <url>http://www.apache.org/licenses/LICENSE-2.0.txt</url>
            <distribution>repo</distribution>
        </license>
    </licenses>
```
7.  开发者信息
```
    <developers>
        <developer>
            <id>ck</id>
            <name>ck</name>
            <email>yuqiang.cui@gmail.com</email>
        </developer>
        <developer>
            <id>wyzhangjie</id>
            <name>wyzhangjie</name>
        </developer>
    </developers>
```
8. SCM信息
```
    <scm>
        <connection>scm:git:git@github.com:fartherp/framework.git</connection>
        <developerConnection>scm:git:git@github.com:fartherp/framework.git</developerConnection>
        <url>https://github.com/fartherp/framework</url>
        <tag>HEAD</tag>
    </scm>
```
## 部署（maven）
1. 分布管理和认证: pom.xml
```
    <distributionManagement>
        <repository>
            <id>oss</id>
            <name>Nexus Release Repository</name>
            <url>https://oss.sonatype.org/service/local/staging/deploy/maven2/</url>
        </repository>
        <snapshotRepository>
            <id>oss</id>
            <name>Nexus Snapshot Repository</name>
            <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
        </snapshotRepository>
    </distributionManagement>
```
2. settings.xml配置jira的账号和密码**(和上面的id一样)**
```
  <servers>
    <server>
      <id>oss</id>
      <username>your-jira-id</username>
      <password>your-jira-pwd</password>
    </server>
  </servers>
```
3. 配置生成javadoc和sources包的插件
```
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-source-plugin</artifactId>
        <version>2.2.1</version>
        <executions>
            <execution>
                <id>attach-sources</id>
                <phase>package</phase>
                <goals>
                    <goal>jar-no-fork</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-javadoc-plugin</artifactId>
        <version>2.9.1</version>
        <executions>
            <execution>
                <id>attach-javadocs</id>
                <goals>
                    <goal>jar</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
```
4. GPG自动签名的插件
```
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-gpg-plugin</artifactId>
        <version>1.6</version>
        <executions>
            <execution>
                <id>sign-artifacts</id>
                <phase>verify</phase>
                <goals>
                    <goal>sign</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
```
maven-settings.xml中配置gpg的签名: （需要先用gpg来生成）
```
    <profile>
      <id>oss</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <properties>
        <gpg.executable>gpg2</gpg.executable>
        <gpg.passphrase>qwertyuiop</gpg.passphrase>
      </properties>
    </profile>
```
5. 使用Profile
```
应该javadoc和source的jar包生成也需要使用gpg来签名，所以很浪费时间，而且这些执行通常都独立于标准构建流程，所以把他们移动到一个profile.
 <profiles>
   <profile> 
    <id>release</id>
    <build>
        <plugins>
            <plugin>
               <groupId>org.sonatype.plugins</groupId>
               <artifactId>nexus-staging-maven-plugin</artifactId>
               <version>1.6.3</version>
               <extensions>true</extensions>
               <configuration>
                 <serverId>ossrh</serverId>
                 <nexusUrl>https://oss.sonatype.org/</nexusUrl>
                 <autoReleaseAfterClose>true</autoReleaseAfterClose>
               </configuration>
             </plugin>
             <plugin>
                 <groupId>org.apache.maven.plugins</groupId>
                 <artifactId>maven-release-plugin</artifactId>
                 <version>2.5</version>
                 <configuration>
                   <autoVersionSubmodules>true</autoVersionSubmodules>
                   <useReleaseProfile>false</useReleaseProfile>
                   <releaseProfiles>release</releaseProfiles>
                   <goals>deploy</goals>
                 </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.0</version>
                <configuration>
                    <source>1.6</source>
                    <target>1.6</target>
                </configuration>
            </plugin>
            <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-gpg-plugin</artifactId>
               <version>1.5</version>
               <executions>
                 <execution>
                   <id>sign-artifacts</id>
                   <phase>verify</phase>
                   <goals>
                     <goal>sign</goal>
                   </goals>
                 </execution>
               </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-source-plugin</artifactId>
                <version>2.2.1</version>
                <executions>
                    <execution>
                        <id>attach-sources</id>
                        <goals>
                            <goal>jar-no-fork</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-javadoc-plugin</artifactId>
                <version>2.9</version>
                <executions>
                    <execution>
                        <id>attach-javadocs</id>
                        <goals>
                            <goal>jar</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
         </plugins>
    </build>
  </profile>
</profiles>
```
6. 提交snapshot版本
```
mvn clean deploy
```
7. 发布release版本
```
1. 修改version
mvn versions:set -DnewVersion=1.0.0
2. 执行 
mvn clean deploy -P release
```
8. 回滚版本
```
mvn versions:revert
```
9. 提交版本
```
mvn versions:commit
```

