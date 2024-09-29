# 1. ��� ����� �������� �������� (IoC) � ��������� ������������ (DI)? ��� ��� �������� ����������� � Spring?

**�������� �������� (IoC)** - ��� ������� ����������������, ��� ������� ���������� ������� ��������� ���������� �������� ���������� ��� ����������, � �� ������������ ����� �����. � ��������� ��������-���������������� ���������������� ��� ��������, ��� ������ �� ������� ���� ����������� ��������������, � �������� �� �����.

**��������� ������������ (Dependency Injection, DI)** - ��� ���� �� �������� ���������� �������� IoC. DI ��������� ���������� ����������� (��������, �������, �� ������� ������� ������ ������) ����� �����������, ������ ��� ���� ������.

**��� ��� ����������� � Spring?**

Spring - ��� ���������, ������� ������ ���������� ������� IoC � ������������� ��������� ��������� ��� ��������� ������������:

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

IoC (Inversion of Control) ��������� - ��� ����������� ��������� ���������� Spring, ������� ��������� ���������, ���������� � ����������� ��������� ������ �������� (�����). �� �������� ����������� ����� ������������, ��� ��������� ����������� ������� �������� ����������.

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
**BeanFactory** - ��� ��������� � Spring, ������� ������������� �������� ���������� IoC ����������, ������� �������� � ���������� ������. �� ������������ ������� �������������, ��� ��������, ��� ������� (����) ��������� ������ �����, ����� ��� ������������� �����.

#### ������ ������������� BeanFactory:

```java
Resource resource = new ClassPathResource("applicationContext.xml");
BeanFactory factory = new XmlBeanFactory(resource);

MyBean myBean = (MyBean) factory.getBean("myBean");
```

### ApplicationContext
**ApplicationContext** - ��� ����� �������������� ��������������, ����������� `BeanFactory`. �� ������������� �������������� �����������, ����� ���:
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
   - `@Service` - ������������ ��� �������, �������������� ����� �������.
   - `@Repository` - ������������ ��� �������, ����������� ���� ������������.
   - `@Controller` - ������������ ��� ������������ � Spring MVC.

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
  
- **������������� � ������������**: `@Component` ����������� � ����� �������, � �� ����� ��� `@Bean` - � ������� ������ ���������������� �������.

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

- **���� ����������**: `@Service` ������������ ��� �������, ������� ��������� ������-������, � `@Repository` - ��� �������, ������� ��������� �������� � ������.
  
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
  - `@Autowired` �������� ����������� ��� Spring, ����� ��� `@Inject` - ��� ����������� ��������� Java.

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

- **���������� ��� ������������� `prototype` � `singleton`**: ���� � ��� ���� `singleton`-���, ������� ������� �� `prototype`-����, � ��� �����, ����� ������ ����� ������ �������� ����� ��������� `prototype`-����, ��������� `@Lookup` - ��������� �������.

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

��������� `@Lookup` - ������ ���������� � Spring ��� ������������� �������� � ���������� �������������, ����������� ��������� ������ ������, ��������� � ���������� ����� � �������� ��������� `prototype` � ���� � �������� ��������� `singleton`, ������� ������� ������� � ����������� ����.

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
� ���� ������� ��������� ��� ���� ���� `MyService`, ������� ������������� � ����������� �� ������������ �������, �� ������� ����������� ����������. ���� ������� Windows, ����� ������ `WindowsService`, � ��� Linux - `LinuxService`.

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
� ���� ������� ��������� ��� ���� ���� `MyService`, ������ �� ������� ������������ � ����������� �� ��������� �������. ���� ������� "dev" �������, ����� ������ `DevService`, � ���� "prod" - `ProdService`.

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

����� ����������� ������ ������� �������� N+1 - ������������� JPQL ��� Criteria API � `JOIN FETCH`. ��� ��������� ��������� ��������� �������� �� ���� ������.

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

`@Controller` - ��� ���������, ������������ � Spring ��� ����������� ���������� �����������, ������� ������������ HTTP-������� � ���������� ������������� (views). ������ ��� ��������� ����������� � MVC-�����������, ��� ���������� ��������� �������� ������ ����� ������� � ��������������.

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

������������� `@Controller` � `@RestController` ������� �� ���� ����������: ��� MVC-���������� ����� ������������ `@Controller`, � ��� �������� RESTful API - `@RestController`.

# 26. ��� ����� ResponseEntity?

`ResponseEntity` ? ��� ����������� ����� � Spring Framework, ������� ������������ ��� �������� HTTP-������� � ������� �����������. �� ��������� �������������� �� ������ ���� ������, �� � ���������, � ����� ��������� ��� HTTP.

## �������� ����������� ResponseEntity:
- **���������� ����� ������**: ��������� ������� ������� ������, ������� ����� ������������� � JSON ��� XML (��� ������ �������).
- **���������� �������� ������**: ����� ������� ��������� ��� HTTP (��������, 200 OK, 404 Not Found).
- **���������� �����������**: ����� ������������� ���������������� HTTP-��������� (��������, Content-Type, Location).

## ������ ������������� ResponseEntity

### 1. ������� ������������� ��� �������� ������ � �������

```java
@RestController
public class MyController {

    @GetMapping("/greeting")
    public ResponseEntity<String> greeting() {
        return new ResponseEntity<>("Hello, World!", HttpStatus.OK);
    }
}
```

� ���� ������� `ResponseEntity` ���������� ������ "Hello, World!" � HTTP �������� `200 OK`.

### 2. �������� ����������

```java
@GetMapping("/greeting-with-headers")
public ResponseEntity<String> greetingWithHeaders() {
    HttpHeaders headers = new HttpHeaders();
    headers.add("Custom-Header", "foo");

    return new ResponseEntity<>("Hello, World!", headers, HttpStatus.OK);
}
```

����� �� ��������� ���������������� ��������� `Custom-Header` � �����.

### 3. ������ � �������� � ��������

```java
@GetMapping("/greeting-object")
public ResponseEntity<Greeting> greetingObject() {
    Greeting greeting = new Greeting("Hello, World!");
    return ResponseEntity.status(HttpStatus.CREATED).body(greeting);
}
```

���� ������ ���������� ������ `Greeting` � ������������� ������ `201 Created`.

## ����������

`ResponseEntity` ���� ������������ ������ �������� ��� HTTP-�������: ��������� ������� ����, ��������� � ������ ������. ��� �������� ���������� ��� �������� RESTful ���-��������, ����� ��������� ������ ���������� ��������.

# 27. ��� ����� ViewResolver?

## ��������:
`ViewResolver` ? ��� ��������� � Spring MVC, ������� �������� �� ���������� ������������� (views) �� �����, ������������� ������������. ����� ���������� ���������� ��� �������������, `ViewResolver` ������� ��������������� ������������� � �������� ��� � ������� ���������� �������.

## �������� ����:
1. **InternalResourceViewResolver**:
   ������������ ��� JSP ������. �� ����� ����� ������������� �� �������� JSP �����, ����������� � ������������ ����������.
   
   ������ ��������� � `application.properties`:
   ```properties
   spring.mvc.view.prefix=/WEB-INF/views/
   spring.mvc.view.suffix=.jsp
   ```
   � ���� �������, ���� ���������� ���������� ������ `"home"`, `ViewResolver` ����������� ���� `/WEB-INF/views/home.jsp`.

2. **ThymeleafViewResolver**:
   ������������ ��� ���������� � �������������� Thymeleaf, ������� ������������ ��� ���������� HTML-�������.

3. **FreeMarkerViewResolver** � **VelocityViewResolver**:
   ��� ���������� � ������� ���������������, ������ ��� FreeMarker � Velocity.

## ������ ���������:
� `Java Config`:
```java
@Bean
public InternalResourceViewResolver viewResolver() {
    InternalResourceViewResolver resolver = new InternalResourceViewResolver();
    resolver.setPrefix("/WEB-INF/views/");
    resolver.setSuffix(".jsp");
    return resolver;
}
```
����� ����������� ������� � ������� ��� �������������.

## ����:
`ViewResolver` ��������� ������������ �������� ������ ������������ �� ���������� �������� �������������. ��� ������ ��� ������������ ����� ������������� � ����������� �� ��������� ����������.

# 28. ��� ���������� Model, ModelMap � ModelAndView?

## 1. **Model**
`Model` ? ��� ���������, ������� ������������ ��� �������� ������ �� ����������� � �������������. �� ��������� ��������� �������� (������), ������� ����� �������� � ������� ��� ����������. ����� ������������ � ������� ����������� ��� ��������.

### ������ �������������:
```java
@GetMapping("/home")
public String home(Model model) {
    model.addAttribute("message", "Welcome to the homepage!");
    return "home";
}
```
� ������ ������� � ������������� `"home"` ���������� ������� `"message"`.

