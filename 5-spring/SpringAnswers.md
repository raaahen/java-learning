# 1. ��� ����� �������� �������� (IoC) � ��������� ������������ (DI)? ��� ��� �������� ����������� � Spring?

**�������� �������� (IoC)** ? ��� ������� ����������������, ��� ������� ���������� ������� ��������� ���������� �������� ���������� ��� ����������, � �� ������������ ����� �����. � ��������� ��������-���������������� ���������������� ��� ��������, ��� ������ �� ������� ���� ����������� ��������������, � �������� �� �����.

**��������� ������������ (Dependency Injection, DI)** ? ��� ���� �� �������� ���������� �������� IoC. DI ��������� ���������� ����������� (��������, �������, �� ������� ������� ������ ������) ����� �����������, ������ ��� ���� ������.

**��� ��� ����������� � Spring?**

Spring ? ��� ���������, ������� ������ ���������� ������� IoC � ������������� ��������� ��������� ��� ��������� ������������:

1. **��������� IoC**: � Spring ��������� IoC �������� �� �������� � ���������� ��������� ������ �������� (�����). ��������� ������� �������, ��������� �� ���� � ������, ����������� �� � ��������� �� ��������� ������ � ����������� �� ������������, ������� ����� ���� ���������� � XML-������, ���������� ��� Java-����.

2. **������� ��������� ������������**:
   - **����� �����������**: ����������� ���������� ����� ����������� ������. ��� �������� ���������� � ������������� ������, ��� ��� ����������� ��������������� ��� �������� ������� � �� ����� ���� �������� ������������.
   - **����� �������**: ����������� ���������� ����� ������� (������ ���������). ���� ������ ��������� �������� ����������� ����� �������� �������.
   - **����� ����**: ��������� ������������ ��������������� � ���� ������ � �������������� ��������� `@Autowired`.

������ ��������� ����������� ����� �����������:

```java
@Component
public class MyService {

    private final MyRepository myRepository;

    @Autowired
    public MyService(MyRepository myRepository) {
        this.myRepository = myRepository;
    }

    public void performService() {
        // ������������� myRepository ��� ���������� ������-������
    }
}
```

� ���� ������� `MyService` ������� �� `MyRepository`. Spring ������������� ������� ������ ��� `MyRepository` � `MyService` ��� �������� ���������� `MyService`. 

����� �������, Spring ������������� ������ ����������� ��� ���������� ��������� IoC � DI, ��� �������� ����������, ������������ � ������������� ����������.

# 2. ��� ����� IoC ���������?

## �����������

IoC (Inversion of Control) ��������� ? ��� ����������� ��������� ���������� Spring, ������� ��������� ���������, ���������� � ����������� ��������� ������ �������� (�����). �� �������� ����������� ����� ������������, ��� ��������� ����������� ������� �������� ����������.

## �������� ������ IoC ����������:

1. **�������� ��������**: IoC ��������� ��������� ��������� ����������� ������� �� ������ ������������, ����� ��� ��������� ��� XML.
  
2. **��������� ������������**: ��������� ������������� �������� ����������� ����� ���������, ���� ����� ������������, ���� ����� �������.

3. **���������� ��������� ������ �����**: IoC ��������� ��������� ������ ��������� ������ �����, ������� �� ��������, ������������� � �����������.

4. **���������������� � ���������**: IoC ��������� ������������� ����������� ��� ���������������� � ��������� ����� ����� ������� ����� ������������ ��� ���������.

## ������

���� ������ ������������� IoC ���������� � Spring � �����������:

```java
@Component
public class UserService {
    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void performOperation() {
        // ������ ������ � userRepository
    }
}
```

� ���� ������� `UserService` ������� �� `UserRepository`, � ��� ����������� ���������� ����������� IoC ������������� ����� ��������� `@Autowired`.

## ����������

IoC ��������� �������� ���������� ������������� � ������������ ����� ������ � ��������� ����������� ����������, �������� ������������ ��������������� �� ������-������, � �� �� ������ ���������� �������������.

# 3. ���������� ��� ApplicationContext � BeanFactory, ��� ����������? � ����� ������� ��� ����� ������������?

## ApplicationContext � BeanFactory

### BeanFactory
**BeanFactory** ? ��� ��������� � Spring, ������� ������������� �������� ���������� IoC ����������, ������� �������� � ���������� ������. �� ������������ ������� �������������, ��� ��������, ��� ������� (����) ��������� ������ �����, ����� ��� ������������� �����.

#### ������ ������������� BeanFactory:

```java
Resource resource = new ClassPathResource("applicationContext.xml");
BeanFactory factory = new XmlBeanFactory(resource);

MyBean myBean = (MyBean) factory.getBean("myBean");
```

### ApplicationContext
**ApplicationContext** ? ��� ����� �������������� ��������������, ����������� `BeanFactory`. �� ������������� �������������� �����������, ����� ���:
- **��������� ������� (Event handling)**.
- **��������� �������������������**.
- **�������������� �������� �����** (��������, `ApplicationContext` ��������� ��� ���� ����� ��� �������������, � �� ������).
- **���������� � AOP (Aspect-Oriented Programming)**.
- **���������� ��������� ������ �����**, ��������, ��������� ������� ������������� � �����������.

#### ������ ������������� ApplicationContext:

```java
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");

MyBean myBean = context.getBean(MyBean.class);
```

## �������� �������

1. **��������� �������**: `ApplicationContext` ������������ �������� �������, ��� ��������� �������� � ��������� � ����������, � ������� �� `BeanFactory`.

2. **��������� �������������������**: � `ApplicationContext` ������������� ��������� ������������������� ����� `MessageSource`, ���� ��� � `BeanFactory`.

3. **������������ �����**: � `ApplicationContext` ��� ���� ��������� � ���������������� ��� ������� ���������� (eager initialization), ����� ��� `BeanFactory` ��������� �� ������.

4. **��������� AOP**: `ApplicationContext` ������������ ���������� � ��������-��������������� �����������������, ��� �� ����������� � `BeanFactory`.

## ����� ������������?

- **BeanFactory**: ����� ������������ � �������, ����� ��������� ����������� ��������� � ������������ ���������� ���������, � ������������� ����� ������ ����������� ������.

- **ApplicationContext**: ������������� ������������ � ����������� ���������� Spring, ��� ��� �� ������������� ��� ������� `BeanFactory` � ����� �������������� ������������, ����� ��� ���������� ���������, ������������������� � ���������� � AOP.

# 4. ���������� ��� ��������� @Bean?

## ��������� @Bean

��������� `@Bean` � Spring ������������ ��� ����������� �������, ������� ���������� ������, ������������� ����������� Spring. ��� ������ ������ ��������� � �������, ���������� ���������� `@Configuration`. ������������ ������ ������������� ���������� Spring-����� � ����������� ����������� IoC.

### �������� ����������� ��������� @Bean

1. **����������� �����**: �����, ���������� ���������� `@Bean`, ����������, ��� ������������ ������ ������ ���� ��������������� ��� Spring-���. ���� ��� �������� ��� �������� ������������ � ������ ����.

2. **���������������� ������**: ������ `@Bean` ������������ � �������, ���������� ���������� `@Configuration`. ����� ����� ������������ ����� ���������������� ���� � Java, ����������� XML-������������.

3. **���������� �������������**: ������ ������ � `@Bean` ����� ��������� ������������� � ���������� ��� ������������������ ������.

4. **���������� ��������� ������**: ������ � ���������� `@Bean` ����� ��������� ������ ������������� ��� ����������� ����� ����� ������������� ����������� ��������� `initMethod` � `destroyMethod`.

### ������ ������������� ��������� @Bean

```java
@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }

    @Bean
    public MyRepository myRepository() {
        return new MyRepositoryImpl();
    }
}
```

� ���� ������� ����� `AppConfig` ������� ���������� `@Configuration`, ��� ������ ��� ���������������� �������. ������ `myService()` � `myRepository()` ���������� �������, ������� ���������� Spring-�� ������.

### �������������� �������� ��������� @Bean

- **name**: ��������� ������ ��� ����. ���� �� �������, ������������ ��� ������.
- **initMethod**: ���������� �����, ������� ����� ������ ��� ������������� ����.
- **destroyMethod**: ���������� �����, ������� ����� ������ ��� ����������� ����.

### ������ � initMethod � destroyMethod

```java
@Bean(initMethod = "init", destroyMethod = "cleanup")
public MyBean myBean() {
    return new MyBean();
}
```

� ���� ������� ������ `init()` � `cleanup()` ������� `MyBean` ����� ������� ��� ��� �������� � ����������� ��������������.

��������� `@Bean` ������������ ��� ������� ����������� � ������������ ����� � Spring-����������, �������� ������������� ��������� �� ��������� � ��������� ������.

# 5. ���������� ��� ��������� @Component?

## ��������� @Component

��������� `@Component` � Spring ������������ ��� ��������������� ����������� � ����������� ���� � ��������� Spring. ��� ���������, ��� �������������� ����� �������� ���������� �� �������� ���� � ��� ����������� ���������� ����������� IoC.

### �������� ����������� ��������� @Component

1. **�������������� ����������� �����**: �����, ���������� ���������� `@Component`, ������������� �������������� � ��������� Spring ��� ���. ��� �������� ������������ ����������, ��� ��� �� ��������� ������� ��������� ��� � ���������������� ������.

2. **��������� ������������� ������������**: `@Component` �������� � ������ � ���������� ������������� ������������ (`Component Scanning`), ������� ������������� ������� � ������������ ��� ������ � ���������� `@Component` � ��� ������������.

3. **����� ������ �������������**: ��������� `@Component` ����� ���� ������������ ��� ����� �������, ������� ������ ����������� Spring, �� � Spring ����� ���� ������������������ ���������, ������� �������� ������������ �� `@Component` � ����� ����� ����������� ��������������, ����� ���:
   - `@Service` ? ������������ ��� �������, �������������� ����� �������.
   - `@Repository` ? ������������ ��� �������, ����������� ���� ������������.
   - `@Controller` ? ������������ ��� ������������ � Spring MVC.

### ������ ������������� ��������� @Component

```java
@Component
public class MyService {
    
    public void performTask() {
        System.out.println("Task performed");
    }
}
```

� ���� ������� ����� `MyService` ������� ���������� `@Component`, ��� ������ ��� ������������� ��������� ��� �������� ������������ � ������ ����������� Spring.

### ������������ ������������

��� ���� ����� Spring ��� ������������� ������������ � �������������� ����������, ����� ��������� ������������ ������������. ������ ��� �������� � ������� ��������� `@ComponentScan` � ���������������� ������.

```java
@Configuration
@ComponentScan(basePackages = "com.example.myapp")
public class AppConfig {
    // ������������ ����������
}
```

���� ��� ��������� Spring ����������� ����� `com.example.myapp` � ������������� �������������� ��� ������, ���������� ���������� `@Component` (� ������������ �� ���).

### ������������� @Component � ������� �����������

��������� `@Component` ����� ���������� � ������� �����������, ������ ��� `@Autowired`, ��� �������������� �������� ������������.

```java
@Component
public class MyService {

    private final MyRepository myRepository;

    @Autowired
    public MyService(MyRepository myRepository) {
        this.myRepository = myRepository;
    }
    
    public void performTask() {
        System.out.println("Task performed");
    }
}
```

����� ����� `MyService` ������� �� `MyRepository`, � Spring ������������� ����������� ����������� ����� �����������.

��������� `@Component` �������� ������������� ���������� ��� �������������� ����������� ����� � Spring, ������� ������������ � ���������� �������������.

# 6. ��� ���������� ��������� @Bean � @Component?

## �������� �������

��������� `@Bean` � `@Component` � Spring ������������ ��� �������� � ���������� ������, �� ��� ������������� ��� ������ ����� � ����� ������ ������� �������������.

### ��������� @Component

- **����������**: `@Component` ������������ ��� �������������� ����������� ������� ��� ����� � ��������� Spring. �����, �������������� `@Component`, ������������� �������������� � �������������� Spring ��� ������������ ������������.
  
- **�������������� �����������**: ������������ � ��������� � ������������ �������������, ��� Spring ������������� ������� ������ � `@Component` (� ��� ������������, ������ ��� `@Service`, `@Repository`, `@Controller`) � ������������ �� ��� ����.

- **���� �������**: ����������� � �������, ������� ������ ���� ������������ Spring, ��������, �������, �����������, ����������� � ������ ����������.

- **������ �������������**:

    ```java
    @Component
    public class MyService {
        public void performTask() {
            System.out.println("Task performed");
        }
    }
    ```

### ��������� @Bean

- **����������**: `@Bean` ������������ ��� ������ ����������� ������ � ���������������� ������, ������� ������� � ���������� ������ ����. ���� ��� ����� �������������� � ��������� Spring.

- **������ �����������**: � ������� �� `@Component`, ������� ������������� ������������ ����, `@Bean` ������������ ��� ������ ����������� ����� ������ ������� � ���������������� �������, �������������� `@Configuration`.

- **���� �������**: ����������� � �������, ������� ������� �������, ������� ������ ���� ���������� Spring.

- **�������� � ��������**: `@Bean` ������������� ������� �������� ��� ��������� �������� ����, �������� ��� ��������� ��� ������� ��� ����� �����, ��� � �������������� `@Component`.

- **������ �������������**:

    ```java
    @Configuration
    public class AppConfig {

        @Bean
        public MyService myService() {
            return new MyService();
        }
    }
    ```

## ��������� � ������

- **�������������� vs. ������ �����������**: `@Component` ������������ ��� �������������� ����������� ����� ����� ������������� ������������, ����� ��� `@Bean` ������������ ��� ������� ����������� � ��������� ����� ����� ������ � ���������������� �������.
  
- **������������� � ������������**: `@Component` ����������� � ����� �������, � �� ����� ��� `@Bean` ? � ������� ������ ���������������� �������.

- **������������������ ���������**: `@Component` ����� ���������� ������������������� �����������, ������ ��� `@Service` ��� `@Repository`, ��� ������� ������������� �������, ����� ��� `@Bean` �� ����� ����� ����������� ���������.

### ����� ������������:

- ����������� `@Component`, ����� ��� ����� ������������� ���������������� ����� ��� ���, � Spring ������ ����� ��� ����� ������������ ������������.
  
- ����������� `@Bean`, ����� ��� ����� ������ �������� ��� ��������� ����, ��� ����� ��� ������� ������� ������ �������������, ������� �� ����� ���� ���������� ����� ������� ������������ �������.

# 7. ���������� ��� ��������� @Service � @Repository. ��� ��� ����������?

## ��������� @Service

- **����������**: `@Service` ������������ ��� ������������� �������, ������� �������� ������-������. ��� ������������������ ������ ��������� `@Component`, ������� ������ ��� ����� ����������� � ��������, �������� �� ��, ��� ����� ������������ ����� ��������� ���������.

- **�������������**: ��������� `@Service` ������ ����������� � �������, ������� ��������� �������� ������-������ ����������.

- **������������� ��������**: � �� ����� ��� `@Component` �������� ����� ����� ����������, `@Service` ������������ ��� ����������� ���� ������� � ����������, ��� ������ ��� ����� ����������������� � ��������������.

- **������**:

    ```java
    @Service
    public class UserService {
        public User findUserById(Long id) {
            // ������ ������ ������������ �� ID
        }
    }
    ```

## ��������� @Repository

- **����������**: `@Repository` ������������ ��� ������������� �������, ������� ��������������� � ����� ������. ��� ����� ������������������ ������ `@Component`, �� � ��������������� �������������.

- **�������������**: ����������� � �������, ������� ��������� ������ � ������, ��������, DAO (Data Access Object) ������. Spring ������������� ������������� ����������, ����������� ��� �������������� � ����� ������, � ��������� �� � ��������������� ���������� Spring Data.

- **�������� ����������**: ����� �� ������������ `@Repository` �������� �������������� ��������� � �������������� ����������, ��������� � ����� ������, � ����������, ����������� Spring.

- **������**:

    ```java
    @Repository
    public class UserRepository {
        public User findById(Long id) {
            // ������ ������� � ������ ��� ������ ������������ �� ID
        }
    }
    ```

## ������� ����� @Service � @Repository

- **���� ����������**: `@Service` ������������ ��� �������, ������� ��������� ������-������, � `@Repository` ? ��� �������, ������� ��������� �������� � ������.
  
- **��������� ����������**: `@Repository` ����� �������������� ����������������, ��������� � ���������� ����������, ����������� ��� ������ � ����� ������, ���� ��� � `@Service`.

- **���������**: ���� ��� ��������� �������� ��������������� `@Component`, �� ������������� �������� ��������� ���� � ������ ��� ����� ��������, �������� �� ���� ������ � ����������� ����������.

# 8. ���������� ��� ��������� @Autowired

## �������� ��������

- **����������**: ��������� `@Autowired` ������������ � Spring ��� ��������������� ��������� ������������ (dependency injection) � ����������. ��� ��������� Spring ������������� ������� ����������� ���� � ������� ������, �������� ��� �������.

- **�������������**: `@Autowired` ����� ���� ��������� � �������������, �������, ����� � �������� ��� ��������, ��� Spring ������ ������������� �������� ����������� ��� �������� ���������� ������.

## ������� �������������

### 1. ��������� ����� ����

```java
@Component
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User findUserById(Long id) {
        return userRepository.findById(id);
    }
}
```

- � ������ ������� `UserRepository` ������������� ���������� � `UserService` ����� ����.

### 2. ��������� ����� �����������

```java
@Component
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User findUserById(Long id) {
        return userRepository.findById(id);
    }
}
```

- � ���� ������� ����������� ���������� ����� �����������. ��� ���������������� ������, ��� ��� �� ��������� ���������� �������������� ������������.

### 3. ��������� ����� �����

```java
@Component
public class UserService {

    private UserRepository userRepository;

    @Autowired
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User findUserById(Long id) {
        return userRepository.findById(id);
    }
}
```

- ����� ����������� ���������� ����� ������.

## �����������

- **������������ � �������������� �����������**: �� ���������, `@Autowired` �������, ��� ����������� ����� ��������������. ���� ����������� ����� ���� ��������������, ����� ������������ �������� `required = false`.

  ```java
  @Autowired(required = false)
  private Optional<Dependency> optionalDependency;
  ```

- **����� ����**: ���� ���������� ��������� ����� ������ ����, ���������� ������������ ��������� `@Qualifier` ��� ���������, ����� ������ ��� ������ ���� �������.

  ```java
  @Autowired
  @Qualifier("specificBean")
  private UserRepository userRepository;
  ```

- **��������� ���������**: `@Autowired` ����� ������������ ��������� �������, �������� � ������ ���������, ���������� ���� ������ ����.

  ```java
  @Autowired
  private List<Service> services;
  ```

## ����������

��������� `@Autowired` ��������� ������ � ������������� � Spring, �������� ������������� ��������� ����, ��� ����������� �������� ������������ � ���������� ����������.

# 9. ���������� ��� ��������� @Resource

## �������� ��������

- **����������**: ��������� `@Resource` ������������ ��� ��������� ������������ � ������. ��� �������� ������ ������������ JSR-250 � ������������� ������ �������� ������������ � ������� ����������. � ������� �� ��������� `@Autowired`, ������� �������� � �����, `@Resource` ������������� �� ����������� �������.

## ����������

- **����� �������������**: `@Resource` ����� ���� ��������� � �����, ������� � ��������, ���������� `@Autowired`.

- **������ ��������� ����� ����**:

```java
import javax.annotation.Resource;

@Component
public class UserService {

    @Resource(name = "userRepository")
    private UserRepository userRepository;

    public User findUserById(Long id) {
        return userRepository.findById(id);
    }
}
```

- **������ ��������� ����� ������**:

```java
import javax.annotation.Resource;

@Component
public class UserService {

    private UserRepository userRepository;

    @Resource
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User findUserById(Long id) {
        return userRepository.findById(id);
    }
}
```

## �����������

- **����� ���� �� �����**: ������ ������������ `@Resource` �������� ����������� ������� ��� ���� ����� �������� `name`. ���� ��� �� �������, �� Spring ���������� ��� ���� ��� ������ ��� ������ ���������������� ����.

- **��������� � JNDI**: � ��������� Java EE `@Resource` ����� ������������ ��� ������ � ��������� �������� ����� JNDI (Java Naming and Directory Interface), ����� ��� ��������� ������, ���������� JMS � ������ �������.

- **��������� � `@Autowired`**:
  - `@Autowired` ������������� �� ��� � ����� �������� � `@Qualifier` ��� ���������, ����� ������ ��� ������� ��������.
  - `@Resource` ������������� �� ��� ���� � � ������ ������� �������� �������� ����������� �� �����.

- **���������**:
  - ���� ������� ��� (`name`), `@Resource` ����� ������ ��� �� �����.
  - ���� ��� � ��������� ������ �� ������, �� ����� ����������� ������� ������ �� ����.

## ����������

��������� `@Resource` ������������� ������ ���������� ��� ��������� ������������ � �������� �� ���������� �����, ��� ����� ���� ������� � ������������ ���������, �������� ����� ����� ����� �������, ����� ������ ��� ��� ������ ���� �������.

# 10. ���������� ��� ��������� @Inject

## �������� ��������

- **����������**: ��������� `@Inject` ������������ ��� ��������� ������������ � ������ � ������������ � ���������� Dependency Injection (DI). ��� �������� ������ ������������ JSR-330 (Java Dependency Injection) � ������������� ������ ��������������� ��������� ������������ �� ������ ����.

## ����������

- **����� �������������**: `@Inject` ����� ���� ��������� � �����, ������������� � �������. ��� ���������� ��������� `@Autowired` � Spring.

- **������ ��������� ����� ����**:

```java
import javax.inject.Inject;

@Component
public class UserService {

    @Inject
    private UserRepository userRepository;

    public User findUserById(Long id) {
        return userRepository.findById(id);
    }
}
```

- **������ ��������� ����� �����������**:

```java
import javax.inject.Inject;

@Component
public class UserService {

    private final UserRepository userRepository;

    @Inject
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User findUserById(Long id) {
        return userRepository.findById(id);
    }
}
```

- **������ ��������� ����� �����**:

```java
import javax.inject.Inject;

@Component
public class UserService {

    private UserRepository userRepository;

    @Inject
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User findUserById(Long id) {
        return userRepository.findById(id);
    }
}
```

## �����������

- **�������������� ��������� �� ����**: ��������� `@Inject` �������� ���������� `@Autowired` � Spring � ������������� �� ��� ����. ���� � ��������� Spring ���� ����� ������ ���� ������ ����, �� ����� ������������� ������������� ��������� `@Named` ��� ���������, ����� ������ ��� ������� ��������.

- **������������� � ����� ����������**: ���� ���������� �������� �������� ��� ��������� ����������� �� �������, ����� ��� ������������� �����������, ����� ������������ `Provider<T>`:

```java
import javax.inject.Inject;
import javax.inject.Provider;

@Component
public class UserService {

    private final Provider<UserRepository> userRepositoryProvider;

    @Inject
    public UserService(Provider<UserRepository> userRepositoryProvider) {
        this.userRepositoryProvider = userRepositoryProvider;
    }

    public User findUserById(Long id) {
        return userRepositoryProvider.get().findById(id);
    }
}
```

- **��������� � `@Autowired`**:
  - `@Inject` �� ������������ ����� ���������, ��� `required`, ������������ � `@Autowired` ��� �������� �������������� �����������.
  - `@Autowired` �������� ����������� ��� Spring, ����� ��� `@Inject` ? ��� ����������� ��������� Java.

- **������������� � `@Qualifier`**: ��� ������ ����������� ���� ����� ������������ ��������� `@Qualifier` (��� �� ������ `@Named` �� JSR-330) ��������� � `@Inject`:

```java
import javax.inject.Inject;
import javax.inject.Named;

@Component
public class UserService {

    @Inject
    @Named("specificUserRepository")
    private UserRepository userRepository;

    public User findUserById(Long id) {
        return userRepository.findById(id);
    }
}
```

## ����������

��������� `@Inject` �������� ����������� � ������������� �������� ��������� ������������ � Java. ��� ������������� �������� � ������������� � ���������� DI-������������, ������� Spring, �������� ������������� ������������ ����������� ������� � ���������� �������������.

# 11. ���������� ��� ��������� @Lookup

## �������� ��������

- **����������**: ��������� `@Lookup` ������������ � Spring ��� ������������� ���������� � ��������� ������������ � ����, ����� ���������, ����� ����� ��������� �������� (prototype-scoped) ����. ��� ��������� �������� ����� ��������� ���� ��� ������ ������ ������.

## ����������

- **����� �������������**: `@Lookup` ����������� � �������, ������� ���������� ���� � �������� ��������� `prototype`. ��������� �������, ����� ���������� �������� ��� � ���� �������� � ��� � �������� ��������� `singleton`.

- **������ �������������**:

```java
import org.springframework.beans.factory.annotation.Lookup;
import org.springframework.stereotype.Component;

@Component
public class SingletonBean {

    public void process() {
        PrototypeBean prototypeBean = createPrototypeBean();
        prototypeBean.doSomething();
    }

    @Lookup
    public PrototypeBean createPrototypeBean() {
        // Spring ������������� ������������� ���� ����� � ������ ����� ��������� PrototypeBean
        return null; // ���� ��� ������� �� ����������
    }
}
```

� ������ ������� ����� `createPrototypeBean()` ���������� ����� ��������� `PrototypeBean` ��� ������ ������ ������ `process()`.

## �����������

- **������������ ���������������**: ����� Spring ������� ��������� `@Lookup` ��� �������, �� ����������� ������� �������� �������� ���� � �������������� ��������� �����, ����� �� ��������� ����� ��������� ���� � �������� ��������� `prototype`.

- **���������� ��� ������������� `prototype` � `singleton`**: ���� � ��� ���� `singleton`-���, ������� ������� �� `prototype`-����, � ��� �����, ����� ������ ����� ������ �������� ����� ��������� `prototype`-����, ��������� `@Lookup` ? ��������� �������.

- **���������� ������������� � ����� ��������� ����� ApplicationContext**: ��������� `@Lookup` ��������� �������� ������ ��������� `ApplicationContext` ��� ������������� `ObjectFactory` ��� ��������� ����� ����������� `prototype`-����, ����� ��� ���� � ����� ��������.

## ������ ������� ������

```java
import org.springframework.beans.factory.annotation.Lookup;
import org.springframework.stereotype.Component;

@Component
public class SingletonBean {

    public void executeTask() {
        PrototypeBean prototypeBean = createPrototypeBean();
        prototypeBean.doTask();
    }

    @Lookup
    public PrototypeBean createPrototypeBean() {
        return null; // ���� ����� ���������������� Spring
    }
}

@Component
@Scope("prototype")
public class PrototypeBean {

    public void doTask() {
        System.out.println("Executing task in prototype bean");
    }
}
```

� ���� ������� ����� `createPrototypeBean()` � ������ `SingletonBean` ����� ���������� ����� ��������� `PrototypeBean` ��� ������ ������ `executeTask()`.

## ����������

��������� `@Lookup` ? ������ ���������� � Spring ��� ������������� �������� � ���������� �������������, ����������� ��������� ������ ������, ��������� � ���������� ����� � �������� ��������� `prototype` � ���� � �������� ��������� `singleton`, ������� ������� ������� � ����������� ����.

# 12. ����� �� �������� ��� � ����������� ����? ������?

## �������� ��������

- **������**: ����� �� �������� ��� � ����������� ����?
- **�����**: **���**, ������ �������� �������� Spring-��� � ����������� ���� � ������� ��������� Spring, ����� ��� `@Autowired`, `@Resource`, ��� `@Inject`.

## �������

- **���������� ��������� ����������**: Spring ��������� ������ � ������ ���������� IoC, � ��������� ������������ ���������� �� ������ ����������� �������. ����������� ���� ����������� ������ � �����, � �� ����������� ����������, � �� ������� �� ���������� ����� ���������� �������. ��������� ��������� ����� Spring ���������� � ��������� ���������� ����� ���������� ����, Spring �� ����� ������������� �������� ��� � ����������� ����.

- **��������� ��������� �������� ���������� (IoC)**: ��������� ������������ � ����������� ���� �������� ��������� IoC, ��������� ���������� ������������� �������� �� ������ ����������, � ���������� ��� ��������� � ���� ������ ������. ��� ������ ��� ����� ����������� � ����� ������.

## ������� ������

���� ��� �� ���������� �������� ��� � ����������� ����, ����� ������������ ��������� �������������� �������:

1. **������������� ������������ ������ � ��������� Spring**:
   � ������ ����� ������� ����������� �����, ������� ����� ������������� �������� ������������ ���� � ������� ��������� Spring.

   ```java
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.ApplicationContextAware;
   import org.springframework.stereotype.Component;

   @Component
   public class MyClass implements ApplicationContextAware {

       private static MyService myService;

       @Override
       public void setApplicationContext(ApplicationContext context) {
           myService = context.getBean(MyService.class);
       }

       public static void doSomething() {
           myService.performAction();
       }
   }
   ```

2. **������������� ������������� �������**:
   ������ ������������� ������������ ����, ����� ������� ���� ������������� � ������������ ������� ������ � ���������� ������������.

3. **��������� ����� ����������� ����**:
   � ����������� ����� ������������� ����� ������� ���������������� ���, ��������� �������� Spring. ������ ��� ������� ��������� �� ������ ���������.

   ```java
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.annotation.AnnotationConfigApplicationContext;

   public class MyClass {
       private static MyService myService;

       static {
           ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
           myService = context.getBean(MyService.class);
       }

       public static void doSomething() {
           myService.performAction();
       }
   }
   ```

## ����������

��������� Spring-���� � ����������� ���� �������� ���������� � �������� �������� IoC. ����� �������������� ������������ Spring � ������������ ������������� ���� � ������ ��� ��������� ������������. ���� �� ������������� � ����������� ���� ���-���� ���������, ����� ������������ �������� ����, ������ �� ���������� ������� ��������� ��������.

# 13. ���������� ��� ��������� @Primary � @Qualifier

## �������� ��������

- **@Primary**: ������������ ��� ��������, ��� ������ ��� �������� ���������������� ���������, ����� ���������� ��������� ���������� ��� ��������� ������������.
- **@Qualifier**: ��������� ���� �������, ����� ������ ��� ������ ���� �������, ���� ���� ��������� ����������.

## @Primary

### ��������
��������� `@Primary` ������������ ��� ��������, ��� ������ ��� ������ �������������� �� ���������, ����� ���������� ��������� ����� ������ ����. ��� ��������� �������� ���������� ��� ��������� ������������.

### ������
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    @Primary
    public MyService myPrimaryService() {
        return new MyPrimaryService();
    }

    @Bean
    public MyService mySecondaryService() {
        return new MySecondaryService();
    }
}

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MyComponent {

    private final MyService myService;

    @Autowired
    public MyComponent(MyService myService) {
        this.myService = myService; // ���������� myPrimaryService
    }
}
```
### ����������
� ���� �������, ���� � ������ `MyComponent` �� ����� �������, ����� ��������� ��� ����� ������������, Spring ������� `myPrimaryService` � �������� ����������������� ��������.

## @Qualifier

### ��������
��������� `@Qualifier` ������������ ��� �������� ����������� ����, ������� ������ ���� �������, ����� ���������� ��������� ����� ������ ����. ��� ������������ ����� ����������.

### ������
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public MyService myPrimaryService() {
        return new MyPrimaryService();
    }

    @Bean
    public MyService mySecondaryService() {
        return new MySecondaryService();
    }
}

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

@Component
public class MyComponent {

    private final MyService myService;

    @Autowired
    public MyComponent(@Qualifier("mySecondaryService") MyService myService) {
        this.myService = myService; // ���������� mySecondaryService
    }
}
```
### ����������
� ���� �������, � ������� ��������� `@Qualifier`, � ������ `MyComponent` ���� �������, ��� ����� ������������ `mySecondaryService` ������ `myPrimaryService`.

## ����������

��������� `@Primary` � `@Qualifier` ��������� ��������� ����������� ��� ��������� ������������ � Spring. `@Primary` ���������� ���������������� ���, � �� ����� ��� `@Qualifier` ��������� ���� ���������, ����� ������ ��� ����� ������������.

# 14. ��� ����������� ��������?

## ��������

� Spring ����� ������������� ����������� ���� ������, ����� ��� `int`, `boolean`, `double` � �.�., � ������� ��������� `@Value`, `@Autowired`, � ����� � �������������� ���������������� ������ ��� �������.

## ������������� ��������� @Value

### ��������
��������� `@Value` ��������� ����������� �������� ������������ ���� ��������������� �� ������������, ��������, �� ����� �������.

### ������
```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class MyComponent {

    @Value("${my.int.value}")
    private int myIntValue;

    @Value("${my.boolean.value}")
    private boolean myBooleanValue;

    public void printValues() {
        System.out.println("Integer value: " + myIntValue);
        System.out.println("Boolean value: " + myBooleanValue);
    }
}
```

### ����������
� ���� ������� �������� ��� `myIntValue` � `myBooleanValue` ������� �� ����� ������� (��������, `application.properties`):
```
my.int.value=10
my.boolean.value=true
```

## ������������� ����������������� ������

### ��������
����� ����� ������������ ���������������� ����� ��� �������� ����������� ��������.

### ������
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public int myIntValue() {
        return 10;
    }

    @Bean
    public boolean myBooleanValue() {
        return true;
    }
}

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MyComponent {

    private final int myIntValue;
    private final boolean myBooleanValue;

    @Autowired
    public MyComponent(int myIntValue, boolean myBooleanValue) {
        this.myIntValue = myIntValue;
        this.myBooleanValue = myBooleanValue;
    }

    public void printValues() {
        System.out.println("Integer value: " + myIntValue);
        System.out.println("Boolean value: " + myBooleanValue);
    }
}
```

### ����������
� ���� ������� ����������� �������� `myIntValue` � `myBooleanValue` ��������� � ���������������� ������ `AppConfig` � ����� ������������� � `MyComponent`.

## ����������

����������� ���� ������ ����� ��������������� � Spring � ������� ��������� `@Value` ��� ���������� �������� �� ������������ ��� ����� ���������������� ������, ��� �������� ������������ � �������, ���������� ���������� `@Bean`.

# 15. ��� ����������� ���������?

## ��������

� Spring ����� ������������� ��������� (��������, `List`, `Set`, `Map`) � ������� ��������� `@Autowired`, `@Value` ��� ����� ���������������� ������.

## ������������� ��������� @Autowired

### ��������
��������� `@Autowired` ��������� ������������� ���������, ������� �������� ���� ���� �� ����.

### ������
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;
import java.util.List;

@Component
public class MyComponent {

    private final List<MyService> services;

    @Autowired
    public MyComponent(List<MyService> services) {
        this.services = services;
    }

    public void executeServices() {
        for (MyService service : services) {
            service.execute();
        }
    }
}
```

### ����������
� ���� ������� `MyComponent` �������� ������ �������� `MyService`, ������� ������������� ����������� ����� ������ ���� `MyService`, ������������������� � ��������� Spring.

