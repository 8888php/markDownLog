1: 获取yml的值到bean类上

```java
@Component //注册组件,
@ConfigurationProperties(prefix = "person") //告诉springboot,本类中所有属性和配制文件的属性绑定 prefix = "person",从 person中找.默认是加载全局的.properties
```

2: 

```java
@Component
@Value("${person.last-name}")
```



3: 

```java
@PropertySource(value = {"classpath:abc.properties"})
@Component
@ConfigurationProperties(prefix = "person")
这个可以加载其它的配制文件.properties
```



4:

@ImportResource(locations = {"classpath:web.xml"}) 

导入spring配制文件

5:

```java
//表示当前类是配制类
@Configuration
public class myconfig {

    @Bean
    public HelloController helloController() {
        return new HelloController();
    }
}
```



6: