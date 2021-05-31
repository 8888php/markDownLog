1:配制bean.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--把对象创建交给spring来管理-->
    <bean id="userService" class="org.rain.demo.service.impl.UserServiceImpl" lazy-init="false"></bean>
    <bean id="userDao" class="org.rain.demo.dao.impl.UserDaoImpl" lazy-init="false"></bean>
</beans>
```

2: 获取bean.xml

```java
//获取核心容器对象
ApplicationContext ioc = new ClassPathXmlApplicationContext("bean.xml");
//获取bean对象
IUserServic userService = ioc.getBean("userService", IUserServic.class);
IUserDao userDao = ioc.getBean("userDao", IUserDao.class);
```

3: ApplicationContext 3个常用实现类

```java
/**
 * ApplicationContext 3个常用实现类
 *      ClassPathXmlApplicationContext 加载类路径下面的配制文件,要求必须在类路径下面的
 *      FileSystemXmlApplicationContext 加载磁盘任意路径下的配制文件,要求必须有文件权限
 *      AnnotationConfigApplicationContext 读取注解创建的容器
 */
```

4: 两大核心容器接口的对比

```java
/**
 *    核心容器两个接口引发的问题
 *   ApplicationContext
 *     它构建核心容器时,创建对象立即加载, 单例对象适用
 *
 *   BeanFactory
 *     创建时采用延迟加载,什么时间获取,什么时间加载, 多例对象适用
 */
```

5:xml中bean创建的3种方式

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

<!--    把对象的创建交给spring来管理-->
    <!--    spring对bean的管理细节
                1.创建bean的三种方式
                2.bean对象的作用范围
                3.bean对象的生命周期
    -->
    <!--    创建bean的三种方式-->
    <!--    第一种方式：使用默认构造函数创建
        在spring的配置文件中使用bean标签，配以id和class属性之后，且没有其他属性和标签时。
        采用的就是默认构造函数创建对象，此时如果没有默认构造函数，则对象无法创建
        <bean id="accountService" class="com.ithema.service.impl.AccountServiceImpl"></bean>
    -->

```xml
<!--    第二种方式：使用普通工厂中的方法创建对象（使用某个类中的方法创建对象，并存入spring容器）
<bean id="instanceFactory" class="com.ithema.factory.InstanceFactory"></bean>
<bean id="accountService" factory-bean="instanceFactory" factory-method="getAccountService"></bean>
-->
<!-- 第三种方式：使用工厂中的静态方法创建对象（使用某个类中的静态方法创建对象，并存入spring容器）
    <bean id="accountService" class="com.ithema.factory.StaticFactory" factory-method="getAccountService"></bean>
    -->

<!--    bean的作用范围调整
        bean标签的scope属性：
            作用：用于指定bean的作用范围
            取值：  常用的单例的和多例的
                singleton：单例的（默认值）
                prototype: 多例的
                request： 作用于web应用的请求范围
                session： 作用于web应用的会话范围
                global-session：作用于集群环境的会话范围（全局会话范围），当不是集群环境时，就是session
        <bean id="accountService" class="com.ithema.service.impl.AccountServiceImpl" scope="singleton"></bean>

-->
<!--    bean的生命周期
            单例对象：
                出生：当容器创建时对象出生
                活着：当容器还在，对象一直活着
                死亡：容器销毁，对象消亡
                总结：单例对象的生命周期和容器相同
            多例对象：
                出生：当我们使用对象时spring框架为我们创建
                活着：对象只要是在使用过程中就一直活着。
                死亡：当对象长时间不用，且没有别的对象引用时，由java的垃圾回收机制回收
-->
<bean id="accountService" class="com.ithema.service.impl.AccountServiceImpl" scope="singleton"></bean>
</beans>
```

6: 