## ������������� ��������� @Value ��� ���������� �� ����� �������

### ��������
����� ������������ ��������� `@Value` ��� �������� ���������, ���������� � ���� ����� � ����� �������.

### ������
```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;
import java.util.Arrays;
import java.util.List;

@Component
public class MyComponent {

    @Value("${my.services}")
    private List<String> services;

    public void printServices() {
        System.out.println("Services: " + services);
    }
}
```

### ���� �������
```
my.services=Service1,Service2,Service3
```

### ����������
�������� �� �������� `my.services` ����������� �� �������� ������ �� ������ �������.

## ������������� ����������������� ������

### ��������
����� ������� ���������������� �����, ������� ���������� ��������� ��� ���.

### ������
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import java.util.Arrays;
import java.util.List;

@Configuration
public class AppConfig {

    @Bean
    public List<String> myServices() {
        return Arrays.asList("Service1", "Service2", "Service3");
    }
}

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MyComponent {

    private final List<String> services;

    @Autowired
    public MyComponent(List<String> services) {
        this.services = services;
    }

    public void printServices() {
        System.out.println("Services: " + services);
    }
}
```

### ����������
� ������ ������� ����� `myServices()` ���������� ������ �����, ������� ����� ������������� � `MyComponent`.

## ����������

� Spring ��������� ����� ������������� ����� `@Autowired`, `@Value` ��� ���������� �� ������ ������� ��� ����� ���������������� ������, ������������ ��������� ��� ����.

# 16. ���������� ��� ��������� @Conditional

## ��������

��������� `@Conditional` � Spring ������������ ��� ���������� ��������� ����� � ����������� �� ���������� ������������ �������. ��� ��������� ����� ����� ����������� �������� ����������.

## �������� �������

### �������
��������� `@Conditional` ��������� �����, ������� ��������� ��������� `Condition`. � ���� ������ ���������� ���������� ������, ������� ����� ����������� ��� �������� ����.

### ������

```java
import org.springframework.context.annotation.Condition;
import org.springframework.context.annotation.ConditionContext;
import org.springframework.context.annotation.Conditional;
import org.springframework.context.annotation.Configuration;
import org.springframework.beans.factory.annotation.Value;

@Configuration
public class AppConfig {

    @Bean
    @Conditional(WindowsCondition.class)
    public MyService myWindowsService() {
        return new WindowsService();
    }

    @Bean
    @Conditional(LinuxCondition.class)
    public MyService myLinuxService() {
        return new LinuxService();
    }
}

// ������� ��� Windows
class WindowsCondition implements Condition {
    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        String osName = System.getProperty("os.name").toLowerCase();
        return osName.contains("win");
    }
}

// ������� ��� Linux
class LinuxCondition implements Condition {
    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        String osName = System.getProperty("os.name").toLowerCase();
        return osName.contains("nux");
    }
}
```

### ����������
� ���� ������� ��������� ��� ���� ���� `MyService`, ������� ������������� � ����������� �� ������������ �������, �� ������� ����������� ����������. ���� ������� Windows, ����� ������ `WindowsService`, � ��� Linux ? `LinuxService`.

## ����������

��������� `@Conditional` ��������� ��������� ��������� ����� � Spring � ����������� �� �������� �������, ����������� �������� ������������ ����������.

# 17. ���������� ��� ��������� @Profile

## ��������

��������� `@Profile` � Spring ������������ ��� ����������� ��������, � ������� ���� ������ ���� ������������. ��� ��������� ��������� ������������ ���������� ��� ��������� ����, ����� ��� ����������, ������������ � ��������.

## �������� �������

### ����������� �������
`@Profile` ����� ���� ��������� � ������� ������������ ��� � �������, ��������� ����. ������� ����������� � ���� ����� � ����� ���� ������������ ��� ������� ����������.

### ������

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;

@Configuration
public class AppConfig {

    @Bean
    @Profile("dev")
    public MyService devService() {
        return new DevService();
    }

    @Bean
    @Profile("prod")
    public MyService prodService() {
        return new ProdService();
    }
}
```

### ����������
� ���� ������� ��������� ��� ���� ���� `MyService`, ������ �� ������� ������������ � ����������� �� ��������� �������. ���� ������� "dev" �������, ����� ������ `DevService`, � ���� "prod" ? `ProdService`.

### ��������� �������
������� ����� ���� ������������ � ������� ���������� ��������� ������, ���������� ��������� ��� ���������������� ������. ��������, � `application.properties` ����� �������:

```properties
spring.profiles.active=dev
```

## ����������

��������� `@Profile` ��������� ��������� �������������� ���������� � ����������� �� ����� ����������, ��� �������� ��������� � ������������� ���������� � ��������� ��������.

# 18. ���������� ��� ��������� ���� ����, ��������� @PostConstruct � @PreDestroy()

## ��������

��������� ���� ���� � Spring �������� � ���� ��������� ������, ������� � ��� �������� � ���������� ������������. Spring ������������� ��������� ��� ���������� ���� ������ ����� ���������, ����� ��� `@PostConstruct` � `@PreDestroy`.

## ��������� ���� ����

1. **��������**: ��� ��������� � ���������������� ����������� Spring.
2. **���������**: � �������� ��������� ����� ���� �������� ������������.
3. **�������������**: ����������� ������ �������������, ���� ��� ����������.
4. **�������������**: ��� �������� ��� ������������� ���������.
5. **�����������**: ��������� ����������� �������, ��������� � �����.

## ��������� @PostConstruct

### ��������
��������� `@PostConstruct` ��������� �� �����, ������� ������ ���� �������� ����� �������� ���� � ���������� �������� ������������, �� ����� ���, ��� ��� ����� �������� ��� �������������.

### ������

```java
import javax.annotation.PostConstruct;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    @PostConstruct
    public void init() {
        System.out.println("��� MyBean ���������������.");
    }
}
```

### ����������
� ���� ������� ����� `init()` ����� ������ ����� �������� `MyBean`, �������� ��������� �������������� ��������� ��� �������������.

## ��������� @PreDestroy

### ��������
��������� `@PreDestroy` ��������� �� �����, ������� ������ ���� �������� ����� ������������ ����. ��� ��������� ����������� ������� ��� ��������� ����������� ��������.

### ������

```java
import javax.annotation.PreDestroy;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    @PreDestroy
    public void cleanup() {
        System.out.println("��� MyBean ����� ���������.");
    }
}
```

### ����������
� ���� ������� ����� `cleanup()` ����� ������ ����� ������������ `MyBean`, ��� ��������� ��������� ����� ����������� ��������, ����� ��� �������� ���������� ��� ������������ ��������.

## ����������

��������� `@PostConstruct` � `@PreDestroy` ������������� ������� ������ ���������� �������������� � �������� �������� ����� � Spring, ������� ������ � ��������� ������ �����.

# 19. ���������� ��� ������ �����? ����� ����� ������������ �� ���������? ��� ���������� � Spring 5?

## ��������

������ ����� � Spring ���������� ������� ��������� � ��������� ���� ��������, ����������� ����������� Spring. ������ �������� ����������, ������� ����������� ���� ����� ������� � ����� ��� ����� ������� � ����������.

