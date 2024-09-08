# 1. Что такое ORM? Что такое JPA? Что такое Hibernate?

## ORM (Object-Relational Mapping)

**Object-Relational Mapping (ORM)** — это технология программирования, которая позволяет разработчикам работать с данными в реляционных базах данных, используя объектно-ориентированные парадигмы. Суть ORM заключается в автоматическом преобразовании данных между объектами языка программирования (например, Java-классами) и таблицами базы данных. ORM обеспечивает разработку, которая снижает необходимость написания SQL-кода вручную, предоставляя удобный и абстрагированный доступ к данным.

### Основные возможности ORM:
1. **Маппинг объектов на таблицы:** ORM позволяет маппировать объекты классов на строки таблиц в базе данных.
2. **Автоматическая генерация SQL-запросов:** Система автоматически создает SQL-запросы для операций с объектами (вставка, обновление, удаление и выборка данных).
3. **Работа с объектами:** Разработчики работают с данными как с объектами, а не с таблицами или строками SQL, что упрощает код и повышает читаемость.

## JPA (Java Persistence API)

**Java Persistence API (JPA)** — это спецификация, определяющая стандарт для управления сохранением объектов в Java-приложениях. JPA предоставляет набор аннотаций и API для маппинга объектов Java на реляционные базы данных, но сама по себе не является реализацией. JPA действует как интерфейс между Java-кодом и инструментами ORM, такими как Hibernate, EclipseLink, и OpenJPA.

### Основные возможности JPA:
1. **Управление жизненным циклом объектов:** JPA предоставляет API для создания, чтения, обновления и удаления (CRUD) объектов.
2. **Маппинг объектов:** JPA использует аннотации для маппинга полей классов на столбцы таблиц базы данных.
3. **Кэширование и управление транзакциями:** JPA поддерживает уровни кэширования, управление транзакциями и стратегии блокировок.

## Hibernate

**Hibernate** — это популярная реализация JPA и одна из самых известных ORM-библиотек в Java. Hibernate предоставляет все возможности ORM и JPA, а также расширяет их дополнительными функциями, такими как кэширование, управление соединениями с базой данных и работа с базами, не поддерживающими SQL.

### Основные возможности Hibernate:
1. **Полная поддержка JPA:** Hibernate полностью реализует спецификацию JPA, что делает его совместимым со стандартом.
2. **Дополнительные функции:** Hibernate предлагает поддержку кэширования второго уровня, специфичные методы запросов (HQL, Criteria API), а также поддержку «ленивой» инициализации данных.
3. **Интеграция с различными СУБД:** Поддержка различных баз данных через стандартные и кастомные диалекты SQL.

### Пример использования JPA и Hibernate

Пример создания сущности `Employee` с использованием JPA-аннотаций, которая будет маппироваться на таблицу базы данных:

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;

@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String position;

    // Геттеры и сеттеры

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPosition() {
        return position;
    }

    public void setPosition(String position) {
        this.position = position;
    }
}
```

### Объяснение примера:

1. **Аннотация `@Entity`:** Определяет, что класс `Employee` является сущностью, и должен быть связан с таблицей в базе данных.
2. **Аннотация `@Id`:** Помечает поле `id` как первичный ключ.
3. **Аннотация `@GeneratedValue`:** Указывает, что значение первичного ключа будет генерироваться автоматически.

## Заключение

ORM упрощает работу с базами данных за счет автоматизации маппинга данных между объектами и таблицами. JPA — это спецификация, которая задает стандарт для этой автоматизации в Java, а Hibernate — одна из наиболее популярных реализаций JPA, расширяющая его возможности и предоставляющая дополнительные функции для работы с базами данных.

# 2. Что такое EntityManager?

**EntityManager** — это основной интерфейс для взаимодействия с контекстом постоянства (persistence context) в JPA (Java Persistence API). Он управляет жизненным циклом объектов-сущностей, выполняет CRUD-операции и управляет транзакциями с базой данных. EntityManager обеспечивает маппинг объектов Java на реляционные базы данных и обратно.

## Основные задачи и функции EntityManager

### 1. Управление жизненным циклом сущностей
EntityManager управляет состояниями сущностей, такими как *новая (transient)*, *управляемая (managed)*, *отсоединенная (detached)* и *удаленная (removed)*. Он отвечает за приведение объектов в соответствующее состояние в зависимости от операций, выполняемых с ними.

### 2. CRUD-операции
EntityManager предоставляет методы для создания, чтения, обновления и удаления сущностей:

- **`persist()`** — добавляет новую сущность в контекст постоянства. Вставка в базу данных произойдет при выполнении транзакции.
- **`merge()`** — синхронизирует состояние отсоединенной сущности с базой данных.
- **`remove()`** — удаляет сущность из базы данных.
- **`find()`** — ищет сущность по ее идентификатору (первичному ключу).
- **`getReference()`** — возвращает ссылку на сущность, но без выполнения полного запроса, используется для ленивой загрузки.

### 3. Управление транзакциями
EntityManager работает с транзакциями, предоставляя методы для начала, завершения и отката транзакций:

- **`begin()`** — начало транзакции.
- **`commit()`** — завершение транзакции, при котором все изменения сохраняются в базе данных.
- **`rollback()`** — откат транзакции, отменяющий все изменения.

### 4. Выполнение запросов
EntityManager позволяет выполнять JPQL (Java Persistence Query Language) и Native SQL запросы для извлечения данных из базы:

- **JPQL-запросы:** Абстрагированные запросы, использующие имена классов и полей вместо имен таблиц и колонок.
- **Native SQL:** Прямые запросы на SQL, специфичные для базы данных.

### Пример использования EntityManager

Пример демонстрирует использование EntityManager для добавления новой сущности и ее обновления:

```java
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;

public class EmployeeService {

    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("example-unit");
        EntityManager em = emf.createEntityManager();

        // Начало транзакции
        em.getTransaction().begin();

        // Создание новой сущности Employee
        Employee employee = new Employee();
        employee.setName("John Doe");
        employee.setPosition("Developer");

        // Сохранение сущности в базу данных
        em.persist(employee);

        // Коммит транзакции
        em.getTransaction().commit();

        // Начало новой транзакции для обновления данных
        em.getTransaction().begin();

        // Обновление сущности
        employee.setPosition("Senior Developer");
        em.merge(employee);

        // Коммит транзакции
        em.getTransaction().commit();

