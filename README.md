# git bisect实战

这是一个用来重现[Maven的MNG-6700](https://issues.apache.org/jira/browse/MNG-6700)的实战项目。将本项目clone到本地，然后分别使用Maven 3.6.0和3.6.1运行`mvn compile`，你会发现：

## Maven 3.6.0

```
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
```

## Maven 3.6.1

```
[ERROR] /Users/zhb/Projects/maven-issue-reproduction/./common/Os.kt: (3, 12) Redeclaration: Os
[ERROR] /Users/zhb/Projects/maven-issue-reproduction/common/Os.kt: (3, 12) Redeclaration: Os
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  3.087 s
[INFO] Finished at: 2019-10-18T14:11:42+08:00
[INFO] ------------------------------------------------------------------------
```

这意味着，在[Maven](https://github.com/apache/maven)的3.6.0和3.6.1之间有某个提交引入了一个bug，导致了`MNG-6700`。请运用`git bisect`大法，找到引入bug的commit和责任人。
