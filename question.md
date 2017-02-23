# 常见问题

## 如何排除非表中字段？

> 三种方式选择一种即可！

- 使用 transient 修饰

  ```java
  private transient String noColumn;
  ```

- 使用 static 修饰

  ```java
  private static String noColumn;
  ```

- 使用 TableField 注解

  ```java
  @TableField(exist=false)
  private String noColumn;
  ```

## 出现异常`Invalid bound statement (not found)`的解决方法

> 不要怀疑，正视自己，这个异常肯定是你插入的姿势不对……

- 检查命名空间是否正常？ 检查包扫描路径是否正常？如果扫描不到，MP无法进行预注入

- 检查是否指定了主键？如未指定，则会导致 `selectById` 相关 ID 无法操作，请用注解 `@TableId` 注解表 ID 主键

- 对于`IDEA`系列编辑器，XML 文件是不能放在 java 文件夹中的，IDEA 默认不会编译源码文件夹中的 XML 文件，如果非要放在 java 文件夹中，可以参照一下方式解决：

  - 将配置文件放在 resource 文件夹中
  - 对于 Maven 项目，可指定 POM 文件的 resource

  ```xml
  <build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
            </includes>
        </resource>
        <!--指定资源的位置-->
        <resource>
            <directory>src/main/resources</directory>
        </resource>
    </resources>
  </build>
  ```