        // Закрытие EntityManager и фабрики
        em.close();
        emf.close();
    }
}
```

### Объяснение работы:
1. **Создание EntityManager:** Создается фабрика `EntityManagerFactory`, которая используется для создания `EntityManager`.
2. **Работа с транзакцией:** Начинается транзакция, в которой создается новый объект `Employee` и сохраняется в базу данных с помощью метода `persist()`.
3. **Обновление сущности:** В новой транзакции изменяется поле сущности, и она обновляется методом `merge()`.
4. **Закрытие EntityManager:** Завершаются все открытые ресурсы.

## Заключение

EntityManager является центральным компонентом в JPA, предоставляющим API для работы с сущностями, транзакциями и базой данных. Он абстрагирует взаимодействие с реляционной базой данных, позволяя работать с объектами Java и обеспечивая удобный способ управления их состоянием и жизненным циклом.

# 3. Каким условиям должен удовлетворять класс, чтобы являться Entity?

Класс считается **Entity** (сущностью) в JPA, если он представляет собой объект, который маппируется на строку в таблице базы данных. Сущности используются для хранения данных в базах, их изменения и извлечения. Чтобы класс мог быть признан сущностью, он должен соответствовать ряду условий и правил.

## Основные условия, которым должен удовлетворять класс-сущность:

### 1. Аннотация `@Entity`
Класс должен быть помечен аннотацией `@Entity`. Это основной признак, по которому JPA распознает класс как сущность, подлежащую маппингу на таблицу в базе данных.

```java
import javax.persistence.Entity;

@Entity
public class Employee {
    // поля и методы
}
```

### 2. Наличие конструктора без параметров
Класс-сущность должен иметь **публичный или защищенный конструктор без параметров**. Это необходимо для того, чтобы JPA могла создавать экземпляры сущности рефлексивно во время выполнения.

```java
public Employee() {
    // Конструктор без параметров
}
```

### 3. Наличие уникального идентификатора (`@Id`)
Каждая сущность должна иметь поле, помеченное аннотацией `@Id`, которое будет использоваться как первичный ключ. Это поле должно быть уникальным и идентифицировать каждую запись в таблице.

```java
import javax.persistence.Id;

@Entity
public class Employee {

    @Id
    private Long id;

    // геттеры и сеттеры
}
```

### 4. Поля должны быть маппируемыми
Поля класса должны быть маппируемыми типами, такими как примитивы, строки, объекты-обертки, или другими сущностями. Поля не должны быть объявлены как `transient` или `static`, иначе они не будут маппироваться на базу данных.

```java
private String name;
private String position;
```

### 5. Обязательные аннотации маппинга (при необходимости)
Для корректного маппинга сущности к таблице или столбцам базы данных могут потребоваться дополнительные аннотации, такие как `@Table`, `@Column`, `@GeneratedValue`, `@OneToMany`, `@ManyToOne` и другие. Хотя они не обязательны для базового определения сущности, их использование помогает настроить поведение маппинга более точно.

```java
import javax.persistence.Column;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;

@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "employee_name", nullable = false)
    private String name;
}
```

### 6. Реализация сериализуемости (рекомендуется)
Рекомендуется, чтобы сущности реализовывали интерфейс `Serializable`, чтобы их можно было легко передавать по сети или сохранять на диск. Хотя это не является строгим требованием, это часто применяется в практике разработки.

```java
import java.io.Serializable;

@Entity
public class Employee implements Serializable {
    // поля и методы
}
```

### 7. Неиспользование финальных классов или методов
Сущности не должны быть `final`, и их методы не должны быть `final`, `static` или `transient`, так как это препятствует правильному функционированию ORM. JPA использует прокси-объекты и ленивую загрузку, которые не могут работать с финальными методами и классами.

### 8. Определение равенства и хеш-кода (`equals()` и `hashCode()`)
Хотя это не является жестким требованием, рекомендуется переопределить методы `equals()` и `hashCode()`, чтобы они основывались на первичных ключах (`@Id`). Это обеспечивает корректное поведение сущностей при использовании их в коллекциях или сравнениях.

### Полный пример класса-сущности

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Column;
import java.io.Serializable;

@Entity
public class Employee implements Serializable {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "employee_name", nullable = false)
    private String name;

    private String position;

    // Конструктор без параметров
    public Employee() {
    }

    // Геттеры и сеттеры
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPosition() {
        return position;
    }

    public void setPosition(String position) {
        this.position = position;
    }

    // Переопределение equals() и hashCode() на основе id
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Employee employee = (Employee) o;

        return id != null ? id.equals(employee.id) : employee.id == null;
    }

    @Override
    public int hashCode() {
        return id != null ? id.hashCode() : 0;
    }
}
```

## Заключение

Для того чтобы класс мог являться сущностью в JPA, он должен быть аннотирован `@Entity`, иметь конструктор без параметров, поле с аннотацией `@Id`, не должен быть `final`, и его поля не должны быть `static` или `transient`. Эти условия позволяют JPA корректно управлять объектами и взаимодействовать с базой данных, обеспечивая согласованное и предсказуемое поведение.

# 4. Может ли абстрактный класс быть Entity?

Да, **абстрактный класс** может быть использован как сущность (Entity) в JPA, но с определенными особенностями и ограничениями. Абстрактный класс сам по себе не будет маппироваться напрямую на таблицу в базе данных, но он может быть использован в иерархии наследования сущностей для обеспечения общей функциональности.

## Условия использования абстрактного класса как Entity

1. **Аннотация `@MappedSuperclass`:** Абстрактный класс должен быть помечен аннотацией `@MappedSuperclass`, чтобы указать, что его поля и методы должны быть унаследованы сущностями-наследниками. Этот подход позволяет включать общие поля и бизнес-логику в несколько сущностей.

    ```java
    import javax.persistence.MappedSuperclass;

    @MappedSuperclass
    public abstract class BaseEntity {
        private Long id;

        // Геттеры, сеттеры и другие общие методы
    }
    ```

2. **Абстрактные методы и общая функциональность:** Абстрактный класс может содержать как реализованные, так и абстрактные методы, предоставляя общий интерфейс или поведение, которое будет использоваться всеми наследующими его сущностями.

3. **Запрещено аннотировать абстрактный класс `@Entity`:** Абстрактный класс не может быть напрямую аннотирован `@Entity`, так как JPA не создаст для него таблицу. Он лишь предоставляет общую функциональность и структуру для дочерних классов.

## Пример использования абстрактного класса как базы для сущностей

### Абстрактный класс

```java
import javax.persistence.MappedSuperclass;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@MappedSuperclass
public abstract class BaseEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String createdBy;

    private String updatedBy;

    // Геттеры и сеттеры для общих полей

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getCreatedBy() {
        return createdBy;
    }

    public void setCreatedBy(String createdBy) {
        this.createdBy = createdBy;
    }

    public String getUpdatedBy() {
        return updatedBy;
    }

    public void setUpdatedBy(String updatedBy) {
        this.updatedBy = updatedBy;
    }
}
```

### Класс-наследник, который является сущностью

```java
import javax.persistence.Entity;
import javax.persistence.Table;

@Entity
@Table(name = "employees")
public class Employee extends BaseEntity {

    private String name;
    private String position;

    // Геттеры и сеттеры для полей Employee

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPosition() {
        return position;
    }

    public void setPosition(String position) {
        this.position = position;
    }
}
```

### Объяснение работы:

- **Абстрактный класс `BaseEntity`**: определяет общие поля и методы, которые будут унаследованы всеми дочерними сущностями.
- **Конкретная сущность `Employee`**: наследует все поля и методы от `BaseEntity`, а также добавляет свои уникальные свойства, такие как `name` и `position`. Эта сущность будет маппироваться на таблицу `employees` в базе данных.

## Заключение

Абстрактный класс может быть частью иерархии сущностей, если он помечен аннотацией `@MappedSuperclass`. Это позволяет реализовывать повторно используемые свойства и методы в нескольких сущностях, обеспечивая удобную иерархию и сокращая дублирование кода. Однако такой класс не будет сам по себе сущностью и не будет маппироваться на таблицу в базе данных.

# 5. Может ли Entity класс наследоваться от не Entity классов (non-entity classes)?

Да, Entity класс в JPA (Java Persistence API) может наследоваться от не Entity классов (non-entity classes). Это распространенный подход для улучшения структуры и повторного использования кода в приложении.

## Основные условия наследования от non-entity классов

1. **Класс-родитель не должен быть аннотирован `@Entity`:** Родительский класс не должен быть помечен аннотацией `@Entity`, так как он сам по себе не является сущностью и не маппируется на таблицу в базе данных. Он может предоставлять поля, методы и логику, которые будут унаследованы сущностями.

2. **Использование `@MappedSuperclass`:** Для класса-родителя можно использовать аннотацию `@MappedSuperclass`, если нужно, чтобы его поля и методы стали частью сущностей-наследников. Если `@MappedSuperclass` не используется, JPA просто игнорирует поля родительского класса при маппинге.

3. **Нет прямого маппинга:** Поля и методы, определенные в родительском классе без `@MappedSuperclass`, не будут напрямую маппироваться в базу данных. Однако они остаются частью логики сущности и могут использоваться в бизнес-логике.

## Пример использования не Entity классов в иерархии сущностей

### Класс-родитель (не сущность)

```java
public class AuditInfo {
    private String createdBy;
    private String updatedBy;

    // Геттеры и сеттеры
    public String getCreatedBy() {
        return createdBy;
    }

    public void setCreatedBy(String createdBy) {
        this.createdBy = createdBy;
    }

    public String getUpdatedBy() {
        return updatedBy;
    }

    public void setUpdatedBy(String updatedBy) {
        this.updatedBy = updatedBy;
    }
}
```

### Сущность, наследующая от класса `AuditInfo`

```java
import javax.persistence.Entity;
import javax.persistence.Table;
import javax.persistence.Id;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;

@Entity
@Table(name = "orders")
public class Order extends AuditInfo {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String orderNumber;

    // Геттеры и сеттеры
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getOrderNumber() {
        return orderNumber;
    }

    public void setOrderNumber(String orderNumber) {
        this.orderNumber = orderNumber;
    }
}
```

### Объяснение работы

1. **Класс `AuditInfo`:** Это обычный класс, не аннотированный `@Entity`, который содержит поля и методы для аудита (например, кто создал и обновил запись). Он предоставляет общую функциональность для сущностей, но не маппируется на таблицу.
   
2. **Сущность `Order`:** Наследует `AuditInfo`, и поэтому все поля и методы родительского класса доступны в этой сущности. Однако маппингу подлежат только те поля, которые определены в классе `Order` или отмечены в `@MappedSuperclass` в родительском классе.

## Заключение

Сущности в JPA могут наследовать от не Entity классов, что помогает лучше структурировать код и повторно использовать общие части, такие как бизнес-логика или вспомогательные методы. Основное ограничение — такие классы не маппируются на таблицы в базе данных, если они не аннотированы как `@MappedSuperclass`.

# 6. Может ли Entity класс наследоваться от других Entity классов?

Да, Entity класс может наследоваться от других Entity классов в JPA. Это называется **наследование сущностей** и является мощным механизмом для моделирования объектов, когда один класс может расширять другой, унаследовав его поля и методы. JPA предоставляет несколько стратегий для маппинга иерархий классов на таблицы в базе данных.

## Основные стратегии наследования Entity классов

1. **Single Table (наследование с одной таблицей):** Все сущности иерархии хранятся в одной таблице, с дополнительным столбцом, идентифицирующим тип сущности. Это простая стратегия с высокой производительностью, но может привести к большому количеству `NULL` значений.

   - Аннотация: `@Inheritance(strategy = InheritanceType.SINGLE_TABLE)`
   - Дополнительная аннотация для идентификации типа: `@DiscriminatorColumn`

2. **Joined Table (наследование с объединением таблиц):** Каждая сущность маппируется на свою таблицу, а таблицы связаны через внешние ключи. Это более гибкий способ, который сохраняет нормализованную структуру данных.

   - Аннотация: `@Inheritance(strategy = InheritanceType.JOINED)`

3. **Table Per Class (таблица на каждый класс):** Каждая сущность маппируется на свою таблицу, содержащую все поля, включая унаследованные. Это приводит к дублированию данных, но позволяет избежать `NULL` значений.

   - Аннотация: `@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)`

## Пример наследования с использованием стратегии Single Table

### Базовый класс-сущность

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Inheritance;
import javax.persistence.InheritanceType;
import javax.persistence.DiscriminatorColumn;

@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "vehicle_type")
public class Vehicle {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String manufacturer;

    // Геттеры и сеттеры
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getManufacturer() {
        return manufacturer;
    }

    public void setManufacturer(String manufacturer) {
        this.manufacturer = manufacturer;
    }
}
```

### Подкласс-сущность Car

```java
import javax.persistence.Entity;
import javax.persistence.DiscriminatorValue;

@Entity
@DiscriminatorValue("Car")
public class Car extends Vehicle {
    
    private int numberOfDoors;

    // Геттеры и сеттеры
    public int getNumberOfDoors() {
        return numberOfDoors;
    }

    public void setNumberOfDoors(int numberOfDoors) {
        this.numberOfDoors = numberOfDoors;
    }
}
```

### Подкласс-сущность Bike

```java
import javax.persistence.Entity;
import javax.persistence.DiscriminatorValue;

@Entity
@DiscriminatorValue("Bike")
public class Bike extends Vehicle {
    
    private boolean hasPedals;

    // Геттеры и сеттеры
    public boolean isHasPedals() {
        return hasPedals;
    }

    public void setHasPedals(boolean hasPedals) {
        this.hasPedals = hasPedals;
    }
}
```

### Объяснение работы

1. **Базовый класс `Vehicle`:** Аннотирован как сущность с `@Inheritance(strategy = InheritanceType.SINGLE_TABLE)`. Поля этой сущности будут общими для всех дочерних сущностей.
   
2. **Дочерние классы `Car` и `Bike`:** Являются сущностями и наследуют поля от `Vehicle`. Они также добавляют свои уникальные поля.

3. **Маппинг в одну таблицу:** В базе данных будет создана одна таблица `Vehicle`, содержащая все поля `Vehicle`, `Car` и `Bike`, а столбец `vehicle_type` указывает тип сущности.

## Заключение

Наследование Entity классов в JPA позволяет гибко моделировать иерархии объектов и контролировать, как данные сохраняются в базе. Выбор подходящей стратегии маппинга зависит от требований к производительности и структуры данных.

# 7. Может ли не Entity класс наследоваться от Entity класса?

Нет, не Entity класс не должен наследоваться от Entity класса. В JPA это запрещено, поскольку такие классы не будут корректно обрабатываться механизмами ORM. Если класс не помечен аннотацией `@Entity`, он не будет считаться частью иерархии сущностей, и его наследование от Entity класса может привести к непредсказуемому поведению и ошибкам.

## Причины, почему не Entity класс не должен наследоваться от Entity класса

1. **Некорректное управление жизненным циклом:** Классы, которые не являются сущностями, не управляются EntityManager, поэтому они не могут быть правильно сохранены, обновлены или удалены через JPA.

2. **Проблемы с маппингом и доступом к данным:** Если класс не аннотирован как `@Entity`, JPA не будет маппировать его на таблицу в базе данных. Поля, унаследованные от Entity класса, могут не сохраняться или не загружаться корректно.

3. **Отсутствие поддержки операций JPA:** Такие классы не смогут использовать функциональность, предоставляемую EntityManager, например, для выполнения запросов, транзакций и других операций.

4. **Проблемы с наследованием стратегий:** JPA наследует стратегии маппинга от базового Entity класса. Если дочерний класс не является сущностью, это наследование не будет поддерживаться, что нарушает логику маппинга.

## Пример неверного использования

### Неверное наследование

```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class BaseEntity {
    @Id
    private Long id;
    private String commonField;

    // Геттеры и сеттеры
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getCommonField() {
        return commonField;
    }

    public void setCommonField(String commonField) {
        this.commonField = commonField;
    }
}

// Неверный дочерний класс
public class NonEntitySubclass extends BaseEntity {
    private String specificField;

    // Геттеры и сеттеры
    public String getSpecificField() {
        return specificField;
    }

    public void setSpecificField(String specificField) {
        this.specificField = specificField;
    }
}
```

### Проблемы с данным подходом

- **Не будет маппинга:** JPA игнорирует `NonEntitySubclass`, и поля `specificField` не будут сохраняться в базу данных.
- **Ошибка при использовании JPA:** Попытка сохранить объект `NonEntitySubclass` с использованием `EntityManager` приведет к исключению или некорректному поведению.

## Заключение

В JPA класс, который наследуется от сущности, должен сам быть сущностью, чтобы корректно управляться EntityManager. Если требуется использовать общую функциональность, лучше выделить её в `@MappedSuperclass` или использовать абстрактные классы с общей логикой, но избегать наследования от сущностей для классов, которые не должны маппироваться на таблицы.

# 8. Что такое встраиваемый (Embeddable) класс? Какие требования JPA устанавливает к встраиваемым (Embeddable) классам?

**Встраиваемый класс (Embeddable)** — это специальный тип класса в JPA, который не является самостоятельной сущностью, а используется для группировки нескольких полей в единую логическую структуру, которая может быть включена в другие сущности. Встраиваемые классы позволяют повторно использовать код, избегая дублирования полей в различных сущностях.

## Основные особенности Embeddable классов

1. **Не являются сущностями:** Встраиваемые классы не управляются напрямую EntityManager и не имеют собственного идентификатора (`@Id`). Вместо этого они используются как компоненты других сущностей.
  
2. **Включение в другие сущности:** Поля встраиваемого класса становятся частью сущности, которая его использует. Это упрощает дизайн объектов, позволяя логически группировать связанные данные.

3. **Аннотация `@Embeddable`:** Для обозначения класса как встраиваемого используется аннотация `@Embeddable`.

4. **Использование аннотации `@Embedded`:** Встраиваемый класс используется внутри сущности при помощи аннотации `@Embedded`.

## Требования к встраиваемым классам в JPA

1. **Аннотация `@Embeddable`:** Класс должен быть помечен аннотацией `@Embeddable` для того, чтобы JPA распознавала его как встраиваемый.

2. **Конструктор по умолчанию:** Как и другие классы JPA, встраиваемые классы должны иметь конструктор по умолчанию (без аргументов), который может быть как публичным, так и с модификатором доступа `protected`.

3. **Сериализация (желательно):** Хотя это не является строгим требованием, рекомендуется, чтобы встраиваемый класс реализовывал интерфейс `Serializable`, особенно если данные будут кэшироваться.

4. **Поля или свойства:** Встраиваемые классы могут использовать поля или свойства для доступа к данным, и JPA поддерживает аннотации над этими полями или геттерами/сеттерами.

## Пример использования встраиваемого класса

### Встраиваемый класс Address

```java
import javax.persistence.Embeddable;
import java.io.Serializable;

@Embeddable
public class Address implements Serializable {
    private String street;
    private String city;
    private String zipCode;

    // Конструктор по умолчанию
    public Address() {
    }

    // Геттеры и сеттеры
    public String getStreet() {
        return street;
    }

    public void setStreet(String street) {
        this.street = street;
    }

    public String getCity() {
        return city;
    }

    public void setCity(String city) {
        this.city = city;
    }

    public String getZipCode() {
        return zipCode;
    }

    public void setZipCode(String zipCode) {
        this.zipCode = zipCode;
    }
}
```

### Сущность с использованием встраиваемого класса

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Embedded;

@Entity
public class Person {
    @Id
    private Long id;
    private String name;

    @Embedded
    private Address address;

    // Геттеры и сеттеры
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }
}
```

### Объяснение работы

1. **Класс `Address`:** Помечен аннотацией `@Embeddable` и используется для хранения адресных данных. Он не является самостоятельной сущностью и не имеет собственного идентификатора.
  
2. **Класс `Person`:** Сущность, содержащая поля `id`, `name` и встраиваемое поле `address`, аннотированное `@Embedded`. Поля класса `Address` станут частью таблицы `Person`.

3. **Преимущества:** Повторное использование и группировка связанных данных без создания отдельных таблиц и идентификаторов.

## Заключение

Встраиваемые классы в JPA позволяют структурировать и повторно использовать данные, обеспечивая гибкость и упрощение моделей объектов. Использование таких классов упрощает управление связанными данными, делая код более читаемым и поддерживаемым.

# 9. Что такое Mapped Superclass?

**Mapped Superclass** — это специальный тип класса в JPA, который используется как базовый класс для других сущностей, но сам по себе не является сущностью и не маппируется на таблицу в базе данных. Классы, помеченные аннотацией `@MappedSuperclass`, предоставляют общие свойства и поведение для своих дочерних сущностей, но не могут быть напрямую управляемы EntityManager.

## Основные особенности Mapped Superclass

1. **Не является самостоятельной сущностью:** Класс с аннотацией `@MappedSuperclass` не имеет собственного идентификатора и не маппируется на отдельную таблицу.
   
2. **Поля и методы наследуются дочерними сущностями:** Поля, аннотированные в Mapped Superclass, будут включены в дочерние классы, которые являются сущностями, и будут маппироваться на их таблицы.

3. **Общие свойства и методы:** Используется для определения общих полей (например, `id`, `createdDate`, `updatedDate`) и методов (например, `getId()`, `setId()`), которые могут использоваться в нескольких сущностях.

4. **Нет связи с EntityManager:** Mapped Superclass не управляется напрямую EntityManager и не может участвовать в запросах JPA.

## Требования к Mapped Superclass

1. **Аннотация `@MappedSuperclass`:** Класс должен быть помечен аннотацией `@MappedSuperclass`.

2. **Конструктор по умолчанию:** Класс должен иметь конструктор по умолчанию.

3. **Отсутствие аннотации `@Entity`:** Класс не должен быть аннотирован как `@Entity`, так как это противоречит его назначению.

## Пример использования Mapped Superclass

### Определение Mapped Superclass

```java
import javax.persistence.MappedSuperclass;
import javax.persistence.Id;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import java.time.LocalDateTime;

@MappedSuperclass
public abstract class BaseEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private LocalDateTime createdDate;
    private LocalDateTime updatedDate;

    // Геттеры и сеттеры
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public LocalDateTime getCreatedDate() {
        return createdDate;
    }

    public void setCreatedDate(LocalDateTime createdDate) {
        this.createdDate = createdDate;
    }

    public LocalDateTime getUpdatedDate() {
        return updatedDate;
    }

    public void setUpdatedDate(LocalDateTime updatedDate) {
        this.updatedDate = updatedDate;
    }
}
```

### Дочерние сущности, наследующие Mapped Superclass

```java
import javax.persistence.Entity;

@Entity
public class User extends BaseEntity {
    private String username;
    private String email;

    // Геттеры и сеттеры
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}

@Entity
public class Product extends BaseEntity {
    private String name;
    private Double price;

    // Геттеры и сеттеры
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Double getPrice() {
        return price;
    }

    public void setPrice(Double price) {
        this.price = price;
    }
}
```

### Объяснение работы

1. **Класс `BaseEntity`:** Определяет общие поля `id`, `createdDate`, и `updatedDate`, которые часто используются в других сущностях.
   
2. **Классы `User` и `Product`:** Эти классы наследуют от `BaseEntity`, но при этом маппируются на собственные таблицы в базе данных. Поля из `BaseEntity` также будут включены в эти таблицы.

3. **Упрощение кода:** Использование Mapped Superclass позволяет избежать дублирования кода и поддерживать общие свойства в одном месте.

## Заключение

Mapped Superclass используется для определения общих полей и поведения, которые могут быть унаследованы дочерними сущностями. Это позволяет организовать код более структурированно и избежать дублирования, обеспечивая централизованное управление общими аспектами моделей данных.

# 10. Какие три типа стратегий наследования мапинга (Inheritance Mapping Strategies) описаны в JPA?

В JPA существуют три основных стратегии маппинга наследования, которые определяют, как классы с наследованием маппируются на таблицы в базе данных. Эти стратегии позволяют управлять тем, как данные из иерархий классов будут храниться и извлекаться из базы данных.

## 1. Стратегия `SINGLE_TABLE`

**Описание:** В этой стратегии все сущности из иерархии наследования хранятся в одной таблице. Для различия между типами сущностей в таблице используется специальный столбец, который указывает на тип конкретного объекта.

**Преимущества:**
- Простота схемы базы данных, так как все данные хранятся в одной таблице.
- Меньше затрат на выполнение SQL-запросов, так как не требуется выполнять объединения таблиц.

**Недостатки:**
- Таблица может содержать много полей, которые применимы только к некоторым из сущностей.
- Может быть сложным управлять производительностью и масштабируемостью для больших иерархий.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.Inheritance;
import javax.persistence.InheritanceType;
import javax.persistence.DiscriminatorColumn;
import javax.persistence.DiscriminatorValue;

@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "TYPE")
public abstract class Animal {
    private Long id;
    private String name;

    // Геттеры и сеттеры
}

@Entity
@DiscriminatorValue("DOG")
public class Dog extends Animal {
    private String breed;

    // Геттеры и сеттеры
}

@Entity
@DiscriminatorValue("CAT")
public class Cat extends Animal {
    private String color;

    // Геттеры и сеттеры
}
```

**Таблица в базе данных:**

| ID | NAME | BREED | COLOR | TYPE |
|----|------|-------|-------|------|
| 1  | Rex  | Beagle| NULL  | DOG  |
| 2  | Whiskers | NULL  | Black | CAT  |

## 2. Стратегия `TABLE_PER_CLASS`

**Описание:** В этой стратегии каждая сущность из иерархии наследования маппируется на отдельную таблицу. Каждая таблица содержит все столбцы, необходимые для хранения данных этой сущности.

**Преимущества:**
- Чистота и независимость таблиц, каждая таблица содержит только поля, относящиеся к соответствующей сущности.
- Легкость управления данными и расширяемостью.

**Недостатки:**
- Может потребоваться выполнение объединений таблиц для выполнения запросов, что может влиять на производительность.
- Увеличение количества таблиц в базе данных.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.Inheritance;
import javax.persistence.InheritanceType;

@Entity
@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)
public abstract class Animal {
    private Long id;
    private String name;

    // Геттеры и сеттеры
}

@Entity
public class Dog extends Animal {
    private String breed;

    // Геттеры и сеттеры
}

@Entity
public class Cat extends Animal {
    private String color;

    // Геттеры и сеттеры
}
```

**Таблицы в базе данных:**

- Таблица `Animal` (или может отсутствовать, если используется только в качестве абстрактного класса):
  | ID | NAME |
  |----|------|

- Таблица `Dog`:
  | ID | NAME | BREED |
  |----|------|-------|

- Таблица `Cat`:
  | ID | NAME | COLOR |
  |----|------|-------|

## 3. Стратегия `JOINED`

**Описание:** В этой стратегии каждая сущность из иерархии наследования маппируется на отдельную таблицу, но при этом в таблице базового класса содержатся общие поля, и таблицы наследников содержат только поля, уникальные для этих сущностей. Связь между таблицами реализуется с помощью объединений по идентификатору.

**Преимущества:**
- Нормализация данных, так как общие поля хранятся в одной таблице.
- Легкость в управлении данными для сложных иерархий.

**Недостатки:**
- Необходимость выполнения объединений таблиц при выполнении запросов, что может повлиять на производительность.
- Сложность запросов и управления базой данных.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.Inheritance;
import javax.persistence.InheritanceType;
import javax.persistence.PrimaryKeyJoinColumn;

@Entity
@Inheritance(strategy = InheritanceType.JOINED)
public abstract class Animal {
    private Long id;
    private String name;

    // Геттеры и сеттеры
}

@Entity
@PrimaryKeyJoinColumn(name = "ID")
public class Dog extends Animal {
    private String breed;

    // Геттеры и сеттеры
}

@Entity
@PrimaryKeyJoinColumn(name = "ID")
public class Cat extends Animal {
    private String color;

    // Геттеры и сеттеры
}
```

**Таблицы в базе данных:**

- Таблица `Animal`:
  | ID | NAME |
  |----|------|

- Таблица `Dog`:
  | ID | BREED |
  |----|-------|

- Таблица `Cat`:
  | ID | COLOR |
  |----|-------|

## Заключение

Выбор стратегии наследования зависит от требований к проекту, таких как необходимость производительности, нормализации данных и удобства управления. Каждая стратегия имеет свои преимущества и недостатки, и правильный выбор зависит от конкретных условий и требований приложения.

# 11. Как мапятся Enum'ы?

В JPA `Enum`-типы могут быть маппированы на базу данных с использованием аннотации `@Enumerated`. Эта аннотация позволяет задать способ хранения значений перечислений в базе данных. Существует два основных способа маппинга `Enum`:

## 1. Маппинг по порядковому номеру (`@Enumerated(EnumType.ORDINAL)`)

**Описание:** Значения `Enum` сохраняются в базе данных как порядковые номера, соответствующие их позициям в перечислении (начиная с 0). Например, первый элемент перечисления будет сохранен как 0, второй как 1 и так далее.

**Преимущества:**
- Меньший объем занимаемого места в базе данных, так как используется числовое представление.

**Недостатки:**
- Если порядок значений в перечислении изменится, это может привести к некорректным данным в базе данных и проблемам совместимости.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.EnumType;
import javax.persistence.Enumerated;
import javax.persistence.Id;

public enum Status {
    ACTIVE,
    INACTIVE,
    SUSPENDED
}

@Entity
public class User {
    @Id
    private Long id;
    
    @Enumerated(EnumType.ORDINAL)
    private Status status;

    // Геттеры и сеттеры
}
```

**Таблица в базе данных:**

| ID | STATUS |
|----|--------|
| 1  | 0      |
| 2  | 1      |
| 3  | 2      |

## 2. Маппинг по имени (`@Enumerated(EnumType.STRING)`)

**Описание:** Значения `Enum` сохраняются в базе данных как строки, представляющие имена элементов перечисления. Например, значение `Status.ACTIVE` будет сохранено как `"ACTIVE"`.

**Преимущества:**
- Более читаемое и понятное представление данных в базе данных.
- Безопасность от изменений порядка значений в перечислении.

**Недостатки:**
- Занимает больше места в базе данных, так как используется строковое представление.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.EnumType;
import javax.persistence.Enumerated;
import javax.persistence.Id;

public enum Status {
    ACTIVE,
    INACTIVE,
    SUSPENDED
}

@Entity
public class User {
    @Id
    private Long id;
    
    @Enumerated(EnumType.STRING)
    private Status status;

