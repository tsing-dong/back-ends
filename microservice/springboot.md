# SpringBoot之集成SringAOP

1. 在 pom 中添加依赖:

```text
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-aop</artifactId>
            </dependency>


            <!-- https://mvnrepository.com/artifact/com.google.guava/guava -->
            <!-- com.google.common.collect.Maps 依赖-->
            <dependency>
                <groupId>com.google.guava</groupId>
                <artifactId>guava</artifactId>
                <version>24.1-jre</version>
            </dependency>

            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>fastjson</artifactId>
                <version>1.2.43</version>
            </dependency>
```

1. 主要介绍  环绕通知 ,其他的后续会进行补充.                   
   * 准备                     

       a. 创建 Aspect切面类:

```text
                /**
                    * 1.先创建一个Aspect切面类
                    */
                @Component
                @Aspect
                public class WebControllerAop {

                }
```

```text
        b. 指定切入点:
```

```text
                /**
                * 
                * executeService:(切面类的切入点). <br/>
                * 
                * @author 李栋
                * @since JDK 1.8
                */
                @Pointcut("execution(* com.baichanghui.order.controller..*.*(..))")
                public void executeService() {

                }
```

```text
        c. 创建 Controller  
```

```text
                @RestController
                public class BillingController {


                            @RequestMapping(value="/get",method=RequestMethod.GET)
                        public Billing getBilling (@RequestParam( value="_id",required=false) long _id) {
                            //处理业务逻辑
                            }

                }
```

1. 环绕通知:

   \`\`\`

   ```text
        /**
        * executeService:(切面类的切入点). <br/>
        * @author 李栋
        * @since JDK 1.8
        */
        @Pointcut("execution(* com.baichanghui.order.controller..*.*(..))")
        public void executeService() {}
   ```

```text
            /**
                * 环绕通知： 环绕通知非常强大，可以决定目标方法是否执行，什么时候执行，执行时是否需要替换方法参数，执行完毕是                                                                                    
                否需要替换返回值。
                * 环绕通知第一个参数必须是org.aspectj.lang.ProceedingJoinPoint类型
                */
                @Around("execution(* com.baichanghui.order.controller..*.get*(..))")
                public Object doAroundService(ProceedingJoinPoint proceedingJoinPoint) {
                    System.out.println("环绕通知的目标方法名为 ： " + proceedingJoinPoint.getSignature().getName());
                        //处理传入参数
                        processInputArg(proceedingJoinPoint.getArgs());
                    try {
                        Object object = proceedingJoinPoint.proceed();
                        //处理返回结果
                        processOutPutObj(object);
        return object;
                    } catch (Throwable throwable) {
                        throwable.printStackTrace();
                    }
                    return null;
                }


                    //环绕通知--处理返回结果
                    private void processOutPutObj(Object object) {
                        // TODO Auto-generated method stub
                        System.out.println("OBJ 原本为：" + object.toString());
                    }

                    //环绕通知--处理请求参数
                    private void processInputArg(Object[] args) {
                        for (Object arg : args) {
                            System.out.println("ARG原来为:" + arg);
                        }
                    }
```

```text
        4、切入点规则说明：
           //所有执行的方法都会执行 环绕通知
            . *  

           //指定一个包下面的一个类中的方法中包含字段的方法执行,  \ 用来转义:
            cn\.itcast\.spring3\.OrderDao\.add\.* 

           //只要包含 add 的方法就执行:
           . *add.*

### SpringBoot 定时任务
        注意： 现在微服务架构项目做定时任务应该避免，将定时任务写在不同的服务中，因为如果将定时任务写在不同的服务中，正式环境部署时因为需要 nginx 负载均衡，到时候会多个项目同时执行定时任务。所以做微服务的项目需要将定时任务单独放在一个项目中。

    1. 在 springboot 的启动类上添加注解:
            @EnableScheduling//支持定时任务

    2. 创建定时任务类:
