# 初始化项目

可以通过 https://start.spring.io/ 官网上生成项目。

## 1. 通过 elipse 创建 maven 项目：

File --> New --> Maven Project --> Next --> 直接选 Next --> 
填写相关的内容 Group Id （包名） ArtifactId (项目名) Package （包名+项目名） --> 完成

## 2. POM 文件中填写内容：
```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.8.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.example</groupId>
	<artifactId>demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>demo</name>
	<description>Demo project for Spring Boot</description>

	<properties>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```

## 3. 核心启动类
```java
@SpringBootApplication
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}

}
```

## 4. 测试 Controller
```java
/**
 * 测试类
 * @author dong.li
 *
 */
@RestController
@RequestMapping("/demo")
public class DemoController {

	/**
	 * 测试方法
	 * @return
	 */
	@RequestMapping(value="/sayHello",method=RequestMethod.GET)
	public String sayHello() {
		HashMap<String, String> map = new HashMap<String, String>();
		map.put("name", "白静");
		map.put("desc", "希望你一直幸福");
		return map.toString();
	}
}

```

## 5. 启动核心类

## 6. 访问链接：
127.0.0.1:8080/demo/sayHello