    // Геттеры и сеттеры
}
```

**Таблица в базе данных:**

| ID | STATUS    |
|----|-----------|
| 1  | ACTIVE    |
| 2  | INACTIVE  |
| 3  | SUSPENDED |

## Заключение

Выбор способа маппинга `Enum` зависит от требований к базе данных и приложения. Использование `EnumType.STRING` делает данные более читаемыми и устойчивыми к изменениям порядка значений, в то время как `EnumType.ORDINAL` может быть предпочтительным для оптимизации использования памяти.

# 12. Как мапятся даты (до Java 8 и после)?

В JPA маппинг дат и времени изменился с приходом Java 8, когда были введены новые типы данных для работы с датами и временем. До Java 8 использовались старые классы из пакета `java.util` и `java.sql`, тогда как начиная с Java 8 появились новые классы в пакете `java.time`.

## До Java 8

До Java 8 в JPA для маппинга дат и времени использовались следующие классы:

1. **`java.util.Date`**
   - Маппится на тип данных `DATE`, `TIME` или `TIMESTAMP` в базе данных, в зависимости от того, какие значения требуется хранить.
   
   **Пример:**
   ```java
   import javax.persistence.Entity;
   import javax.persistence.Id;
   import java.util.Date;

   @Entity
   public class Event {
       @Id
       private Long id;
       private Date eventDate;

       // Геттеры и сеттеры
   }
   ```
   **Маппинг:**
   - `java.util.Date` для хранения даты и времени в формате `TIMESTAMP`.

2. **`java.sql.Date`**
   - Используется для хранения только даты (без времени). Маппится на тип данных `DATE` в базе данных.
   
   **Пример:**
   ```java
   import javax.persistence.Entity;
   import javax.persistence.Id;
   import java.sql.Date;

   @Entity
   public class Event {
       @Id
       private Long id;
       private Date eventDate;

       // Геттеры и сеттеры
   }
   ```
   **Маппинг:**
   - `java.sql.Date` для хранения только даты в формате `DATE`.

3. **`java.sql.Timestamp`**
   - Используется для хранения даты и времени. Маппится на тип данных `TIMESTAMP` в базе данных.
   
   **Пример:**
   ```java
   import javax.persistence.Entity;
   import javax.persistence.Id;
   import java.sql.Timestamp;

   @Entity
   public class Event {
       @Id
       private Long id;
       private Timestamp eventTimestamp;

       // Геттеры и сеттеры
   }
   ```
   **Маппинг:**
   - `java.sql.Timestamp` для хранения даты и времени в формате `TIMESTAMP`.

## После Java 8

С Java 8 и введением нового API для работы с датами и временем, JPA поддерживает следующие классы из пакета `java.time`:

1. **`java.time.LocalDate`**
   - Используется для хранения только даты (без времени). Маппится на тип данных `DATE` в базе данных.
   
   **Пример:**
   ```java
   import javax.persistence.Entity;
   import javax.persistence.Id;
   import java.time.LocalDate;

   @Entity
   public class Event {
       @Id
       private Long id;
       private LocalDate eventDate;

       // Геттеры и сеттеры
   }
   ```
   **Маппинг:**
   - `java.time.LocalDate` для хранения даты в формате `DATE`.

2. **`java.time.LocalTime`**
   - Используется для хранения только времени (без даты). Маппится на тип данных `TIME` в базе данных.
   
   **Пример:**
   ```java
   import javax.persistence.Entity;
   import javax.persistence.Id;
   import java.time.LocalTime;

   @Entity
   public class Event {
       @Id
       private Long id;
       private LocalTime eventTime;

       // Геттеры и сеттеры
   }
   ```
   **Маппинг:**
   - `java.time.LocalTime` для хранения времени в формате `TIME`.

3. **`java.time.LocalDateTime`**
   - Используется для хранения даты и времени. Маппится на тип данных `TIMESTAMP` в базе данных.
   
   **Пример:**
   ```java
   import javax.persistence.Entity;
   import javax.persistence.Id;
   import java.time.LocalDateTime;

   @Entity
   public class Event {
       @Id
       private Long id;
       private LocalDateTime eventDateTime;

       // Геттеры и сеттеры
   }
   ```
   **Маппинг:**
   - `java.time.LocalDateTime` для хранения даты и времени в формате `TIMESTAMP`.

4. **`java.time.ZonedDateTime`**
   - Используется для хранения даты и времени с учетом часового пояса. Маппится на тип данных `TIMESTAMP WITH TIME ZONE` в базе данных.
   
   **Пример:**
   ```java
   import javax.persistence.Entity;
   import javax.persistence.Id;
   import java.time.ZonedDateTime;

   @Entity
   public class Event {
       @Id
       private Long id;
       private ZonedDateTime eventZonedDateTime;

       // Геттеры и сеттеры
   }
   ```
   **Маппинг:**
   - `java.time.ZonedDateTime` для хранения даты и времени с учетом часового пояса в формате `TIMESTAMP WITH TIME ZONE`.

## Заключение

Переход от старых типов данных к новым в Java 8 улучшает поддержку и управление датами и временем. Новые классы из пакета `java.time` предоставляют более удобные и надежные средства работы с датами и временем, поддерживая разнообразные форматы и зоны времени, что делает их предпочтительным выбором для современных приложений.

# 13. Как "смапить" коллекцию примитивов?

В JPA нет встроенной поддержки для маппинга коллекций примитивных типов данных (таких как `int`, `long`, `double` и т.д.). Вместо этого, вам нужно использовать коллекции объектов-оберток (такие как `Integer`, `Long`, `Double`) или специальные коллекции для хранения примитивов. 

Однако есть несколько способов работы с коллекциями примитивов в JPA:

## 1. Маппинг коллекций объектов-оберток

Если вам нужно хранить коллекции числовых значений, лучше использовать коллекции объектов-оберток. JPA поддерживает маппинг коллекций, состоящих из объектов-оберток, например, `List<Integer>`, `Set<Double>` и т.д.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.ElementCollection;
import javax.persistence.CollectionTable;
import javax.persistence.Column;
import javax.persistence.OrderColumn;
import java.util.List;

@Entity
public class Product {
    @Id
    private Long id;

    @ElementCollection
    @CollectionTable(name = "product_prices")
    @Column(name = "price")
    private List<Double> prices;

    // Геттеры и сеттеры
}
```

**Таблица в базе данных:**

- `product_prices` (с двумя столбцами: `product_id` и `price`)

## 2. Использование встроенных коллекций для хранения примитивов

Если вам действительно нужно работать с примитивами, вы можете использовать специальные коллекции, такие как `IntArrayList` или `LongArrayList` из библиотек сторонних производителей, например, из `FastUtil`.

**Пример:**

```java
import org.eclipse.persistence.jpa.JpaEntityManager;
import org.eclipse.persistence.jpa.JpaEntityManagerFactory;
import org.eclipse.persistence.jpa.JpaEntityManagerFactoryBuilder;
import org.eclipse.persistence.jpa.JpaEntityManagerFactoryImpl;
import org.eclipse.persistence.jpa.JpaEntityManagerFactorySettings;

import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.ElementCollection;
import javax.persistence.CollectionTable;
import javax.persistence.Column;
import java.util.List;
import it.unimi.dsi.fastutil.ints.IntArrayList;

@Entity
public class Product {
    @Id
    private Long id;

    @ElementCollection
    @CollectionTable(name = "product_quantities")
    @Column(name = "quantity")
    private IntArrayList quantities;

    // Геттеры и сеттеры
}
```

**Таблица в базе данных:**

- `product_quantities` (с двумя столбцами: `product_id` и `quantity`)

## 3. Использование JSON или других типов данных

В некоторых случаях вы можете использовать типы данных, такие как JSON, для хранения коллекций примитивов. Это возможно, если база данных поддерживает хранение JSON и у вас есть возможность использовать пользовательские преобразователи.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Convert;
import javax.persistence.Converter;
import javax.persistence.Column;
import java.util.List;

@Entity
public class Product {
    @Id
    private Long id;

    @Convert(converter = ListToStringConverter.class)
    @Column(name = "quantities")
    private List<Integer> quantities;

    // Геттеры и сеттеры
}

@Converter
public class ListToStringConverter implements AttributeConverter<List<Integer>, String> {

    @Override
    public String convertToDatabaseColumn(List<Integer> attribute) {
        return attribute == null ? null : attribute.toString();
    }

