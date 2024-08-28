# SpringBoot

## 快捷键

### Ctrl+Alt+F7查找类使用的地方

![image-20231201174258943](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201174258943.png)

### .快速创建一个对象

![image-20231201174415248](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201174415248.png)

### .sout快速输出该对象

### .iter快速遍历数组

### Alt+Insert快速插入方法

![image-20231201174754085](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201174754085.png)

## 引入依赖

![image-20231201103651545](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201103651545.png)

### Lombok

用于编写代码方便

常用注解：

1.类注解@Data：在当前类下自动生成get,set,toString等方法，具体可以编译后在target目录中对应类查看。

2.类注解@NoArgsConstructor：用于在类中生成一个无参数的构造方法。

3.类注解@AllArgsConstructor：用于在类中生成一个全参数的构造方法。

### Spring Web

包含Tomcat，Jetty等插件，用于将程序转发到对应网址。默认使用Tomcat。

如何切换其他插件？

在pom.xml文件中将tomcat移除，并引入新的依赖。

![image-20231201102104512](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201102104512.png)

### Mysql Driver

提供对Mysql数据库的支持。

### MyBatis Framework

提供对数据库操作语言的支持

相关依赖：

方法注解@Select，@Insert，@Update，@Delete：分别对应数据库四种常用sql语句的操作，在后面以字符串形式给出sql语句即可。

![image-20231201102517372](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201102517372.png)

类注解@Repository：使该类标识为数据库访问类。需要在配置文件application.yml中将实体类与Mapper.xml文件进行绑定。

![image-20231201102946300](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201102946300.png)

![image-20231201102957521](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201102957521.png)

同时Mapper接口中方法名字要与Mapper.xml中对应

![image-20231201103127885](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201103127885.png)

namespace声明Mapper所在位置

方法名对应到id

![image-20231201103225511](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201103225511.png)

### Redis

缓存数据库

使用方法：用@Resourse声明一个RedisTemplate

![image-20231201103805851](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201103805851.png)

调用bondValueOps方法+set方法以键值对的方式存入数据
调用bondValueOps方法+get方法用键获得数据

![image-20231201103823072](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201103823072.png)

## 常用5种请求概述

### GET

用于**从服务器获取资源**。GET请求通常是幂等的，即多次发送相同的GET请求会返回相同的结果。GET请求将参数附加在URL的查询字符串中，可以通过URL直接访问。

### POST

用于向服务器提交数据，并在服务器上**创建新资源**。POST请求通常不是幂等的，即多次发送相同的POST请求可能会创建多个资源。POST请求**将参数包含在请求体**中，而不是URL中。

### PUT

用于**向服务器更新或替换资源**。PUT请求需要将完整的资源表示发送到服务器，如果资源已存在，则进行替换；如果资源不存在，则进行创建。PUT请求通常是幂等的，即多次发送相同的PUT请求会产生相同的结果。

### PATCH

用于**部分更新**服务器上的资源。PATCH请求类似于PUT请求，但是只需要将要更新的部分数据发送到服务器，而不是整个资源。PATCH请求也可以是幂等的，但在实践中并不总是这样。

### DELETE

用于**删除**服务器上的资源。DELETE请求用于删除指定的资源，多次发送相同的DELETE请求将产生相同的结果。DELETE请求**不应包含请求体**。

## YML配置文件

![image-20231201172036757](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201172036757.png)

默认是.properties文件可以手动改成.yml文件

.properties文件采用键值对方式书写(a=1)，但是对于同一个父类下的字类要多次书写父类，因此推荐yml。

yml对缩进有极高要求，父类下的子类必须换行加一个Tab缩进，冒号后必须要一个空格(以上)。

### 服务器配置

第一行为服务器开放的端口，第二行则为相对路径，即localhost:8080/myapp

```yaml
server:
  port: 8080
  servlet:
    context-path: /myapp
```

### MyBatis配置

这个作用是将数据库的下划线命名映射到实体类的驼峰命名

比如数据库里的字段是create_time，而实体类里面是createTime没有下面这个就会找不到

```yaml
mybatis:
  configuration:
    map-underscore-to-camel-case: true
```

### Mysql配置

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/big_event
    username: root
    password: 123456
```

### Redis配置

```yaml
spring:
  data:
    redis:
      host: 127.0.0.1
      port: 6379