## �������� ������ �����

1. **Singleton**:
   - **��������**: ��� ����� �� ���������. � ���������� ��������� ������ ���� ��������� ����, ������� ������������ ��� ������ �������.
   - **������**: 
     ```java
     @Component
     public class MySingletonBean {
         // Singleton bean
     }
     ```

2. **Prototype**:
   - **��������**: ��� ������ ������� ��������� ������� ����� ��������� ����.
   - **������**:
     ```java
     @Component
     @Scope("prototype")
     public class MyPrototypeBean {
         // Prototype bean
     }
     ```

3. **Request**:
   - **��������**: ������� ��� �� ������ HTTP-������ (�������� ������ � ���-�����������).
   - **������**:
     ```java
     @Component
     @Scope("request")
     public class MyRequestBean {
         // Request scope bean
     }
     ```

4. **Session**:
   - **��������**: ������� ��� �� ������ HTTP-������ (����� �������� ������ � ���-�����������).
   - **������**:
     ```java
     @Component
     @Scope("session")
     public class MySessionBean {
         // Session scope bean
     }
     ```

5. **Global Session**:
   - **��������**: ������� ��� �� ������ ���������� HTTP-������ (�������� ������ � ���������).
   - **������**:
     ```java
     @Component
     @Scope("globalSession")
     public class MyGlobalSessionBean {
         // Global session scope bean
     }
     ```

## ����� �� ���������

�� ���������, ���� �� ������� �����, ������������ **Singleton**.

## ��������� � Spring 5

� Spring 5 �������� ��������� ����������� ����������������, ��� ����� �������� �� ������. ������ ����� ������������ ����� ������, ����� ��� `@Scope("webflux")` ��� ���������� ����������. ����� ��������� ����������� ���������� ���������� � ��������� ������ ����� � ��������� ����������� ����������������.

## ����������

������ ����� � Spring ��������� �������������� �� �������� � �������������, ��� ����� ��� ���������� ��������� � ����������� ������������������ ����������.

# 20. ���������� ��� ��������� @ComponentScan

## ��������

��������� `@ComponentScan` � Spring ������������ ��� ��������������� ������ � ����������� ����� � ��������� ����������. ��� ��������� ��������� ���������� Spring, ��� ������ ������, ���������� �����������, ������ ��� `@Component`, `@Service`, `@Repository` � `@Controller`.

## �������� ��������������

1. **����� �������**:
   - `@ComponentScan` ��������� ������� ���� ��� ��������� ������� ��� ������������. �� ��������� Spring ��������� �����, � ������� ��������� �����, ���������� ���������� `@ComponentScan`.

   ```java
   @Configuration
   @ComponentScan(basePackages = "com.example.service")
   public class AppConfig {
       // ������������ ����������
   }
   ```

2. **���������� �������**:
   - ����� ��������� ������������ ������ �� ������������ � ������� �������� `excludeFilters`.

   ```java
   @ComponentScan(
       basePackages = "com.example",
       excludeFilters = @ComponentScan.Filter(type = FilterType.ASSIGNABLE_TYPE, classes = MyExcludedClass.class)
   )
   public class AppConfig {
   }
   ```

3. **���������� �������**:
   - � ������� `includeFilters` ����� ��������� �������������� ������� ��� ��������� ������� � ������������.

   ```java
   @ComponentScan(
       basePackages = "com.example",
       includeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = MyCustomAnnotation.class)
   )
   public class AppConfig {
   }
   ```

## ����������

`@ComponentScan` ����� ������������ � ���������������� �������, ����� ��������� ������� ��������� � ��������� ���������� ����, ������������ ��� ����������� �����. ��� �������� ������� � ������� ����������� � ���������� �����������.

## ����������

��������� `@ComponentScan` ��������� ���������� ��������� ��������� ������ � ����������� ����� � ���������� Spring, ������� ����������� � ���������� ����.

# 21. ��� ������ �������� � ������������? ���������� ��� ��������� @Transactional

## ��������

Spring ������������� ������ ����������� ��� ���������� ������������, �������� ������������� ����� �������������� ������� ���������� � ������������ ����������� ������. �������� ������������ ��� ������ � ������������ � Spring �������� ��������� `@Transactional`.

## �������� �������������� ��������� @Transactional

1. **����������� ������ ����������**:
   - ��������� `@Transactional` ���������, ��� ����� ��� ����� ������ ����������� � ������ ����������. ���� ����� ���������� �������, ���������� ����� ������������� (commit). � ������ ���������� ���������� ����� �������� (rollback).

   ```java
   @Service
   public class UserService {
       @Transactional
       public void createUser(User user) {
           userRepository.save(user);
           // �������������� ��������, ������� ����� ������ ����������
       }
   }
   ```

2. **���������� �� ������ ������ ��� ������**:
   - `@Transactional` ����� ����������� ��� � ��������� �������, ��� � �� ����� ������. ���� ����������� � ������, ��� ��� ������ ���������� ��� ���������, ���� �� ������� ����.

3. **��������� ��������� ����������**:
   - ��������� ��������� ����������� ���������, ����� ��� ������� ��������, ��� ��������� ����������, timeout � ������.

   ```java
   @Transactional(isolation = Isolation.READ_COMMITTED, rollbackFor = Exception.class)
   public void updateUser(User user) {
       userRepository.update(user);
   }
   ```

4. **���������� � Spring � JTA**:
   - Spring ������������ ��� ��������� ���������� (��������, � ������� JDBC), ��� � �������������� ���������� ����� JTA. ��� ����� ���������� ��������� ��������������� �������� ����������.

## ��� �������� ���������� ������������

- **Proxy-��������������� ������**:
  Spring ���������� AOP (Aspect-Oriented Programming) ��� ��������� ��������� ����������. ����� �����, ���������� `@Transactional`, ����������, Spring ������� ������, ������� ��������� ������� � ����������� ����������.

- **��������� ����������**:
  �� ��������� Spring ���������� ���������� ������ ��� ������������� ����������� (unchecked exceptions). ��� ������ ����� ���������� ��������� ����� ���� ��������� � ������� ���������� ���������.

## ����������

��������� `@Transactional` � Spring ����������� �������� ������ � ������������, �������� ������������� ��������������� �� ������-������, �� ���������� � ���������� ���������� ������������ � �� ����������.

# 22. ����� ���� �������� � @Transactional?

��������� `@Transactional` � Spring ����� ��������� ���������, ����������� ����������� ��������� ����������. ��� �������� �� ���:

## ��������

1. **propagation**:
   - ���������, ��� ������ ����� ���� ���������� � ��������� ��� ������������ ����������.
   - ������� ��������:
     - `REQUIRED`: ���������� ������� ����������, ���� ��� ����������, ��� ������� �����.
     - `REQUIRES_NEW`: ������ ������� ����� ����������.
     - `NESTED`: ������� ��������� ����������, ���� ���� ��������.

2. **isolation**:
   - ���������� ������� �������� ����������, �������� �� ��������� ���������, ��������� ������� ������������.
   - ������� ��������:
     - `READ_UNCOMMITTED`
     - `READ_COMMITTED`
     - `REPEATABLE_READ`
     - `SERIALIZABLE`