```

```text
    @Component
    public class TeamBuildingJob {

        public final static long ONE_MINUTE= 1500;

        @Scheduled(fixedDelay=ONE_MINUTE)
        public void fixDelatJib() {
            System.out.println(TimeCmmons.getNowDate()+" >>fixedDelay执行....");
        }

        @Scheduled(fixedRate=ONE_MINUTE)
            public void fixedRateJob(){
                System.out.println(TimeCmmons.getNowDate()+" >>fixedRate执行================....");
            }

            @Scheduled(cron="*/5 * * * * *")  //每5秒执行一次
            public void cronJob(){
                System.out.println(TimeCmmons.getNowDate()+" >>cron执行....");
            }

    }
```

```text
        * 注意: 上面两种是在项目启动时就先执行一次定时任务,后面按规定的时间执行.
            cron 表达式是按照规定的时间执行.比如: 规定了 5 秒执行一次,等项目启动时 5 秒之后进行启动.
            * 说明:
                单位: 毫秒  1min= 60 * 1000
                    *  fixedDelay 和 fixedRate 区别: 
                        fixedRate 这个是多多次执行任务时,无论业务数据执行多长时间,定时任务都是再次执行.
                        fixedRate 是当业务数据执行完成后的 1 分钟执行.
                    *   还有一种方式就是:
```

```text
                        cron 表达式:
                                * 第一位，表示秒，取值0-59
                                * 第二位，表示分，取值0-59
                                * 第三位，表示小时，取值0-23
                                * 第四位，日期天/日，取值1-31
                                * 第五位，日期月份，取值1-12
                                * 第六位，星期，取值1-7，星期一，星期二...，注：不是第1周，第二周的意思
                                另外：1表示星期天，2表示星期一。
                                * 第7为，年份，可以留空，取值1970-2099
```

```text
                            cron中，还有一些特殊的符号，含义如下:

                                (*)星号：可以理解为每的意思，每秒，每分，每天，每月，每年...
                                (?)问号：问号只能出现在日期和星期这两个位置，表示这个位置的值不确定，每天3点执行，所以第六位星期的位置，我们是不需要关注 
                                    的，就是不确定的值。同时：日期和星期是两个相互排斥的元素，通过问号来表明不指定值。比如，1月10日，比如是星期1，如果在星期 
                                    的位置是另指定星期二，就前后冲突矛盾了。
                                (-)减号：表达一个范围，如在小时字段中使用“10-12”，则表示从10到12点，即10,11,12
                                (,)逗号：表达一个列表值，如在星期字段中使用“1,2,4”，则表示星期一，星期二，星期四
                                (/)斜杠：如：x/y，x是开始值，y是步长，比如在第一位（秒） 0/15就是，从0秒开始，每15秒，最后就是0，15，30，45，60    另： 
                                    */y，等同于0/y

### spring 常用注解:
    * @RestController                
        说明：如果使用 @RestController , 则 Controller 中的方法无法返回页面，或者 jsp 。 配置的视图解析器就会不起作用。返回的是 return 内容。          
    * @Controller        
        说明：如果需要返回指定的页面或者 JSP ，使用 @Controller 和 InternalResourceViewResolver 配合。如果需要返回 JSON ,需要在方法上添加 @ResponseBody 注解。                  

### springBoot 2.* 之集成 redis: 

    * 添加 POM 依赖:
```

```text
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
```

```text
    * application.properties 配置 redis 信息:
```

```text
    #redis 相关配置
    #Ip
    spring.redis.host=39.98.165.77
    #端口
    spring.redis.port=6379
    #密码
    spring.redis.password=123456789
    #使用数据库
    spring.redis.database=0
    # 数据库连接超时时间，2.0 中该参数的类型为Duration，这里在配置的时候需要指明单位
    spring.redis.timeout=2000ms
    # 最大空闲连接数
    spring.redis.jedis.pool.max-idle=500 
    # 最小空闲连接数
    spring.redis.jedis.pool.min-idle=50
    # 等待可用连接的最大时间，负数为不限制
    spring.redis.jedis.pool.max-active=-1 
```

\`\`\`

* 直接注入:            

    @Autowired

    private StringRedisTemplate stringRedisTemplate;   