```

### 不同配置的分隔

使用三个减号将同一个文件里面的不同配置分隔用于切换

```yaml
---
```

下面这个用来给每一个配置分区命名

也可以将配置文件名改为application-pro.yml实现同样效果

```yaml
spring:
  config:
    activate:
      on-profile:
        pro
```

指定要使用的配置分区

```yaml
spring:
  profiles:
    active: pro
```

如果要指定多个同时生效

```yaml
spring:
  profiles:
    active: dev
    group:
      "dev": devServer,devDB,devSelf
```

### 配置文件的读取

使用该类注解可以将配置文件里的person字段读取到实体类上

```yaml
person:
  name: zhangsan
  age: 20
  address:
    - beijing
    - shanghai
```

```java
@ConfigurationProperties(prefix = "person")
```

```java
@Component
@ConfigurationProperties(prefix = "person")
public class Person {

    private String name;
    private int age;
    private String[] address;
}
```

也可以使用@Value将配置文件里面的某一变量映射到指定变量上

需要用${}指定变量名

```java
@Value("${server.port}")
```



## 项目结构

![image-20231201104041227](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201104041227.png)

### config

存放配置类，一般使用@Configuration类注解

### controller

存放Controller类，一般用于各种接口的实现，使用

```
@RestController
@RequestMapping("/user")
```

RequestMapping后面的路径是接口的一级路径

Controller中还有@PostMapping("/login")等方法注解

之后访问就以localhost:8080/user/login访问

### exception

存放全局异常处理器

将对应类增加一个@RestControllerAdvice注解

![image-20231201104537550](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201104537550.png)

`@ExceptionHandler(Exception.class)`，表示它用于处理`Exception`类型的异常。当控制器中的其他方法抛出`Exception`类型的异常时，`handleException`方法会被调用。

### interceptors

存放拦截器，将未登录的用户拦截

其中的类一般使用@Component注解

类实现HandlerInterceptor接口

重写preHandle方法：当请求处理前先处理此方法

编写登录验证逻辑

return true代表拦截器将处理该请求

return false代表拦截器拒绝处理请求

![image-20231201105019146](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201105019146.png)

重写afterCompletion方法，当请求处理后使用此方法

里面释放缓存或者清空线程数据防止内存溢出

![image-20231201105313892](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201105313892.png)

### mapper

存放Mapper接口，里面实现对数据库的操作，通常使用Mapper注解

### pojo

存放实体类（一般用于读写数据的类，例如User），可以添加@Data注解便于编写和使用

### service

存放Service接口，定义对数据库的增删改查方法

#### impl

存放Service接口的实现类ServiceImpl，需要加@Service注解，实现Service接口中定义的所有方法，一般直接调用Mapper的方法并返回。

### utils

存放工具类

## Result返回

作为实体类编写，放在pojo中，目的是使所有请求以同样的格式返回，如果请求成功返回请求得到的数据，失败则返回null附带失败信息。

![image-20231201105915246](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201105915246.png)

## JWT令牌验证

![image-20231201112030599](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201112030599.png)

### 引入包

```java
import com.auth0.jwt.JWT;
import com.auth0.jwt.algorithms.Algorithm;
```

制作成工具类便于使用

![image-20231201113426613](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201113426613.png)

### 创建令牌

```java
JWT.create()
        .withClaim("claims", claims)
        .withExpiresAt(new Date(System.currentTimeMillis() + 1000 * 60 * 60 * 12))
        .sign(Algorithm.HMAC256(KEY));
```

这个会返回一个字符串，即令牌

#### withClaim方法

```java
public Builder withClaim(String name, Map<String, ?> map)
```

Map一般是"id"->用户的id
"username"->用户名
map.put()可以存入

此处不能存入密码因为此处的编码方式是公开的

#### withExpiresAt方法

用于指定令牌过期时间

System.currentTimeMillis()为当前的系统时间

Date中以毫秒为单位，1000为一秒，此处为12小时

#### sign方法

将claims以某种指定加密方法进行签名，此处使用是

```java
import com.auth0.jwt.algorithms.Algorithm;
```

中的HMAC256加密算法，传入一个字符串进行加密，该字符串类似于密码，不能公开。

### 解码令牌

```java
JWT.require(Algorithm.HMAC256(KEY))
        .build()
        .verify(token)
        .getClaim("claims")
        .asMap();
