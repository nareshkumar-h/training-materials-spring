# Spring Jdbc Template

#### Task 1: Database Credentials
* application.properties
```java
spring.datasource.driverClassName=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://101.53.133.59:3306/revature_training_db
spring.datasource.username=rev_user
spring.datasource.password=rev_user
```

#### Task 2: Define JdbcTemplate Bean
```java

@Configuration
public class DataSourceConfiguration {

  @Bean
  public JdbcTemplate jdbcTemplate(DataSource dataSource) {
    JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
    return jdbcTemplate;
  }
}
```

##### Task 3: Insert Query

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;

public class BookDAO {

	@Autowired
	JdbcTemplate jdbcTemplate;
	
	
	public void addBook(String bookName) {
		String sql= "insert into books(title) values ( ?)";
		Object[] params = { bookName };
		int rows = jdbcTemplate.update(sql, params);
		
	}
	
	
}

```

##### Task 4: Select Query

* Refer : https://nareshkumarh.wordpress.com/2017/05/16/questiontypedao-using-jdbctemplate/