3. **timeout**:
   - ������������� ����� � ��������, ����� �������� ���������� ����� ������������� ���������, ���� ��� ��� �� �����������.

4. **readOnly**:
   - ���������, �������� �� ���������� ������ ��� ������. ��� ����� ������ �������������� ������������������.
   - �������:
     - `true`: ���������� ������ ��� ������.
     - `false`: ���������� ��� ������.

5. **rollbackFor**:
   - ����������, ����� ���������� ������ �������� ����� ����������. ����� ��������� ������ ���������� ��� ������ ���� �������.

6. **noRollbackFor**:
   - ���������, ����� ���������� �� ������ �������� ����� ����������.

## ������ �������������

```java
@Transactional(
    propagation = Propagation.REQUIRED,
    isolation = Isolation.READ_COMMITTED,
    timeout = 30,
    readOnly = false,
    rollbackFor = {CustomException.class}
)
public void performTransaction() {
    // ������ ����������
}
```

## ����������

�������� ��������� `@Transactional` ������������� �������� � ���������� ������������ � ��������� ������������� ��������� ��������� � ������������ � ������������ ������-������.

# 23. ��� @Transactional �������� ��� �������?

��������� `@Transactional` � Spring ������������ ���������� ������������ � �������� ��������� �������:

## 1. ������-������

����� �� ����������� ��������� `@Transactional`, Spring ������� ������-������ ��� ������ ����. ��� ����� ���� ���� JDK ������������ ������ (���� ��� ����� ��������� ���������), ���� CGLIB ������ (���� �� �� ��������� ����������). 

## 2. Aspect-Oriented Programming (AOP)

Spring ���������� ������ ��������-���������������� ���������������� (AOP) ��� ���������� ������������. ����� �����, ���������� `@Transactional`, ����������, ������ ������������� ���� ����� � ��������� �������������� ��������, ��������� � ����������� ������������.

## 3. ������ ����������

��� ����� � ����� � ���������� `@Transactional` ������:
- ���������, ���������� �� �������� ����������.
- ���� ���������� �� ����������, ��������� �����.
- ���� ���������� ��� �������, ������������ �������.

## 4. ���������� ������

����� ������ ���������� ���������� ������� �����. � �������� ���������� ������ ����� ��������, ������������ � ����� ������, ����� �������� � ����������.

## 5. ���������� ����������

����� ���������� ������ ������:
- ���� ����� ���������� �������, ���������� ����������.
- ���� ��������� ���������� (���� ��� ������������� �������� ������), ���������� ������������.

## 6. ��������� ������

�� ������ ���������, ����� ���������� �������� �����, ��������� �������� `rollbackFor` � `noRollbackFor` � ��������� `@Transactional`.

## ������

```java
@Transactional
public void performTransaction() {
    // ������, ������� ����� ��������� � ������ ����������
}
```

## ����������

����� �������, `@Transactional` ��������� ������������ � ������� ������-�������� � AOP, ����������� �������������� ������, ���������� � ����� ���������� � ����������� �� ���������� ���������� �������.

# 24. ��� ������ �������� N+1 � �������������� @Transactional?

�������� N+1 ���������, ����� ��� ������� ������ �� ���� ������ ����������� ���� ������ ��� �������� �������� � N �������� ��� ��������� ���������. ��� ����� �������� � ������������� �������� ������������������. ������� �������� ����� ���� ���������� � ������� `@Transactional` � ��������� � ����������� ����������� �������� ������.

## 1. ������������� `@Transactional`

������������ ������ � ��������� `@Transactional` ��������� ���������� ����������� ������ � �������� �������� N+1 �� ���� ���������� ���������� �������� � ���� ������.

### ������

```java
@Service
public class OrderService {

    @Autowired
    private OrderRepository orderRepository;

    @Transactional
    public List<Order> fetchOrdersWithItems() {
        return orderRepository.findAll(); // ������������ �������� ��������� ���������
    }
}
```

## 2. ������������� `FetchType.EAGER`

�� ������ ���������� ��������� �������� ��� ��������� ��������� � `EAGER`, ����� ��� ����������� ������ � �������� ���������.

### ������

```java
@Entity
public class Order {

    @OneToMany(fetch = FetchType.EAGER)
    private List<Item> items;
}
```

������ ������������� `EAGER` ����� �������� � �������� ���������� ������, ���� ��������� �������� �� ������ �����.

## 3. ������������� `JOIN FETCH`

����� ����������� ������ ������� �������� N+1 ? ������������� JPQL ��� Criteria API � `JOIN FETCH`. ��� ��������� ��������� ��������� �������� �� ���� ������.

### ������

```java
public interface OrderRepository extends JpaRepository<Order, Long> {

    @Query("SELECT o FROM Order o JOIN FETCH o.items")
    List<Order> findAllWithItems();
}
```

## 4. �������������� �������

� ����������� �� ���������, �� ������ ������������� ��������� �������, ����� �������������� �������� ������ � �������� ���������� ��������.

## ����������

������������� ��������� `@Transactional` � ��������� � ����������� ����������� �������� ������, ������ ��� `JOIN FETCH`, �������� ���������� ������ �������� N+1, ����������� ���������� �������� � ���� ������ � ������� ������������������ ����������.

# 25. ���������� ��� ��������� @Controller � @RestController. ��� ��� ����������?

## 1. ��������� @Controller

`@Controller` ? ��� ���������, ������������ � Spring ��� ����������� ���������� �����������, ������� ������������ HTTP-������� � ���������� ������������� (views). ������ ��� ��������� ����������� � MVC-�����������, ��� ���������� ��������� �������� ������ ����� ������� � ��������������.

### ������

```java
@Controller
public class MyController {

    @GetMapping("/greeting")
    public String greeting(Model model) {
        model.addAttribute("message", "Hello, World!");
        return "greeting"; // ���������� ��� �������������
    }
}
```

## 2. ��������� @RestController

`@RestController` �������� ������������������ ������� `@Controller`. ��� ������������ ��� �������� RESTful ���-��������, ������� ���������� ������ ��������������� � ������� JSON ��� XML. ��� ��������� ������������� ��������� `@ResponseBody`, ��� ��������, ��� ������������ �������� ������� ����� ������������� � JSON � ���������� � HTTP-������.

### ������

```java
@RestController
public class MyRestController {

    @GetMapping("/greeting")
    public Greeting greeting() {
        return new Greeting("Hello, World!"); // ���������� ������, ������� ����� ������������ � JSON
    }
}
```

## 3. �������� �������

- **������� ������**: 
  - `@Controller` ���������� ������������� (��������, JSP, Thymeleaf).
  - `@RestController` ���������� ������ (��������, JSON ��� XML).

- **�������������� ������������**:
  - `@Controller` ������� ������������� `@ResponseBody`, ����� ������� ������ � ���� JSON ��� XML.
  - `@RestController` ������������� ��������� `@ResponseBody` �� ���� �������.

## ����������

������������� `@Controller` � `@RestController` ������� �� ���� ����������: ��� MVC-���������� ����� ������������ `@Controller`, � ��� �������� RESTful API ? `@RestController`.