```

#### require方法

指定你使用的加密方法

#### build方法

用于构建JWT验证器

#### verify方法

对传入的token进行验证，该token应该是上面创建令牌生成的方法才能验证成功

#### getClaim方法

获得特定声明的值"claims"需要与上面创建的时候的字符串对应

#### asMap方法

将其值转化为map类型便于后续处理

## ThreadLocal

![image-20231201113706458](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201113706458.png)

每个用户的线程独立不会相互影响，可以用来存储被反复使用的数据，免得每次使用到该数据都需要作为方法参数传递。

#### 声明一个ThreadLocal

```java
private static final ThreadLocal THREAD_LOCAL = new ThreadLocal();
```

#### 根据键获取值

```java
public static <T> T get(){
    return (T) THREAD_LOCAL.get();
}
```

#### 存储键值对

```java
public static void set(Object value){
    THREAD_LOCAL.set(value);
}
```

#### 清除内存

```java
public static void remove(){
    THREAD_LOCAL.remove();
}
```

#### 使用

拦截器验证token成功则将claims存进去

![image-20231201131718912](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201131718912.png)

用户需要查询信息时再从中获得claims就可以减少参数

![image-20231201132006734](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231201132006734.png)

## 参数校验

### 方法一

在需要参数校验方法所在的类上添加注解@Validated

需要包

```java
import org.springframework.validation.annotation.Validated;
import org.springframework.validation.annotation.Validated;
```

在需要校验的参数上添加注解@Pattern(regexp = 正则表达式)

如：

```java
public Result register(@Pattern(regexp = "^\\S{5,16}$") String username)
```

如果参数校验失败会返回一个异常（所以需要全局异常处理）

### 方法二

适用于封装的变量

在需要校验的变量上添加一个@Validated

```java
@Validated User user
```

在对应的实体类上添加注解限制参数

```java
@Data
public class User {
    @NotNull
    private Integer id;//主键ID
    private String username;//用户名
    @JsonIgnore//让springmvc把当前对象转换成json字符串的时候，忽略password，最终json字符串就没有password这个属性了
    private String password;//密码
    @NotEmpty
    @Pattern(regexp = "^\\S{1,10}$")
    private String nickname;//昵称
    @NotEmpty
    @Email
    private String email;//邮箱
    private String userPic;//用户头像地址
    private LocalDateTime createTime;//创建时间
    private LocalDateTime updateTime;//更新时间
}
```

@NotEmpty代表字符串不能为空字符

@NotNull代表参数不能为空

@Email代表参数需要满足邮箱格式

只有在含@Validated注解时以上校验才会生效

### URL

@URL可以校验传入参数是不是url类型

一般写在Mapper层

```java
public Result updateAvatat(@RequestParam @URL String avatarUrl)
```

### 自定义注解校验

1.自定义一个注解

```java
@Documented
@Constraint(
        validatedBy = {StateValidation.class}//指定提供校验规则的类
)
@Target(ElementType.FIELD)//注解的对象是类的字段上
@Retention(RetentionPolicy.RUNTIME)//注解在运行时保留
public @interface State {

    //提供校验失败后的提示信息
    String message() default "State参数的值只能是已发布或者草稿";
    //指定分组
    Class<?>[] groups() default {};
    //负载  获取到State注解的附加信息
    Class<? extends Payload>[] payload() default {};

}
```

2.定义一个类继承ConstraintValidator

```java
public class StateValidation implements ConstraintValidator<State,String> {//ConstraintValidator<给哪个注解提供校验规则，校验的数据类型>

    /**
     *
     * @param value 将来要校验的数据
     * @param context
     * @return 如果是false不通过，如果是true则通过
     */
    @Override
    public boolean isValid(String value, ConstraintValidatorContext context) {
        //提供校验规则
        if(value==null){
            return false;
        }
        if(value.equals("已发布")||value.equals("草稿")){
            return true;
        }
        return false;
    }
}
```

3.给自定义注解的Constraint指定第二步制作的类

```java
@Constraint(
        validatedBy = {StateValidation.class}//指定提供校验规则的类
)
```

4.将注解应用在类的字段上

```java
@State
private String state;//发布状态 已发布|草稿
```

## 全局异常处理

所有的异常产生后都需要执行这个方法

具体参考
项目结构->exception

```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(Exception.class)
    public Result handleException(Exception e){
        e.printStackTrace();
        return Result.error(StringUtils.hasLength(e.getMessage())?e.getMessage():"操作失败");
    }
}
```

## 分组校验

解决不同方法校验方式不同的问题

### 在需要校验的类中增加多个接口

在实体类中

```java
public interface Add{

}