    @Override
    public List<Integer> convertToEntityAttribute(String dbData) {
        // Преобразуйте строку обратно в список целых чисел
        return dbData == null ? null : Arrays.stream(dbData.split(","))
                                              .map(Integer::parseInt)
                                              .collect(Collectors.toList());
    }
}
```

**Таблица в базе данных:**

- `product` (с одним столбцом `quantities`, где данные хранятся как строка JSON)

## Заключение

Для хранения коллекций примитивов в JPA рекомендуется использовать коллекции объектов-оберток, так как это наиболее совместимо с JPA и реляционными базами данных. В случае необходимости работы с примитивами можно использовать сторонние библиотеки или специальные коллекции, а также рассмотреть возможность хранения данных в формате JSON.

# 14. Какие есть виды связей?

В JPA (Java Persistence API) существуют несколько видов связей между сущностями. Основные типы связей включают в себя:

## 1. Один к одному (One-to-One)

**Описание:** Каждая сущность A связана с одной сущностью B, и каждая сущность B связана только с одной сущностью A. В этой связи одна сущность является владельцем отношения и обычно хранит внешний ключ.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.OneToOne;
import javax.persistence.JoinColumn;

@Entity
public class Person {
    @Id
    private Long id;

    @OneToOne
    @JoinColumn(name = "passport_id")
    private Passport passport;

    // Геттеры и сеттеры
}

@Entity
public class Passport {
    @Id
    private Long id;

    private String number;

    // Геттеры и сеттеры
}
```

**Особенности:**
- Используется аннотация `@OneToOne`.
- Внешний ключ обычно хранится в одной из таблиц (может быть как в таблице A, так и в таблице B).

## 2. Один ко многим (One-to-Many)

**Описание:** Каждая сущность A может быть связана с несколькими сущностями B, но каждая сущность B связана только с одной сущностью A. В этой связи одна сущность является владельцем отношения и хранит внешний ключ.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.OneToMany;
import javax.persistence.CascadeType;
import javax.persistence.FetchType;
import javax.persistence.JoinColumn;

import java.util.Set;

@Entity
public class Department {
    @Id
    private Long id;

    @OneToMany(mappedBy = "department", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private Set<Employee> employees;

    // Геттеры и сеттеры
}

@Entity
public class Employee {
    @Id
    private Long id;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;

    // Геттеры и сеттеры
}
```

**Особенности:**
- Используется аннотация `@OneToMany` на стороне родительской сущности и `@ManyToOne` на стороне дочерней сущности.
- Внешний ключ хранится в таблице дочерней сущности.

## 3. Многие к одному (Many-to-One)

**Описание:** Каждая сущность A может быть связана с одной сущностью B, но каждая сущность B может быть связана с несколькими сущностями A. Эта связь является обратной к связи "один ко многим".

**Пример:** Смотри пример для связи "Один ко многим" выше, где `Employee` связан с `Department` через аннотацию `@ManyToOne`.

**Особенности:**
- Используется аннотация `@ManyToOne` на стороне дочерней сущности и `@OneToMany` на стороне родительской сущности.

## 4. Многие ко многим (Many-to-Many)

**Описание:** Каждая сущность A может быть связана с несколькими сущностями B, и каждая сущность B может быть связана с несколькими сущностями A. Эта связь обычно требует промежуточной таблицы для хранения связей между сущностями.

**Пример:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.ManyToMany;
import javax.persistence.JoinTable;
import javax.persistence.JoinColumn;

import java.util.Set;

@Entity
public class Student {
    @Id
    private Long id;

    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses;

    // Геттеры и сеттеры
}

@Entity
public class Course {
    @Id
    private Long id;

    @ManyToMany(mappedBy = "courses")
    private Set<Student> students;

    // Геттеры и сеттеры
}
```

**Особенности:**
- Используется аннотация `@ManyToMany` и `@JoinTable` для указания промежуточной таблицы, которая хранит связи.
- Промежуточная таблица содержит два внешних ключа, каждый из которых указывает на одну из связанных таблиц.

## Заключение

Разные виды связей в JPA позволяют моделировать различные отношения между сущностями в базе данных. Правильный выбор типа связи помогает обеспечить корректное отображение данных и поддержание целостности данных в реляционных базах данных.

# 15. Что такое владелец связи?

В JPA (Java Persistence API) владелец связи — это сущность, которая отвечает за управление и хранение внешнего ключа, определяющего связь между двумя сущностями. Владелец связи указывает, в какой таблице будет находиться внешний ключ, и тем самым определяет, как будет реализована связь в базе данных.

## Роль владельца связи

1. **Определение внешнего ключа:** Владелец связи хранит внешний ключ, который связывает записи в таблицах. Этот внешний ключ указывает на строку в другой таблице и таким образом управляет связью между сущностями.

2. **Управление обновлениями:** Владелец связи управляет изменениями, такими как обновление или удаление записей, и обеспечивает согласованность данных. Если изменение требуется в таблице, содержащей внешний ключ, владелец связи будет отвечать за это изменение.

3. **Упрощение управления связями:** Являясь владельцем связи, сущность также может управлять каскадными операциями (например, `CascadeType.PERSIST`), влияющими на связанные сущности.

## Примеры

### Один к одному (One-to-One)

В связи "один к одному" владелец связи определяется аннотацией `@JoinColumn`:

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.OneToOne;
import javax.persistence.JoinColumn;

@Entity
public class Person {
    @Id
    private Long id;

    @OneToOne
    @JoinColumn(name = "passport_id")
    private Passport passport;

    // Геттеры и сеттеры
}
```

В этом примере сущность `Person` является владельцем связи, так как внешний ключ `passport_id` хранится в таблице `Person`.

### Один ко многим (One-to-Many)

В связи "один ко многим" владелец связи определяется аннотацией `@ManyToOne`:

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.ManyToOne;
import javax.persistence.JoinColumn;

@Entity
public class Employee {
    @Id
    private Long id;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;

    // Геттеры и сеттеры
}
```

В этом примере сущность `Employee` является владельцем связи, так как внешний ключ `department_id` хранится в таблице `Employee`.

### Многие ко многим (Many-to-Many)

В связи "многие ко многим" владелец связи определяется аннотацией `@JoinTable`:

```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.ManyToMany;
import javax.persistence.JoinTable;
import javax.persistence.JoinColumn;

import java.util.Set;

@Entity
public class Student {
    @Id
    private Long id;

    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses;

    // Геттеры и сеттеры
}

@Entity
public class Course {
    @Id
    private Long id;

    @ManyToMany(mappedBy = "courses")
    private Set<Student> students;

    // Геттеры и сеттеры
}
```

В этом примере сущность `Student` является владельцем связи, так как таблица `student_course` содержит внешний ключ `student_id` для связи с таблицей `Student`.

## Заключение

Владелец связи в JPA определяет, в какой таблице хранится внешний ключ и управляет связями между сущностями. Правильное назначение владельца связи важно для обеспечения целостности данных и правильной работы каскадных операций.
