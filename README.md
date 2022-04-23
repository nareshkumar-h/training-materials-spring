# Spring Learning Plan

#### Task 1: Create Spring Boot Project 
* Create Spring Boot Project ( Add Dependencies : Spring Web + DevTools )
* Change Port : 9000
* Run the Project 

#### Task 2:  Create REST API 
* @RestController, 
* @RequestMapping
* @GetMapping , @PostMapping, @PutMapping, @PatchMapping, @DeleteMapping
* @RequestParam, @PathVariable
* @RequestHeader

#### Task 3: Spring IOC(Inversion of Control) 

* Spring IoC Container is the core of Spring Framework. 
* It creates the objects, configures and assembles their dependencies, manages their entire life cycle. 
* The Container uses Dependency Injection(DI) to manage the components that make up the application

```java
public class UserDAO {

}
```

##### 3.1: Manual Object Creation (Core Java)
```java
UserDAO userDAO = new UserDAO();
```

##### 3.2: Object Creation usung Spring IOC

* Bean Declarations ( We can declare bean using annotions or using xml configuration ) 
```java
@Bean
@Scope("singleton")   // Scope: singleton(default), prototype,request,session,application,websocket
//@Lazy //Lazy vs Eager(default)
public UserDAO userDAO(){
    
    UserDAO dao = new UserDAO();
    return dao;
}
```
* Note: During Spring Boot Server Startup, IOC container will create all objects which are declared in Bean and keep the objects ready for use.

* **Using Object in Controller**
```java
@RestController
public class UserController {

    @Autowired
    UserDAO userDAO;
}
```

#### 4. Spring JDBC

* Select Dependencies : jdbc + mysql
* In application.properties

```
spring.datasource.driverClassName=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://101.53.133.59:3306/revature_training_db
spring.datasource.username=rev_user
spring.datasource.password=rev_user
```

* **Task 1: Get DataSource**

```java
import java.sql.DataSource;

@Autowired
DataSource dataSource;
```

* **Task 2: Create JdbcTemplate using datasource**

* **Using Constructor(we are passing dataSource) **
```java
JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
```
(or)

* **Using setter method( we are passing dataSource) **
```java
JdbcTemplate jdbcTemplate = new JdbcTemplate();
jdbcTemplate.setDataSource(dataSource);
```

* **Task 3: Define JdbcTemplate as Bean**

* **Dependency Injection using Constructor **
```java
@Bean
public JdbcTemplate jdbcTemplate(DataSource dataSource){
    JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
    return jdbcTemplate;
}
```
(or)
* **Dependency Injection using Setter **
```java
@Bean
public JdbcTemplate jdbcTemplate(DataSource dataSource){
    JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
    return jdbcTemplate;
}
```
