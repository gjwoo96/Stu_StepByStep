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

- Mybatis란?
```
	자바 오브젝트와 SQL 사이의 자동 매핑 기능을 지원하는 ORM(Object Relational Mapping)프레임 워크
```
- 특징
```
	1.SQL 파일을 별도로 관리가능하여 자바 내에서 쿼리작성을 할 필요가 없어짐
	2.JDBC의 모든 기능을 Mybatis가 대부분 제공
	3.다양한 프로그래밍 언어로 구현 각능
```
- 아키텍쳐
<img src="https://github.com/gjwoo96/Stu_StepByStep/blob/main/Spring%20Stu/img/mybatis_architecture.png?raw=true"/>


- connection이란?
    ```
    java와 DB의 연결 돕는 메소드이다. 
    JDBC 드라이버에서  DB와 연결을 하게된다, 이 연결 자체를 connection 이라고 의미한다.
    ```
    <img src="https://github.com/gjwoo96/Stu_StepByStep/blob/main/Spring%20Stu/img/connection.png?raw=true"/>
    
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
	JDBC란 데이터베이스 커넥션 인터페이스이다.
	DBCP란 DB 커넥션 방법론이다.
	사실 둘을 비교하는것은 같은 개념이라고 하기에는 엄연히 다르지만 DB를 연결하기위해 생성하는 커넥션을 사용하는 방식때문에 비교가 되는것 같다.
	그 방식의 차이는 아래와 같다.
	
   JDBC : DB연결을 할때마다 커넥션객체를 얻는 작업을 반복(사실상 connection pool을 사용하지않음)
   DBCP : WAS를 실행시 일정 커넥션을 생성하고 pool에 저장, DB연결 요청이 있을시 pool에서 connection객체를 가져다 쓰고 반환
   ``` 

   * 추가공부사항

   -JNDI (Java Naming and Directory Interface)
	
	```
	-JNDI(Java Naming and Directory Interface), DB 커넥션 방법론이다.
	- 자바 애플리케이션을 외부 디렉터리 서비스에 연결(ex 주소 데이터베이스 또는 LDAP서버)
	- 자바 애플릿이 호스팅 웹 컨테이너가 제공하는 구성정보를 참고
	-WAS 단에서 DB커넥션을 제어하며 서버에서 하나의 커넥션 풀을 가진다

	간단하게 내가 이해한 바로는
	WAS단에서 DB 커넥션 객체를 미리 네이밍 해두는 이점이 있으며, DBCP를 사용할 경우는 프로젝트 소스 내에 설정을하여 소스 개발자 외에 DB설정 정보를 찾기 힘든 단점이 있지만 JNDI의 경우 WAS단에서 설정하기때문에 커넥션 정보를 찾기 용이하여 유지보수에 좋다.
	그리고 어플리케이션이 하나여도 여러 DB를 끌어와 쓸수있다는 이점이 있다고한다.
	```
	JNDI 참고:(https://eongeuni.tistory.com/43)  
___	

    * 나는 위의 개념을 모르고 일단 mybatis 연결 예제를 따라했다. 연결세팅을 완료 후 접속 라이브러리의 종류와 개념이 궁금해서 찾던중 DBCP가 훨씬 효율적이라는 것을 찾게되었고 추후에 다시 세팅할 예정이다.
    ```

- sqlsessionFactory,sqlsession은 내일 공부해야지 헤헤


참고: (https://bigfat.tistory.com/95)
____