## 2. **ModelMap**
`ModelMap` ? ��� �����, ������� ��������� ��������� `Map` � ������������ ��� �������� ��������� ������. � ������� �� `Model`, �� �������� ����������� ����������� � ��������� �������� � ���������� ����� ������ `Map` (`put`, `get`, `remove` � �.�.).

### ������ �������������:
```java
@GetMapping("/home")
public String home(ModelMap modelMap) {
    modelMap.addAttribute("message", "Welcome to the homepage!");
    return "home";
}
```
����� ���������� ��������� ���������� ��� ��, ��� � � `Model`, �� ����� ������������ ������ `Map` ��� ����������� �������.

## 3. **ModelAndView**
`ModelAndView` ? ��� �����, ������� ���������� ��� ������ ������, ��� � ������������� (view). �� ��������� ������������ ���������� ��� ������������� � �������� � ���� ������. ������������ � ������������ ��� ����� ������������ ���������� �����������.

### ������ �������������:
```java
@GetMapping("/home")
public ModelAndView home() {
    ModelAndView mav = new ModelAndView("home");
    mav.addObject("message", "Welcome to the homepage!");
    return mav;
}
```
����� ��������� ������ `ModelAndView`, ��������������� ������������� `"home"` � ����������� ������� `"message"`.

## �������� �������:
- **Model** ? ���������, ������������ ��� �������� ������ �� ����������� � �������������. ���� ����� ����������� � ������� �����������.
- **ModelMap** ? ���������� ���������� `Map`, ������� ��������� �������� � ���������� ������ ����� ������ `Map`.
- **ModelAndView** ? ���������� ��� ������ (������), ��� � ������������� (view), �������� ����������� ���������� ����� ���.

����� �������, ���� ��������� ������ �������� ������ � �������������, ���� ������������ `Model` ��� `ModelMap`. ���� ����� ��������� � �������, � �������������� ������������, ��������������� ������������ `ModelAndView`.

# 29. ���������� ��� ������� Front Controller, ��� �� ���������� � Spring?

## ������� Front Controller
**Front Controller** ? ��� ����������� ������ ��������������, ������� ������������ ��� ��������� ���� �������� � ���������� ����� ������ ����������. � ����������� ���-���������� �� ������ ����������� ������ ����� ��� ���� �������� � ������, ����� ���������� ���������� ������ ���������� ��� ��� ���� ������.

### �������� ������� Front Controller:
- ��������� ��� �������.
- ����������, ����� ��������� (��� ����������) ����� ������������ ������.
- ��������� ��������� ��������� ��������, ������� ��������������, �����������, ����������� � ������ �������, ������� ����� ����������� �� ���� ��������.
  
### ������������:
- ���������������� ��������� ��������.
- ��������� ���������� ���������������, ������������, ���������� ������ � ������ ����� �����.
- ����� ������������ ������ �������� ��� ���� ��������.

## ���������� Front Controller � Spring
� Spring Framework ������� **Front Controller** ���������� ����� ��������� **`DispatcherServlet`**, ������� ������������ ��� HTTP-������� � ���������� �� �� ��������������� �����������.

### ��� �������� `DispatcherServlet`:
1. **��������� �������:** ��� �������� HTTP-������� ������������ �� `DispatcherServlet`, ������� ������ ���� ������ ����� ����� � ����������.
   
2. **����� �����������:** `DispatcherServlet` ���������� **HandlerMapping** ��� ����������� �����������, ������� ����� ������������ ������, ����������� �� URL, HTTP-������ � ������ ����������.

3. **��������� �������:** ����� ���� ��� ���������� ���������� ��� ������, �� ������������ ������. ��� ����� ���� ������, ��������������, ��������, ��� `@Controller` � `@RequestMapping`.

4. **������������ ������:** ����� ��������� ������� ���������� �������� ������ � �������������. ��� ����� ���� HTML-��������, JSON-�����, ��� ����� ������ ������.

5. **�������� ������:** `DispatcherServlet` �������� ����� ������� ������� (�������� ��� ������� �������).

### ������ ������ Front Controller � Spring:
```java
// ����������, �������������� �������
@Controller
public class HomeController {

    @GetMapping("/home")
    public String homePage(Model model) {
        model.addAttribute("message", "Welcome to the homepage!");
        return "home"; // ���������� ��� �������������
    }
}
```

### ������ ����������:
- **`DispatcherServlet`** ? Front Controller, ������� ��������� ������� � ���������� �� � ������ �����������.
- **`HandlerMapping`** ? ���������, ������� �������� `DispatcherServlet` �������� ������ ���������� ��� ��������� �������.
- **`ViewResolver`** ? �������� �� ����������� �������������, ������� ����� ����������� � ����� �� ������.

### ��� `DispatcherServlet` �������������:
� ������������ Spring ����� ��������� `DispatcherServlet` ����� XML ��� Java Config.

#### Java-based ������������:
```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Bean
    public DispatcherServlet dispatcherServlet() {
        return new DispatcherServlet();
    }
}
```

#### XML-������������:
```xml
<servlet>
    <servlet-name>dispatcher</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>dispatcher</servlet-name>
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

## ����������
`DispatcherServlet` ? ��� ���������� �������� Front Controller � Spring, ������� �������� �� ������������� ���� �������� � ������ ������������ � ��������� �� � ������� ��������� �����������, ����� ��� `HandlerMapping` � `ViewResolver`.

# 30. ���������� ��� ������� MVC, ��� �� ���������� � Spring?

## ������� MVC (Model-View-Controller)
**MVC (Model-View-Controller)** ? ��� ������������� ������, ������� ��������� ������ ���������� �� ��� ��������������� �����:

1. **Model** ? ������ ������, �������� �� ������ ���������� � ������ � �������. ��� �� ������� �� ������������� � �����������.
2. **View** ? �������������, �������� �� ����������� ������ ������������. ��������������� ������ � ������� ��� ����������� ����������.
3. **Controller** ? ����������, �������� �� ��������� ���������������� ��������, ��������� ������ � �������������, ��������� ������� ������ ����� ����.

### ������������ MVC:
- ������ ���������� ���������������.
- �������� ������������ ��������� �����������.
- ��������� �������� � ������������� ����������.

## ���������� MVC � Spring
Spring Framework ��������� MVC ����� ������ **Spring Web MVC**, ������� ������������ ��� ����������� ���������� ��� ������ �� ������� MVC.

### �������� ���������� Spring MVC:
1. **Model** ? ������������ ��������� Java (POJO), ������� �������� ������-������ � ������ ����������.
2. **View** ? ������ ��� JSP, Thymeleaf, ��� ������ ��������� ������, ������� ��������� HTML-������ �� ������ ������ �� ������.
3. **Controller** ? ��� Java-����� � ��������, ������� ������������ ��� ��������� HTTP-�������� � ��������������� � ������� � ��������������.

### ��� �������� Spring MVC:

1. **������ �������:** ������ ���������� HTTP-������ � �������.
2. **`DispatcherServlet` ��� Front Controller:** ������ �������� �� `DispatcherServlet`, ������� ������������ ��� �������.
3. **��������� ������� ������������:** `DispatcherServlet` ���������� ���������� � ������� `HandlerMapping`, ������� �������� �� ������ ������, � �������� ������ � ���� ����������.
4. **���������� ������:** ���������� ������������ ������, ��������� ������ (���� ����������), � �������� ������ ��� ����������� �������������.
5. **����� �������������:** `ViewResolver` �������� ���������� ������������� �� ������ ������, ������������ ������������.
6. **����� ������������:** ������������� (��������, JSP ��� Thymeleaf) ���������� HTML � ���������� ��� ������� ������� � �������� ������.

### ������ ����:
```java
// ����������
@Controller
public class HomeController {

    @GetMapping("/home")
    public String home(Model model) {
        // ��������� ������ �������
        model.addAttribute("message", "Welcome to the homepage!");
        return "home"; // ��� ������������� (��������, home.jsp ��� home.html)
    }
}
```

### ���������� Spring MVC:
- **`DispatcherServlet`** ? ��� Front Controller, ������� ������������ ��� �������� �������.
- **`Controller`** ? �����, ������� ������������ �������, ��������������� � ������� � �������� ������������� ��� ������.
- **`Model`** ? ������ ������, ������� ����� �������� ������������� ��� �����������.
- **`View`** ? ��������� �����, ��������� ������ ������������.
- **`ViewResolver`** ? �������� �� ����� ����������� ������������� ��� ���������� ������.

### ������ ��������� Spring MVC:
#### ������������ � �������������� Java Config:
```java
@Configuration
@EnableWebMvc
@ComponentScan(basePackages = "com.example")
public class WebConfig implements WebMvcConfigurer {

