1.servlet 配制web.xml

```java
<!--配制servlet-->
<servlet>
    <servlet-name>demo1</servlet-name>
    <servlet-class>com.rain.web.servlet.ServletDemo</servlet-class>
</servlet>
<!--配制mapping关系-->
<servlet-mapping>
    <servlet-name>demo1</servlet-name>
    <url-pattern>/demo1</url-pattern>
</servlet-mapping>
<!--配制servlet-->
<servlet>
    <servlet-name>demo2</servlet-name>
    <servlet-class>com.rain.web.servlet.ServletDemo2</servlet-class>
    <!--load-on-startup配制大于等于0时会被初始化,创建-->
    <load-on-startup>0</load-on-startup>
</servlet>
<!--配制mapping关系-->
<servlet-mapping>
    <servlet-name>demo2</servlet-name>
    <url-pattern>/demo2</url-pattern>
</servlet-mapping>
```

1.1.Servlet 中的init只执行一次,service执行多次



2.第二种使用注解 @WebServlet