public interface Update{

}
```

### 在相关校验注解后按接口进行分组

在实体类的变量上

```java
@NotEmpty(groups = {Add.class,Update.class})
private String categoryAlias;//分类别名
```

### 在需要校验的方法的变量上进行分组

```java
public Result add(@RequestBody @Validated(Category.Add.class) Category category)
```

### Default分组

如果某个校验项没有指定分组，默认属于Default分组

分组之间可以继承

```java
@Data
public class Category {
    @NotNull(groups = Update.class)
    private Integer id;//主键ID
    @NotEmpty
    private String categoryName;//分类名称
    @NotEmpty
    private String categoryAlias;//分类别名
    private Integer createUser;//创建人ID
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")
    private LocalDateTime createTime;//创建时间
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")
    private LocalDateTime updateTime;//更新时间

    //如果某个校验项没有指定分组，默认属于Default分组
    //分组之间可以继承
    public interface Add extends Default {}

    public interface Update extends Default{}
}
```

## 拦截器

具体参考
项目结构->interceptors

```java
@Component
public class LoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //令牌验证
        String token = request.getHeader("Authorization");
        //验证token
        try {
            Map<String,Object> claims = JwtUtil.parseToken(token);
            //把业务数据存储到ThreadLocal中
            ThreadLocalUtil.set(claims);
            //放行
            return true;
        } catch (Exception e) {
            //http响应状态码为401
            response.setStatus(401);
            //不放行
            return false;
        }
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        //清空ThreadLocal中的数据
        ThreadLocalUtil.remove();
    }
}
```

## 拦截器配置类

拦截器会拦截所有请求要求令牌验证，但是登录和注册不能被拦截。

因此新增一个配置类放行这两个接口。

该类需要实现接口**WebMvcConfigurer**

重写**addInterceptors**，该方法本来是用于添加拦截器到注册表，实际上添加跟移除都可以写

这里的**loginInterceptor**就是我们之前写过的拦截器

**InterceptorRegistry**即拦截器注册表

调用其**addInterceptor**修改拦截器注册表，传入我们的拦截器作为参数

调用**excludePathPatterns**排除不需要拦截的路径（相对路径即可），此处可以传入多个字符串，接收参数是一个字符串数组

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Autowired
    private LoginInterceptor loginInterceptor;
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        //登录和注册接口不拦截
        registry.addInterceptor(loginInterceptor).excludePathPatterns("/user/login","user/register");
    }
}
```

## 分页

### 引入依赖

```xml
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.4.6</version>
</dependency>
```

### 开启分页查询

使用PageHelper.startpage(pageNum,pageSize)方法开启分页查询

### 对象转化

将Mapper层返回的List对象强制转换为Page对象

### 样例

```java
@Override
public PageBean<Article> list(int pageNum, int pageSize, int categoryId, String state) {
    //1.创建PageBean对象
    PageBean<Article> pb = new PageBean<>();
    //2.开启分页查询
    PageHelper.startPage(pageNum,pageSize);
    //3.调用mapper
    Map<String,Object> map = ThreadLocalUtil.get();
    int id = (int) map.get("id");
    List<Article> as = articleMapper.list(id,categoryId,state);
    //Page中提供了方法，可以获取PageHelper分页查询后的总记录条数和当前页数据
    Page<Article> p = (Page<Article>) as;
    //把数据填入到PageBean对象中
    pb.setTotal(p.getTotal());
    pb.setItems(p.getResult());
    return pb;
}
```

## Redis

### 引入依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

### 声明一个StringRedisTemplate

```java
@Autowired
private StringRedisTemplate stringRedisTemplate;
```

### 用opsForValue()方法获取一个ValueOperations对象

```java
ValueOperations<String, String> operations = stringRedisTemplate.opsForValue();
```

### 调用ValueOperations对象的set方法设置键值对存入（也可以设置过期时间）

第二行中第三个参数是时间，第四个参数是时间单位，此处表示15秒

```java
operations.set("username","zhangsan");
operations.set("id","1",15, TimeUnit.SECONDS);
```

### 调用get方法获得键对应的值

```java
ValueOperations<String,String> operations = stringRedisTemplate.opsForValue();
System.out.println(operations.get("username"));
```

### 删除键值对

```java
operations.getOperations().delete("username");
```
