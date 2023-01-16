> Service
- @service 어노테이션
```
public int writeComment(CommentDto comment);
```

> ServiceImpl
- Service Implements 
- @Autowired(객체주입) DAO
```
@Autowired
    private CommentDao commentDao;

     @Override
    public int writeComment(CommentDto comment) {
        return commentDao.writeComment(comment);
    }
```

> DAO
- @Repositroy
- @Autowired(객체주입) SqlSessionTemplate 
```
    @Autowired
    protected SqlSessionTemplate sqlSession;
    
    private static String namespace = "com.edu.comment.dao.CommentDao";
    
    @Override
    public int writeComment(CommentDto comment) {
        return sqlSession.insert(namespace+".writeComment", comment);
    }
```

# 로직구현 

> 1. pom.xml
```
myBatis, myBatis-spring, JDBC 추가
		<!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
		<dependency>
		    <groupId>com.mysql</groupId>
		    <artifactId>mysql-connector-j</artifactId>
		    <version>8.0.31</version>
		</dependency>
		
		<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
		<dependency>
		    <groupId>org.springframework</groupId>
		    <artifactId>spring-jdbc</artifactId>
		    <version>${org.springframework-version}</version>
		</dependency>
		
		<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
		<dependency>
		    <groupId>org.mybatis</groupId>
		    <artifactId>mybatis</artifactId>
		    <version>3.5.6</version>
		</dependency>
		
		<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
		<dependency>
		    <groupId>org.mybatis</groupId>
		    <artifactId>mybatis-spring</artifactId>
		    <version>2.0.6</version>
		</dependency>
		
		<!-- https://mvnrepository.com/artifact/org.springframework/spring-tx -->
		<dependency>
		    <groupId>org.springframework</groupId>
		    <artifactId>spring-tx</artifactId>
		    <version>${org.springframework-version}</version>
		</dependency> 
```


> 2. root-context.xml

```
    jdbc,sqlSessionFactory,sqlSession 객체 생성
        <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
	<property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/> --> dbcp드라이버로 수정할 예정
	<property name="url" value="jdbc:mysql://localhost:3306/board"/>
	<property name="username" value="root"/>
	<property name="password" value="1234"/>
	</bean>
	
	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource"></property>
		<property name="mapperLocations" value="classpath*:/mappers/**/*.xml">   
	</property></bean>
		
	<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg ref="sqlSessionFactory"></constructor-arg>	  
```


- connection이란?
    ```
    java와 DB의 연결 돕는 메소드이다. 
    JDBC 드라이버에서  DB와 연결을 하게된다, 이 연결 자체를 connection 이라고 의미한다.
    ```
    <img src="https://github.com/gjwoo96/Stu_StepByStep/blob/main/Spring%20Stu/img/connection.png?raw=true">
    
- connection pool이란?
    ```
    클라이언트의 요청마다 connection을 생성하는게 아니라
    미리 일정 개수의 connection을 만들어 필요한 어플리케이션에 전달하여 이용하는 방법이다.
    ```

- datasource란?
    ```
    connction pool를 어플리케이션단에서 어떻게 관리할지를 구현해야하는 인터페이스이다.
    ```

- JDBC vs DBCP DB접속 라이브러리
    ```
   JDBC : DB연결을 할때마다 커넥션객체를 얻는 작업을 반복(사실상 connection pool을 사용하지않음)
   DBCP : WAS를 실행시 일정 커넥션을 생성하고 pool에 저장, DB연결 요청이 있을시 pool에서 connection객체를 가져다 쓰고 반환 

    * 나는 위의 개념을 모르고 일단 mybatis 연결 예제를 따라했다. 연결세팅을 완료 후 접속 라이브러리의 종류와 개념이 궁금해서 찾던중 DBCP가 훨씬 효율적이라는 것을 찾게되었고 추후에 다시 세팅할 예정이다.
    ```

- sqlsessionFactory,sqlsession은 내일 공부해야지 헤헤


참고: (https://bigfat.tistory.com/95)
____