    @Bean
    public ViewResolver viewResolver() {
        InternalResourceViewResolver resolver = new InternalResourceViewResolver();
        resolver.setPrefix("/WEB-INF/views/");
        resolver.setSuffix(".jsp");
        return resolver;
    }
}
```

#### ������������ � �������������� XML:
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/mvc 
           http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- �������� ��������� ��������� @Controller -->
    <mvc:annotation-driven/>

    <!-- ���������� ������������ JSP ������������� -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

    <!-- ��������� ���������� ��� ������������ -->
    <context:component-scan base-package="com.example.controllers"/>
</beans>
```

### ������ ������ Spring MVC:
1. ������ ���������� ������ `GET /home`.
2. `DispatcherServlet` �������� ������ � ����� ����������� `home()`.
3. ���������� ��������� ��������� � ������ � ���������� ������ `"home"`, ����������� �� ������������� `home.jsp`.
4. `ViewResolver` ������� ���� `WEB-INF/views/home.jsp` � �������� ��� � ������� �� ������.
5. HTML-�������� ������������ �������.

## ����������
Spring MVC ��������� ������ �������������� MVC � �������������� `DispatcherServlet` � �������� Front Controller. ��� ��������� ����� ��������� ������ ��������� ��������, ���������� ������� � ��������������, ����������� ��������, ������������� � ��������� ���������� ���-����������.

# 31. ��� ����� ���? ��� ����������� � �������?

## ��� (��������-��������������� ����������������)

**��� (Aspect-Oriented Programming)** ? ��� ��������� ����������������, ������� ��������� �������� �������� ���������������� �� �������� ������ ����������. �������� ���������������� ? ��� ����� ������, ������� ����� ����������� � ������ ������ �������, ����� ���:

- �����������
- ������������
- ���������� ������������
- �����������

��� ��������� ��������������� ��� ���������������� � ����������� ����� ����, ���������� ���������, � �������� �� � �������� ������ ���������. ��� �������� �������� ����������� � ��������� ������������� ����.

## �������� ������� ���:

1. **������ (Aspect)** ? ������, ���������� �������� ������, ����� ��� ����������� ��� ���������� ������������.
2. **����� ���������� (Join Point)** ? ����� ���������� ���������, ���� ����� ���� ������� ������ (��������, ����� ������).
3. **����� (Advice)** ? ��������, ����������� �������� � ���������� ����� ����������. ������ ����� ���� ��������� ��, ����� ��� ������ ����� ����������.
4. **���� (Pointcut)** ? ���������, ������� ����������, � ����� ������ ���������� ����������� �������.
5. **��������� (Weaving)** ? ������� ���������� �������� � ������� �������. ��� ����� ����������� �� ����� ����������, �������� ��� ���������� ���������.

## ���������� ��� � Spring

� Spring Framework ��� ����������� � ������� ������������� ��������. Spring ���������� **������������ ������**, ����� �������� ������� � �������, ��� ��������� ��� ��������� ��������� ���� ��������� ���������������� � ��������� ���������� ����������.

### �������� ���������� Spring AOP:

1. **�������** ��������� � �������������� ���������, ����� ��� `@Aspect`.
2. **������ (Advices)** ������������ � ������� ���������, ����� ��� `@Before`, `@After`, `@Around`, � �.�.
3. **����� (Pointcuts)** ���������, � ����� ������� ��� ������� ����� ��������� �������, � �������������� ���������� ��������� ��� ������ ����� ����������.
4. **������������** ���������� � ������� Java-����, XML ��� ���������.

### ������ ���������� ��� � Spring:

1. **���������� ����������� Spring AOP:**
   
   Maven:
   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-aop</artifactId>
   </dependency>
   ```

2. **�������� �������:**

   ������, ������� �������� ������ ������� �� �� ����������:
   ```java
   import org.aspectj.lang.annotation.Aspect;
   import org.aspectj.lang.annotation.Before;
   import org.springframework.stereotype.Component;

   @Aspect
   @Component
   public class LoggingAspect {

       @Before("execution(* com.example.service.*.*(..))")
       public void logBeforeMethod() {
           System.out.println("����� ����� ������...");
       }
   }
   ```

   � ���� �������:
   - ��������� `@Aspect` ���������, ��� ��� ������.
   - ��������� `@Before` ����������, ��� ����� `logBeforeMethod()` ����� ������ ����� ������ ������� � ����� ������ ������ ������ `com.example.service`.
   - ��������� `execution(* com.example.service.*.*(..))` ? ��� ����, ������� ��������� �� ��� ������ � ������� `com.example.service`.

3. **������ ������������� ������� � �������:**

   ```java
   @Service
   public class ExampleService {

       public void performAction() {
           System.out.println("����������� ��������...");
       }
   }
   ```

4. **��������� ������:**
   
   ����� ���������� ����� `performAction()`:
   ```java
   exampleService.performAction();
   ```
   ����� ����� �����:
   ```
   ����� ����� ������...
   ����������� ��������...
   ```

### ���� ������� � Spring AOP:

1. **`@Before`** ? ��������� ����� ����� ������ ����������.
2. **`@After`** ? ��������� ����� ����� ���������� ����� ����������, ���������� �� ���������� (����� ��� ����������).
3. **`@AfterReturning`** ? ����������� ����� ��������� ���������� ������.
4. **`@AfterThrowing`** ? �����������, ���� ����� �������� ����������.
5. **`@Around`** ? ����������� ���������� ������, �������� ��������� ������ �� � ����� ���������� ������, � ����� �������������� ��� ���������.

### ������ ������������� `@Around`:
```java
@Around("execution(* com.example.service.*.*(..))")
public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
    long start = System.currentTimeMillis();
    
    Object proceed = joinPoint.proceed(); // ���������� ������
    
    long executionTime = System.currentTimeMillis() - start;
    System.out.println(joinPoint.getSignature() + " �������� �� " + executionTime + " ��");
    
    return proceed;
}
```

### ����� ���:
- �������� ���������� �������� ������, �� ����� �� �������� ���.
- �������� ��������� ��� ���������� ��������.
- �������� ���������� � ��������� ����, ������� �������� ������ �� ������-������.

### ����������� Spring AOP:
- �������� ������ � ������, ������������ Spring (�� ����� ����������� � ��-managed ��������).
- ���������� ������, ��� ��������� ��������� �������, �������� � ������� ������� ��������.

## ����������
��� � Spring �������� ��������� �������� ���������������� � ������-������ ����������. ��� �������� ����������, ������������ � ��������� ����, ����� ���������� ����� ��������� � ������.

# 32. � ��� ������� ����� Filters, Listeners and Interceptors?

## Filters (�������)
**�������** ? ��� �������, ������� ������������� HTTP-������� � HTTP-������ � ���-���������� �� ������ ��������� �� ����, ��� ��� ��������� �������� ��� ����� ��� ���������.

### �������� �������������� ��������:
- ������������ ������� � ������ �� � ����� ������ ��������.
- ������������ ��� �����������, ��������������, �����������, ������ ������ � ������ �����, ��������� � ��������� � ��������.
- ������� �� ������� �� ���������� ���������, ��� ����� ����������� �� ���� �������� ��� ������ � ������������ URL-��������.

### ������ ������������� Filter:
```java
@WebFilter(urlPatterns = "/api/*")
public class LoggingFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        System.out.println("������ ���������� � �������");
        chain.doFilter(request, response); // �������� ������� ������
        System.out.println("����� ���������� � �������");
    }
}
```
- � ���� ������� ������ ����� ������������� ��� �������, ������������ �� URL, ������������ � `/api`.

## Listeners (���������)
**���������** ? ��� �������, ������� ��������� �� ������������ ������� � ��������� ���-����������. ��� "�������" ��������� �������, ����� ��� ������ � ��������� ����������, �������� ��� ����������� ������, � ��������� �� ���.

### �������� �������������� ����������:
- ����������� ������� �� ������ ����������, ������ � ��������.
- ����������� ��� ����� �����, ��� ���������� ��������, ����������� ������� � ������������� ��������.

### ������ ������������� Listener:
```java
@WebListener
public class SessionListener implements HttpSessionListener {

    @Override
    public void sessionCreated(HttpSessionEvent se) {
        System.out.println("������ �������: " + se.getSession().getId());
    }

    @Override
    public void sessionDestroyed(HttpSessionEvent se) {
        System.out.println("������ ����������: " + se.getSession().getId());
    }
}
```
- � ���� ������� `SessionListener` ����� ����������� �� ������� �������� � ����������� ������.

## Interceptors (������������)
**������������** ? ��� ����������, ������� ������������� ������ ������� � ����������, �������� � Spring Framework. ��� �������� �� ������ ������-������ � ������������� ������ ������������ ��� ��������. 

### �������� �������������� �������������:
- ������������ ������ ������� �� � ����� ���������� ����������� (� ��������� Spring MVC).
- ����������� ��� ���������, ��������������, �����������, ��������� �������� ��� �������, � ������ �����.
- ����� ��������������� �������� �� ��������� � ���������, �������� �� ������ ������ ������� � ����������.

### ������ ������������� Interceptor � Spring:
```java
public class LoggingInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
            throws Exception {
        System.out.println("������ ���������� ����� ���������� ������������");
        return true; // ���������� ����������
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)
            throws Exception {
        System.out.println("������ ��������� ������������, ����� ���������");
    }
}
```
- ����� `LoggingInterceptor` ������������� ������� �� � ����� ������ ������� �����������.

### ������� ����� Filters, Listeners � Interceptors:
1. **������� ������:**
   - **Filters**: �������� �� ������ HTTP-�������� � �������, ����������� �� ���� ��������/�������.
   - **Listeners**: ��������� �� ������� ���������� ����� ����������, ������ ��� ��������.
   - **Interceptors**: �������� �� ������ ������ ������� � ���������� (�������� � ������������ ��� ��������).

2. **������� ����������:**
   - **Filters**: ������������ ��� ��������� �������� � ������� HTTP.
   - **Listeners**: ��� ���������� ��������� ���������� ����� (��������, ��������/����������� ������).
   - **Interceptors**: ��� ��������� ������� ������� � ���������� ������ ��/����� �� ����������.

3. **�������� �������������:**
   - **Filters** ����������� � �������� � �������-����������� (Java EE, Spring).
   - **Listeners** �������� �� ������ �������-����������� ��� ������������ �������.
   - **Interceptors** ����������� � �������� � Spring Framework ��� ��������� ������-������.

# 33. ����� �� �������� � ������� ���� � ��� �� �������� ��������� ���? ���?

��, ����� �������� ���� � ��� �� �������� ��������� ��� � HTTP-�������. ��� �������� ��� ��� GET, ��� � ��� POST-��������. � ������ GET-�������, ��������� ���������� � ������ ������� (query string) ����� URL, � � POST-������� ? ����� ���� �������.

## GET-������

� GET-������� ����� �������� ��������� �������� ��� ������ ���������, ������ �������� ��� ��������� ���:

```http
GET /example?param=value1&param=value2&param=value3 HTTP/1.1
```

����� `param` ? ��� ��� ���������, � `value1`, `value2`, `value3` ? ��� ��������. ��� ���� ������ ����� ���������� ��� ��� ������ ��������.

### ��������� � Spring:
���� �� ����������� Spring MVC ��� ��������� ��������, ����� ������� ��������� �������� ��������� � ������� ������� ��� ������:

```java
@GetMapping("/example")
public String handleRequest(@RequestParam("param") List<String> params) {
    System.out.println(params); // [value1, value2, value3]
    return "Handled";
}
```

� ���� ������� ��� �������� ��������� `param` ����� ������� � ������ `params`.

## POST-������

� POST-������� ��������� ����� ����� ���� �������� ��������� ���. ���� ��������� ���������� � ������� `application/x-www-form-urlencoded`, �� ��� ����� ���� ���������:

```http
POST /example HTTP/1.1
Content-Type: application/x-www-form-urlencoded

param=value1&param=value2&param=value3
```

Spring ����� ���������� ��� �������� ���������� GET-�������:

```java
@PostMapping("/example")
public String handlePost(@RequestParam("param") List<String> params) {
    System.out.println(params); // [value1, value2, value3]
    return "Handled";
}
```

����� �������, �� ������ ���������� ���� � ��� �� �������� ��������� ��� � �������, � ������ ������ �������� � ���������� ��� �������� ��� ���������.

# 34. ��� �������� Spring Security? ��� ����������������? ����� ���������� ������������?

## ��� �������� Spring Security?

Spring Security ? ��� ������ � ������ ������������� ��������� ��� ����������� ������������ ����������, ���������� �� Spring. �� ������������ ��������� �������:

1. **��������������**: �������� ����������� ������������, ��������, ����� ��� ������������ � ������.
2. **�����������**: ����������� ����, ����� �������� ��� ������� �������� ������������.
3. **������ �� ����**: ������ �� CSRF, XSS � ������ �����������.
4. **��������� ��������� ����������**: ��������� OAuth2, OpenID, SAML � ������.

## ��� ���������������� Spring Security?

### 1. ���������� ������������

��� ������ �������� ����������� ����������� � ��� ������. ��������, ��� Maven ��� �����:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

### 2. ������������ ������������

�������� ����� ������������, ����������� `WebSecurityConfigurerAdapter`, � �������������� ����� `configure`.

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/", "/public/**").permitAll() // ������ ��� ����
                .anyRequest().authenticated() // ��������� ������� ������� ��������������
                .and()
            .formLogin() // ��������� ����� �����
                .loginPage("/login")
                .permitAll()
                .and()
            .logout()
                .permitAll();
    }
}
```

### 3. ��������� ��������������

�� ������ ��������� �������������� �������������, ��������, � �������������� in-memory ���������:

```java
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
    auth.inMemoryAuthentication()
        .withUser("user").password("{noop}password").roles("USER")
        .and()
        .withUser("admin").password("{noop}admin").roles("ADMIN");
}
```

� ������ ������� ������������ `{noop}` ��� ��������, ��� ������ �� ������������.

### 4. ����������

Spring Security ���������� ��������� �������� �����������:

- **AuthenticationManager**: ��������� ��������� ��������������.
- **UserDetailsService**: ��������� ���������������� ������ �� ����� ������������.
- **GrantedAuthority**: ������������ ����������, ��������������� ������������.
- **SecurityContextHolder**: ������ ���������� � ������� ��������� ������������.

## ����������

����� �������, Spring Security ���������� ������ ��������� ��� ��������� ������������ ����������. �� ������ ��������� ���������������, ������������ � ������� �� ����������� � ������� ������������, ���������� �� ���������� � ��������� �������.

# 35. ��� ����� Spring Boot? ����� � ���� ������������? ��� ���������������? ��������.

## ��� ����� Spring Boot?

Spring Boot ? ��� ���������� ���������� Spring, ������� �������� ������� ���������� � ��������� ���������� �� ��� ������. �� ������������� ������������� ��� ��������� ����������� Spring � ������������� ������������� ����������, ����������� ������������� ������ ���������. Spring Boot ��������� ������������� ������ ��������� ����������, �� ����� ����� �� ������� ���������.

## ������������ Spring Boot

1. **������� ���������**: ��������� �������������� ������������, ������������ ����� ��������������� �� ������ ����������, �� ���������� � ��������� Spring.
  
2. **���������� �������� ����������**: Spring Boot �������� ���������� ������� (��������, Tomcat, Jetty), ��� ��������� ������������� � ����������� ���������� ��� ������������� �� ������� �������.

3. **������� ������������**: Spring Boot ���������� �������� ������������, ������� ������������� ��������� ����������� ������ ���������.

4. **��������**: �� ������ ����������� ���������� �� ���� �������������, �������� ����������� � ������������.

5. **���������� �������������**: Spring Boot ������������ �������, ��� ��������� ����� ��������� �������������� ��� ������ ���� (����������, ������������, ��������).

6. **Actuator**: ���������� ������� ��� ����������� � ���������� ����������� (��������, �������, �������� ���������).

## ��� ��������������� Spring Boot?

### 1. �������� �������

��� ������ �� ������ ������� ������ Spring Boot � ������� [Spring Initializr](https://start.spring.io/). ����� ����� ������� �����������, ������� ��� �����, � ������� ZIP-����� � ��������.

### 2. ��������� �������

����������� ��������� ������� ��������:

- `src/main/java`: ��� ������ ����������.
- `src/main/resources`: �������, ����� ��� `application.properties` ��� `application.yml`.
- `src/test/java`: �����.

### 3. �����������

�� ������ ��������� ����������� � ���� `pom.xml` (��� Maven) ��� `build.gradle` (��� Gradle). ��������, ��� Maven:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

### 4. ������������ ����������

������������ ����� �������� � ������ `application.properties` ��� `application.yml`. ������:

```properties
server.port=8080
spring.application.name=MyApplication
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=secret
```

### 5. �������� ����� ����������

�������� �������� ����� � ���������� `@SpringBootApplication`. ��� ����� ����� ����� � ���� ����������.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

### 6. �������� �����������

�������� ����������, ����� ������������ HTTP-�������:

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```

### 7. ������ ����������

��������� ���� ����������, ��������� IDE ��� ������� Maven/Gradle. ���������� ����� �������� �� ������ `http://localhost:8080/hello`.

## ����������

Spring Boot ����������� �������� ������� ���������� ���������� �� ������ Spring, ��������� �������������� ������������, ���������� ������� � ���������� �������������. ��� ��������� ������������� ��������������� �� ���������� ������-������, � �� �� ������������ ��������������.

# 36. ��� ����� Spring Data JPA?

## �����������

Spring Data JPA ? ��� ����� ���������� Spring, ������� �������� ������ � ������ � ������ � ������ ������ ����� Java Persistence API (JPA). ��� ������������� ������� ������ �������������� � ������������ ������ ������, �������� ������������� ������ ��������� �����������, ������� ����� ��������� �������� CRUD (��������, ������, ����������, ��������) ��� ������������� ������ ����� ���������� ����.

## �������� ����������

1. **�����������**: Spring Data JPA ��������� ��������� ���������� ������������, ������� ������������� ��������� ����������� ������ ������� � ������. ��������:

    ```java
    import org.springframework.data.jpa.repository.JpaRepository;

    public interface UserRepository extends JpaRepository<User, Long> {
        List<User> findByLastName(String lastName);
    }
    ```

    � ���� ������� `UserRepository` ������������� ������ ��� ������ � ��������� `User` ��� ������������� ������ ����������.

2. **��������**: ������, �������������� ������� ���� ������. ������ �������� ������������ � �������������� JPA ���������, ����� ��� `@Entity` � `@Table`.

3. **��������� �������**: Spring Data JPA ��������� ��������� ������� �� ������ ���� �������. ��������, ����� `findByFirstNameAndLastName` ������������� ������� SQL-������ ��� ��������� ������������� �� ����� � �������.

4. **������������**: Spring Data JPA ������������ ������������, ��� ��������� ������� ������������ �������.

5. **��������� � ����������**: ���������� ����������� ��� ������ � ���������� � ����������� ������.

## ������������ Spring Data JPA

1. **���������� ����**: ���������� ������ ���������� ����, ������������ ��� ������� � ������.
2. **�������������� ���������� ������������**: ������� �������� ������������ ��� ��������� ����������.
3. **��������**: ��������� ��������� �������� � ������������.
4. **���������� � Spring**: ������ ���������� � ������� ������������ Spring, ������ ��� Spring MVC.

## ������������ Spring Data JPA

### 1. �����������

�������� ����������� ����������� � ���� `pom.xml` (Maven) ��� `build.gradle` (Gradle):

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

### 2. ���������

������������ � `application.properties` ��� `application.yml`:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=create
spring.jpa.show-sql=true
```

### 3. �������� ��������

�������� ��������:

```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String firstName;
    private String lastName;

    // ������� � �������
}
```

### 4. ������������� �����������

����������� ����������� � �������:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    public List<User> findAll() {
        return userRepository.findAll();
    }

    public User save(User user) {
        return userRepository.save(user);
    }
}
```

## ����������

Spring Data JPA ����������� �������� ������ � ������ ������ � ����������� �� Spring, �������� ������������� �������������� �� ������-������, � �� �� ������� ������� � ������.

# 37. ��� ������� ����������� � ������ ��?

## ��������

� ����������� ����������� ����� ��������� ������������� �������� � ����������� ������ ������ ������������. ��� ����� ���� ���������� ��� ���������� ������ �� �������������� �������, ���������� � ���������� ��������� ��� ������������� ������ ����� ��� ������ (��������, ����������� � NoSQL). Spring Framework ������������� ������ ��������� ��� ��������� � ���������� ����������� ����������� ������ (DataSources) � ����� ����������.

## ���� ��� ����������� � ������ �� � Spring

### 1. ���������� ������������

������� ���������� �������� ����������� ����������� ��� ������ ���� ������, � ������� �� ���������� ��������. �����������, �� ������ ������������ � PostgreSQL � MySQL. ��� ����� � `pom.xml` (Maven) ��� `build.gradle` (Gradle) �������� ��������������� �����������:

**Maven (`pom.xml`):**
```xml
<dependencies>
    <!-- Spring Data JPA -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    
    <!-- PostgreSQL Driver -->
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>
    
    <!-- MySQL Driver -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <scope>runtime</scope>
    </dependency>
    
    <!-- �������������� ����������� �� ������������� -->
</dependencies>
```

**Gradle (`build.gradle`):**
```groovy
dependencies {
    // Spring Data JPA
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    
    // PostgreSQL Driver
    runtimeOnly 'org.postgresql:postgresql'
    
    // MySQL Driver
    runtimeOnly 'mysql:mysql-connector-java'
    
    // �������������� ����������� �� �������������
}
```

### 2. ������������ ���������� ������

��������� ��������� ����������� � ������ ���� ������ � ������ ������������ `application.properties` ��� `application.yml`.

**������ `application.properties`:**
```properties
# ��������� ��� ������ ���� ������ (PostgreSQL)
spring.datasource.first.jdbc-url=jdbc:postgresql://localhost:5432/firstdb
spring.datasource.first.username=user1
spring.datasource.first.password=pass1
spring.datasource.first.driver-class-name=org.postgresql.Driver
spring.jpa.first.hibernate.ddl-auto=update
spring.jpa.first.show-sql=true

# ��������� ��� ������ ���� ������ (MySQL)
spring.datasource.second.jdbc-url=jdbc:mysql://localhost:3306/seconddb
spring.datasource.second.username=user2
spring.datasource.second.password=pass2
spring.datasource.second.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.second.hibernate.ddl-auto=update
spring.jpa.second.show-sql=true
```

**������ `application.yml`:**
```yaml
spring:
  datasource:
    first:
      jdbc-url: jdbc:postgresql://localhost:5432/firstdb
      username: user1
      password: pass1
      driver-class-name: org.postgresql.Driver
    second:
      jdbc-url: jdbc:mysql://localhost:3306/seconddb
      username: user2
      password: pass2
      driver-class-name: com.mysql.cj.jdbc.Driver

  jpa:
    first:
      hibernate:
        ddl-auto: update
      show-sql: true
    second:
      hibernate:
        ddl-auto: update
      show-sql: true
```

### 3. �������� ���������������� ������� ��� ������ ���� ������

�������� ��������� ������ ������������ ��� ������ ���� ������, ��������� `DataSource`, `EntityManagerFactory`, `TransactionManager` � �����������.

**������ ������������ ��� ������ ���� ������ (PostgreSQL):**

```java
package com.example.config;

import javax.persistence.EntityManagerFactory;
import javax.sql.DataSource;

import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.boot.orm.jpa.EntityManagerFactoryBuilder;
import org.springframework.boot.autoconfigure.jdbc.DataSourceBuilder;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Primary;
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;
import org.springframework.orm.jpa.JpaTransactionManager;
import org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean;
import org.springframework.transaction.PlatformTransactionManager;

@Configuration
@EnableJpaRepositories(
    basePackages = "com.example.repository.first",
    entityManagerFactoryRef = "firstEntityManagerFactory",
    transactionManagerRef = "firstTransactionManager"
)
public class FirstDbConfig {

    @Primary
    @Bean(name = "firstDataSource")
    @ConfigurationProperties(prefix = "spring.datasource.first")
    public DataSource firstDataSource() {
        return DataSourceBuilder.create().build();
    }

    @Primary
    @Bean(name = "firstEntityManagerFactory")
    public LocalContainerEntityManagerFactoryBean firstEntityManagerFactory(
            EntityManagerFactoryBuilder builder,
            @Qualifier("firstDataSource") DataSource dataSource) {
        return builder
                .dataSource(dataSource)
                .packages("com.example.entity.first")
                .persistenceUnit("firstDb")
                .build();
    }

    @Primary
    @Bean(name = "firstTransactionManager")
    public PlatformTransactionManager firstTransactionManager(
            @Qualifier("firstEntityManagerFactory") EntityManagerFactory firstEntityManagerFactory) {
        return new JpaTransactionManager(firstEntityManagerFactory);
    }
}
```

**������ ������������ ��� ������ ���� ������ (MySQL):**

```java
package com.example.config;

import javax.persistence.EntityManagerFactory;
import javax.sql.DataSource;

import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.boot.orm.jpa.EntityManagerFactoryBuilder;
import org.springframework.boot.autoconfigure.jdbc.DataSourceBuilder;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;
import org.springframework.orm.jpa.JpaTransactionManager;
import org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean;
import org.springframework.transaction.PlatformTransactionManager;

@Configuration
@EnableJpaRepositories(
    basePackages = "com.example.repository.second",
    entityManagerFactoryRef = "secondEntityManagerFactory",
    transactionManagerRef = "secondTransactionManager"
)
public class SecondDbConfig {

    @Bean(name = "secondDataSource")
    @ConfigurationProperties(prefix = "spring.datasource.second")
    public DataSource secondDataSource() {
        return DataSourceBuilder.create().build();
    }

    @Bean(name = "secondEntityManagerFactory")
    public LocalContainerEntityManagerFactoryBean secondEntityManagerFactory(
            EntityManagerFactoryBuilder builder,
            @Qualifier("secondDataSource") DataSource dataSource) {
        return builder
                .dataSource(dataSource)
                .packages("com.example.entity.second")
                .persistenceUnit("secondDb")
                .build();
    }

    @Bean(name = "secondTransactionManager")
    public PlatformTransactionManager secondTransactionManager(
            @Qualifier("secondEntityManagerFactory") EntityManagerFactory secondEntityManagerFactory) {
        return new JpaTransactionManager(secondEntityManagerFactory);
    }
}
```

**����������:**

- **@Primary**: ���������, ��� ������ ��� �������� ��������, ���� Spring �� ����� ����������, ����� ��� ������������. ��� �����, ����� ��������� `DataSource` ���������� � ���������.
  
- **@ConfigurationProperties**: ��������� �������� �� ���������������� ������ � ������.

- **@EnableJpaRepositories**: ��������� �����, ��� ��������� ����������� ��� ������ ���� ������, � ����� ������ �� `EntityManagerFactory` � `TransactionManager`.

### 4. �������� ��������� � ������������

��������� �������� � ����������� �� �������, ��������������� ������ ���� ������.

**������ �������� ��� ������ ���� ������ (PostgreSQL):**

```java
package com.example.entity.first;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class FirstEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // ������� � �������
}
```

**������ ����������� ��� ������ ���� ������:**

```java
package com.example.repository.first;

import org.springframework.data.jpa.repository.JpaRepository;
import com.example.entity.first.FirstEntity;

public interface FirstEntityRepository extends JpaRepository<FirstEntity, Long> {
    // �������������� ������ ������� ��� �������������
}
```

**������ �������� ��� ������ ���� ������ (MySQL):**

```java
package com.example.entity.second;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class SecondEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String description;

    // ������� � �������
}
```

**������ ����������� ��� ������ ���� ������:**

```java
package com.example.repository.second;

import org.springframework.data.jpa.repository.JpaRepository;
import com.example.entity.second.SecondEntity;

public interface SecondEntityRepository extends JpaRepository<SecondEntity, Long> {
    // �������������� ������ ������� ��� �������������
}
```

### 5. ������������� ������������ � ��������

�������� �������, ������� ����� ������������ ��������������� ����������� ��� ������ ���� ������.

**������ ������� ��� ������ ���� ������:**

```java
package com.example.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import com.example.repository.first.FirstEntityRepository;
import com.example.entity.first.FirstEntity;

import java.util.List;

@Service
public class FirstEntityService {

    @Autowired
    private FirstEntityRepository firstEntityRepository;

    public List<FirstEntity> getAllFirstEntities() {
        return firstEntityRepository.findAll();
    }

    public FirstEntity saveFirstEntity(FirstEntity entity) {
        return firstEntityRepository.save(entity);
    }
}
```

**������ ������� ��� ������ ���� ������:**

```java
package com.example.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import com.example.repository.second.SecondEntityRepository;
import com.example.entity.second.SecondEntity;

import java.util.List;

@Service
public class SecondEntityService {

    @Autowired
    private SecondEntityRepository secondEntityRepository;

    public List<SecondEntity> getAllSecondEntities() {
        return secondEntityRepository.findAll();
    }

    public SecondEntity saveSecondEntity(SecondEntity entity) {
        return secondEntityRepository.save(entity);
    }
}
```

### 6. ����������� ��� ��������� ��������

�������� �����������, ������� ����� ������������ ��������������� ������� ��� �������������� � ������� ������ ������.

**������ �����������:**

```java
package com.example.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;
import com.example.service.FirstEntityService;
import com.example.service.SecondEntityService;
import com.example.entity.first.FirstEntity;
import com.example.entity.second.SecondEntity;

import java.util.List;

@RestController
@RequestMapping("/api")
public class MyController {

    @Autowired
    private FirstEntityService firstEntityService;

    @Autowired
    private SecondEntityService secondEntityService;

    // ������ ��� ������ ���� ������
    @GetMapping("/first")
    public List<FirstEntity> getAllFirstEntities() {
        return firstEntityService.getAllFirstEntities();
    }

    @PostMapping("/first")
    public FirstEntity createFirstEntity(@RequestBody FirstEntity entity) {
        return firstEntityService.saveFirstEntity(entity);
    }

    // ������ ��� ������ ���� ������
    @GetMapping("/second")
    public List<SecondEntity> getAllSecondEntities() {
        return secondEntityService.getAllSecondEntities();
    }

    @PostMapping("/second")
    public SecondEntity createSecondEntity(@RequestBody SecondEntity entity) {
        return secondEntityService.saveSecondEntity(entity);
    }
}
```

### 7. �������������� ���������

#### a. ��������� ����������

���� �� ����������� ����������, ���������, ��� ������ `TransactionManager` �������� � ���������������� `EntityManagerFactory`.

**������ ������������� ��������� `@Transactional` � ���������� ���������� ����������:**

```java
package com.example.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;
import com.example.repository.first.FirstEntityRepository;
import com.example.entity.first.FirstEntity;

@Service
public class FirstEntityService {

    @Autowired
    private FirstEntityRepository firstEntityRepository;

    @Transactional("firstTransactionManager")
    public FirstEntity saveFirstEntity(FirstEntity entity) {
        return firstEntityRepository.save(entity);
    }
}
```

#### b. ������������� �������� Spring

����� ������������ ������� ��� ���������� ������������ ��� ������ � ����������� �� ����� ���������� (��������, ����������, ������������, ��������).

**������:**

```java
@Configuration
@EnableJpaRepositories(
    basePackages = "com.example.repository.first",
    entityManagerFactoryRef = "firstEntityManagerFactory",
    transactionManagerRef = "firstTransactionManager"
)
@Profile("dev")
public class FirstDbDevConfig {
    // ������������ ��� ����������
}
```

### 8. ������������ �����������

����� ��������� ���������� �������������� ����������� � ������ ���� ������, ������ � �������� �������� ����� ��������������� �����������.

**������ �����:**

```java
package com.example;

import com.example.entity.first.FirstEntity;
import com.example.entity.second.SecondEntity;
import com.example.repository.first.FirstEntityRepository;
import com.example.repository.second.SecondEntityRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

@Component
public class DataLoader implements CommandLineRunner {

    @Autowired
    private FirstEntityRepository firstEntityRepository;

    @Autowired
    private SecondEntityRepository secondEntityRepository;

    @Override
    public void run(String... args) throws Exception {
        FirstEntity first = new FirstEntity();
        first.setName("First DB Entry");
        firstEntityRepository.save(first);

        SecondEntity second = new SecondEntity();
        second.setDescription("Second DB Entry");
        secondEntityRepository.save(second);

        System.out.println("������ ��������� � ����� ����� ������.");
    }
}
```

## ����������

��������� ����������� � ���������� ����� ������ � Spring ������� ������� ���������� ������������, ��������� � ������������ ��� ������ ���� ������. ������������� ��������� `@Configuration`, `@EnableJpaRepositories`, `@Primary`, `@Qualifier` � ���������� ����������� ������� ��������� ���������� ��������� ����������� ����������� ������ � ����� ����������. ����� ������ ������������ ��������, ���������������� � �������� ��������� ���������� ��� ������ � ���������� ������ ������.

# 38. ���������� ��� ��������� @Query

## ��������

��������� `@Query` � Spring Data JPA ������������� ������������� ����������� ���������� ����������� ������� ��� ������� ������������. ��� ��������� ������ ��� JPQL (Java Persistence Query Language) �������, ��� � �������� SQL-�������, ������������ �������� ��� ��������� ������ �� ���� ������.

## �������� ����������� ��������� @Query

1. **����������� ���������������� JPQL-��������**:
   - ��������� ������ ������� �������, ������� �� ����� ���� ������������� ������������� �� ������ ����� ������.
   
2. **������������� �������� SQL-��������**:
   - � ������� �������� `nativeQuery = true` ����� ������ ������� �� ������ SQL, ��� ������� ��� ����������� ��� ������������� ������������� ������� ����.

3. **�������� ����������**:
   - ��������� ����������� � ����������� ���������� ��� �������� ������ � �������.

4. **��������� ����������� ������**:
   - ����� ������������ ��� �������� ���������� � �������� � ������� ��������� `@Modifying`.

## ������� ������������� @Query

### 1. ���������������� JPQL-������

�����������, � ��� ���� �������� `User`:

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String firstName;
    private String lastName;
    
    // ������� � �������
}
```

**������ ����������� � �������������� JPQL-�������:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    
    @Query("SELECT u FROM User u WHERE u.lastName = :lastName")
    List<User> findUsersByLastName(@Param("lastName") String lastName);
}
```

**����������:**
- ��������� `@Query` �������� JPQL-������, ������� �������� ������������� �� �������.
- ��������� `@Param` ��������� �������� ������ � ���������� �������.

### 2. �������� SQL-������

**������ ����������� � �������������� ��������� SQL-�������:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    
    @Query(
        value = "SELECT * FROM users WHERE last_name = :lastName",
        nativeQuery = true
    )
    List<User> findUsersByLastNameNative(@Param("lastName") String lastName);
}
```

**����������:**
- ������� `nativeQuery = true` ���������, ��� ������ ������� �� ������ SQL.
- ������������ �������� ������� `users`.

### 3. ����������� ���������

**������ ������������� ����������� ����������:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    
    @Query("SELECT u FROM User u WHERE u.firstName = ?1 AND u.lastName = ?2")
    List<User> findUsersByFullName(String firstName, String lastName);
}
```

**����������:**
- � JPQL-������� ������������ ����������� ��������� `?1` � `?2`, ������� ������������� ������ � ������ ���������� ������ ��������������.

### 4. �������������� �������

��� ���������� �������� ���������� ��� �������� ���������� ������������ ��������� `@Modifying` ������ � `@Query`.

**������ ���������� ������:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    
    @Modifying
    @Transactional
    @Query("UPDATE User u SET u.firstName = :firstName WHERE u.id = :id")
    int updateUserFirstName(@Param("id") Long id, @Param("firstName") String firstName);
}
```

**����������:**
- ��������� `@Modifying` ���������, ��� ������ �������� ������.
- ��������� `@Transactional` ���������� ��� ���������� �������� ������.

### 5. ������������� `@Query` � `Pageable`

Spring Data JPA ������������ ��������� � ���������� ��� ������������� ��������� `@Query`.

**������:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    
    @Query("SELECT u FROM User u WHERE u.lastName = :lastName")
    Page<User> findUsersByLastName(@Param("lastName") String lastName, Pageable pageable);
}
```

**����������:**
- ����� ���������� ������ `Page<User>`, ������� �������� ���������� � �������� �����������.
- �������� `Pageable` ��������� �������� ����� ��������, ������ � ����������.

## ������ � ������������

1. **����������� ����������� ��������� ��� ��������� ����������**:
   - ����������� ��������� ������ ������� ����� ��������� � ��������� �� ���������.
   
2. **��������� ������������� �������� ��������, ���� ��� ��������**:
   - JPQL-������� ����� ������ � ���������� �� ���������� ����. ����������� �������� ������� ������ ��� �������������.
   
3. **����������� `@Modifying` � `@Transactional` ��� ���������� ��������**:
   - ��� ���� ��������� Spring �� ������ ��������� ���������� ���������� �������.
   
4. **������������� ������� ��� ������������������**:
   - ������ ���������� ���������� �������� � ����������� ������� � ���� ������ ��� ��������� ������������������.

## ����������

��������� `@Query` �������� ������ ������������ � Spring Data JPA, ������� ��������� ��������� ������ � ���������������� ������� � ���� ������. ��� �������� ������ � �������, ������������ ����������� ������ ��� JPQL, ��� � �������� SQL-�������, � ����� ������������ ��������� ���� ���������� � ��������. ���������� ������������� `@Query` ������������ ��������� ������������������ � �������� ���������� ���������� �� ������ Spring.

# 39. ��� ����� ������������ ��������� (projection interface)?

## ��������

������������ ��������� (projection interface) � Spring Data JPA ��������� �������� � ���������� ������ ������������ ���� ��������� ������ ����� ��������. ��� �������, ����� ����� �������� ������ � ������ ������, ������ ����� ������������ ������ � ������� ������������������. 

## �������� ���� ��������

1. **�������� �������� (Closed Projections)**:
   - ���������� ������ ����, ��������� � ����������. ��� ���� ������ ����� ��������� � ������� ����� ��������.
   
2. **�������� �������� (Open Projections)**:
   - ��������� ������������ ������ � �������, ������������ ����������� �������� �� ������ ����� ��������.

3. **������������ �������� (Dynamic Projections)**:
   - ��������� �������� ������ �������� � ����������� �� ���������, ��� �������� ������� ��� ������ � �������������.

## ������� ������������� ��������

### 1. �������� ��������

��������, � ��� ���� �������� `User`:

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String firstName;
    private String lastName;
    
    // ������� � �������
}
```

**������������ ���������:**

```java
public interface UserProjection {
    String getFirstName();
    String getLastName();
}
```

**�����������:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<UserProjection> findAllProjectedBy();
}
```

**����������:**
- ��������� `UserProjection` �������� ������ ����������� ����, `firstName` � `lastName`.
- ����� `findAllProjectedBy()` � ����������� ���������� ������ ��������, ��������������� ��������, ������ �������� `User`.

### 2. �������� ��������

**������ ���������� � �������:**

```java
public interface UserOpenProjection {
    String getFirstName();
    String getLastName();
    
    default String getFullName() {
        return getFirstName() + " " + getLastName();
    }
}
```

**����������:**
- � ���� ������� �������� ����� `getFullName()`, ������� ���������� ��������� ��������, ������������ ��� � �������.

### 3. ������������ ��������

**����������� � ������������ ���������:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    <T> List<T> findByLastName(String lastName, Class<T> type);
}
```

**������������� ������������ ��������:**

```java
List<UserProjection> users = userRepository.findByLastName("Smith", UserProjection.class);
```

**����������:**
- ����� `findByLastName` ����� ���������� �������� � ����������� �� ����������� ������ ��������.
- ��� ��������� ����������� ��������, ����� �������� ������������ � ������ ���������� ������.

## ������������ ������������� ��������

1. **��������� ������������������**:
   - ������������ ������ ����������� ����, ��� ������� ���������� ������������ ������ � �������� ���������� ��������.
   
2. **��������� ����**:
   - ������������ ���������� ��������� ����� ��������������� ������ ��� ������������� ��� �������� �������������� DTO (Data Transfer Objects).

3. **��������**:
   - ������������� �������� � ������������ �������� ��������� ����� ����� �������� � �������, �������� ������ � ������� ��� ������� ������ �������� � ����������� �� ���������.

## ����������

������������ ���������� ? ��� ������� ���������� � Spring Data JPA, ����������� ���������� �������� � �������� ������, ������� ����������� ������ ������������ ����������. ��� ������������ ��� �������, ��� � ������������ ��������, ������� ������������������ � �������� ������ � �������.

# 40. ��� ���������� �� ����������� ����������� �����?

## ��������

����������� ����������� ���������, ����� ��� ��� ����� Spring-���� ������� ���� �� �����, ��� ������� ��������� ���� ������������. ��� �������� � ������� ��� �������� ����� � ������������� ���������. � Spring Framework ������������� ��������� ������� ������� ���� ��������.

## ������� ���������� ����������� �����������

### 1. **������������� ��������� `@Lazy`**

��������� `@Lazy` ��������� ����������� �������� ���� �� ������� ��� ������������ �������������. ��� ����� ������ ��������� ����������� �����������.

**������:**

```java
@Component
public class A {
    private final B b;

    public A(@Lazy B b) {
        this.b = b;
    }
}

@Component
public class B {
    private final A a;

    public B(A a) {
        this.a = a;
    }
}
```

**����������:**
- � ������ `A` ����������� �� `B` ����������� � ���������� `@Lazy`, ��� ��������� Spring �������� �������� `B` �� �������, ����� ��� ������� �����������.

### 2. **��������� ����� �������**

������ ��������� ������������ ����� ����������� ����� ������������ �������, ����� Spring ������� ������ ����, � ����� ��������� �����������.

**������:**

```java
@Component
public class A {
    private B b;

    @Autowired
    public void setB(B b) {
        this.b = b;
    }
}

@Component
public class B {
    private A a;

    @Autowired
    public void setA(A a) {
        this.a = a;
    }
}
```

**����������:**
- Spring ������� ������� ��� ����, � ����� ��������� ����������� ����� �������, �������� ����.

### 3. **������������� ����������� ��� �������**

��� �������������� ����������� ����������� ����� �������� �����������, �������� ������ ����� ���������� ��� �������. ��� ��������� ������� ����������� ����� ������.

**������:**

```java
public interface ServiceA {
    void performAction();
}

@Component
public class A implements ServiceA {
    private final B b;

    public A(B b) {
        this.b = b;
    }

    @Override
    public void performAction() {
        b.doSomething();
    }
}

@Component
public class B {
    private final ServiceA serviceA;

    public B(ServiceA serviceA) {
        this.serviceA = serviceA;
    }

    public void doSomething() {
        // ������ ������ B
    }
}
```

**����������:**
- ����� `B` �������� ����� ��������� `ServiceA`, ��� ������� ����������� � ��������� ���� �����������.

### 4. **������������� ���������� `ApplicationContextAware`**

� ��������� ������� ����� �������� ��� ������� ����� �������� Spring, ��� ����� �������� ��������� ����������� �����������.

**������:**

```java
@Component
public class A {
    private B b;

    @Autowired
    private ApplicationContext context;

    @PostConstruct
    public void init() {
        this.b = context.getBean(B.class);
    }
}

@Component
public class B {
    private final A a;

    public B(A a) {
        this.a = a;
    }
}
```

**����������:**
- `A` �������� ��������� `B` ����� `ApplicationContext`, ������� ����������� ����������� �� ����� �������������.

## ����������

����������� ����������� ����� � Spring ����� ��������� ���������� ���������: ������������� �������� ������������ ����� `@Lazy`, ���������� ����� �������, ������������� � �������������� ����������� ��� �������, � ����� ���������� ����� ����� �������� Spring. ��� ������� �������� ������������ ����������� ���������� ������ � �������� ������ �������������.

# 40. ��� ���������� �� ����������� ����������� �����?

## ��������

����������� ����������� ���������, ����� ��� ��� ����� Spring-���� ������� ���� �� �����, ��� ������� ��������� ���� ������������. ��� �������� � ������� ��� �������� ����� � ������������� ���������. � Spring Framework ������������� ��������� ������� ������� ���� ��������.

## ������� ���������� ����������� �����������

### 1. **������������� ��������� `@Lazy`**

��������� `@Lazy` ��������� ����������� �������� ���� �� ������� ��� ������������ �������������. ��� ����� ������ ��������� ����������� �����������.

**������:**

```java
@Component
public class A {
    private final B b;

    public A(@Lazy B b) {
        this.b = b;
    }
}

@Component
public class B {
    private final A a;

    public B(A a) {
        this.a = a;
    }
}
```

**����������:**
- � ������ `A` ����������� �� `B` ����������� � ���������� `@Lazy`, ��� ��������� Spring �������� �������� `B` �� �������, ����� ��� ������� �����������.

### 2. **��������� ����� �������**

������ ��������� ������������ ����� ����������� ����� ������������ �������, ����� Spring ������� ������ ����, � ����� ��������� �����������.

**������:**

```java
@Component
public class A {
    private B b;

    @Autowired
    public void setB(B b) {
        this.b = b;
    }
}

@Component
public class B {
    private A a;

    @Autowired
    public void setA(A a) {
        this.a = a;
    }
}
```

**����������:**
- Spring ������� ������� ��� ����, � ����� ��������� ����������� ����� �������, �������� ����.

### 3. **������������� ����������� ��� �������**

��� �������������� ����������� ����������� ����� �������� �����������, �������� ������ ����� ���������� ��� �������. ��� ��������� ������� ����������� ����� ������.

**������:**

```java
public interface ServiceA {
    void performAction();
}

@Component
public class A implements ServiceA {
    private final B b;

    public A(B b) {
        this.b = b;
    }

    @Override
    public void performAction() {
        b.doSomething();
    }
}

@Component
public class B {
    private final ServiceA serviceA;

    public B(ServiceA serviceA) {
        this.serviceA = serviceA;
    }

    public void doSomething() {
        // ������ ������ B
    }
}
```

**����������:**
- ����� `B` �������� ����� ��������� `ServiceA`, ��� ������� ����������� � ��������� ���� �����������.

### 4. **������������� ���������� `ApplicationContextAware`**

� ��������� ������� ����� �������� ��� ������� ����� �������� Spring, ��� ����� �������� ��������� ����������� �����������.

**������:**

```java
@Component
public class A {
    private B b;

    @Autowired
    private ApplicationContext context;

    @PostConstruct
    public void init() {
        this.b = context.getBean(B.class);
    }
}

@Component
public class B {
    private final A a;

    public B(A a) {
        this.a = a;
    }
}
```

**����������:**
- `A` �������� ��������� `B` ����� `ApplicationContext`, ������� ����������� ����������� �� ����� �������������.

## ����������

����������� ����������� ����� � Spring ����� ��������� ���������� ���������: ������������� �������� ������������ ����� `@Lazy`, ���������� ����� �������, ������������� � �������������� ����������� ��� �������, � ����� ���������� ����� ����� �������� Spring. ��� ������� �������� ������������ ����������� ���������� ������ � �������� ������ �������������.

# 41. ���������� ��� ������������ Spring 5.

## �������� ������������ Spring 5

### 1. **��������� ����������� ����������������**

����� �� �������� ������������ � Spring 5 �������� ��������� **����������� ����������������**. ������ ����� ���������� ���-��������� ? **Spring WebFlux**, ������� ��������� ������� �����������, ������������� ���������� � ���������� backpressure. ��� ����� �������� ��������� ���������� � �������� **Reactor**, ���������� �� ������������ Reactive Streams.

**�������� ����������� Spring WebFlux:**
- ����������� ������������� �������� ��� ��������� ������������������.
- ��� ����������� �����: ��������� (��� � Spring MVC) � �������������� API.
- ��������� ���������� ����� ������: `Mono` � `Flux`.

**������:**

```java
@RestController
public class ReactiveController {
    
    @GetMapping("/flux")
    public Flux<String> getFlux() {
        return Flux.just("Spring", "5", "Reactor")
                   .delayElements(Duration.ofSeconds(1));
    }
}
```

**����������:**
- `Flux` ������������ ����� ������, ������� ����� ��������� ��������� ��������� ��� ����������� �������.

### 2. **��������� Java 8 � 9**

Spring 5 ��������� ������� �� ������������� Java 8, � ����� ������������ ����� API �� Java 9. ������ �� ���������� ������� ������������ �������������� ����������� Java 8: ������-���������, ������ � `Optional`. ����� Spring 5 ������������� � **Jigsaw-��������**, ��������������� � Java 9.

### 3. **��������� ������������ ����� Kotlin**

Spring 5 ��������� **��������� ����� Kotlin**, ��� ������ ��� ������ ������� ����������� � �������� ���������� ����� �����. Kotlin ��������� ������ ����� ������������� � ���������� ���, ������������ ����� �����������, ��� �������� ��� ������������ ����������������.

**������ �� Kotlin:**

```kotlin
@RestController
class KotlinController {
    
    @GetMapping("/hello")
    fun hello(): Mono<String> {
        return Mono.just("Hello, Spring 5 with Kotlin!")
    }
}
```

### 4. **���������� ���������� � JDK 9+**

Spring 5 �������� ���������� ��� ������ � �������� JDK 9+ (������� **Jigsaw**). ��� ��������� ���������� �� ������ � �������� ������������� ��������� ����������.

### 5. **�������������� ���� (Functional Bean Registration)**

Spring 5 ������������� ����������� �������������� ���� � �������������� ��������������� �������, � �� ����� ��������� ��� XML-������������. ��� �������� ������� � ���������� �����������, ��� ������ �������� �� �������������� ����������������.

**������:**

```java
@Configuration
public class AppConfig {

    @Bean
    public Supplier<MyService> myService() {
        return MyService::new;
    }
}
```

### 6. **�������� ���������� API**

Spring 5 ��������� �� ���� ���������� API, ����� ���:
- ��������� ������ ������ Java (�� 8).
- XML-based `BeanDefinitionReader`.
- ������, ��������� � ����������, Groovy, � ������ ������������ �����������.

### 7. **��������� Java EE 8**

Spring 5 ������������ ������������ Java EE 8, ������� **JPA 2.2**, **JSF 2.3**, **Servlet 4.0** � ������.

### 8. **Spring WebFlux Test**

����� ����������� ����������, Spring 5 ������� ��������� ������������ ���������� ���������� � �������������� ���������� **Spring WebFlux Test**.

**������ �����:**

```java
@WebFluxTest
class ReactiveControllerTest {
    
    @Autowired
    private WebTestClient webTestClient;
    
    @Test
    void testFlux() {
        webTestClient.get().uri("/flux")
                     .exchange()
                     .expectStatus().isOk()
                     .expectBodyList(String.class)
                     .hasSize(3)
                     .contains("Spring", "5", "Reactor");
    }
}
```

### 9. **��������� ������������ ����������������**

Spring 5 �������� ����������� ��������� ��������� ���������� �����������, ������������ `CompletableFuture`, `Mono`, `Flux` � ������ ������������� ���������.

### 10. **���������� ��������� ��������� ���������**

Spring 5 ������� ��������� ���������� � ����������� ���������� ������������, ������ ���:
- **Reactor 3.0**
- **Hibernate 5**
- **Kotlin 1.1+**
- **Spring Boot 2.0**

## ����������

Spring 5 ���� ������������ ��������� � ������� ����������� ����������������, ��������� ����� ������������ Java, ���������� � Kotlin � ���������� ���������������� �� JDK 9+. ��� ������������ ������ ���������� ���������� �� Spring ��� ����� ������ � �����������.
