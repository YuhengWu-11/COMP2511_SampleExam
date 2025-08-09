# COMP2511 Sample Exam Q1–Q8 翻译与详解

## 目录
- [Q1](#q1)
- [Q2](#q2)
- [Q3](#q3)
- [Q4](#q4)
- [Q5](#q5)
- [Q6](#q6)
- [Q7](#q7)
- [Q8](#q8)

---

## Q1
### Question
A computer science student has many hopes and dreams.

The above relationship is an example of:  
A) Aggregation  
B) Composition  
C) Neither

### 中文逐字翻译
一名计算机科学学生拥有许多“希望与梦想”。  

上述关系属于以下哪一种：  
A）聚合（Aggregation）  
B）组合（Composition）  
C）都不是

### 答案
A) Aggregation

### 解析
“拥有许多 X”通常表示弱所有权，且生命周期不绑定：学生即使不存在，“希望/梦想”这种概念依然可以独立存在。  
这符合**聚合**的定义，而非组合。组合要求部分随整体生命周期结束而消亡。

### 相关知识点
- 聚合（Aggregation）：整体与部分生命周期独立，弱所有权。例如：班级–学生、图书馆–书。
- 组合（Composition）：部分不能脱离整体，生命周期绑定，强所有权。例如：房屋–房间、订单–订单行。
- 判断方法：部分对象是否可以独立存在？可以 → 聚合；不可以且随整体消亡 → 组合。

---

## Q2
### Question
Consider the following lambda function which prints log. The type signature has been redacted.

[redacted] logger = log -> System.out.println(log);

Pick the most semantically correct type from the list below:  
A) Function<String, Boolean>  
B) Consumer<String>  
C) Predicate<String>  
D) Supplier<String>

### 中文逐字翻译
考虑如下会打印日志的 lambda（类型签名已隐去）：  

[已隐藏] logger = log -> System.out.println(log);

从下列选项中选择语义上最正确的类型：  
A）Function<String, Boolean>  
B）Consumer<String>  
C）Predicate<String>  
D）Supplier<String>

### 答案
B) Consumer<String>

### 解析
该 lambda 接受一个 `String` 参数并执行副作用（打印），没有返回值。  
Java 中 `Consumer<T>` 用于接收一个参数且无返回值，这与题意最符合。  
`Function<T,R>` 需要返回值；`Predicate<T>` 返回布尔值；`Supplier<T>` 不接收参数。

### 相关知识点
- `Consumer<T>`：接收 T，无返回值。
- `Function<T,R>`：接收 T，返回 R。
- `Predicate<T>`：接收 T，返回 boolean。
- `Supplier<T>`：无参数，返回 T。

---

## Q3
### Question
Which design pattern is most appropriate for the following scenario.

You have a program that needs to print error messages from multiple methods. All such error messages must be sent to the file called "error.txt".

A) Factory  
B) Strategy  
C) Singleton  
D) Composite  
E) Decorator

### 中文逐字翻译
以下场景最适合使用哪种设计模式？  

你的程序需要在多个方法中打印错误信息，且所有错误必须写入同一个文件 `error.txt`。

A）工厂  
B）策略  
C）单例  
D）组合  
E）装饰

### 答案
C) Singleton

### 解析
典型的全局日志器需求：需要唯一的日志对象管理文件写入，避免多个实例造成的文件句柄冲突或状态不一致。  
单例模式保证全局唯一性并集中管理日志输出。

### 相关知识点
- 单例模式：全局唯一、集中管理资源。
- 适用场景：配置管理、日志器、线程池。
- 注意线程安全和测试替代性。

---

## Q4
### Question
Which of the following would be a valid use case for `instanceof` instead of `getClass()` for checking the type of an object?

A) Checking if an object complies with an interface so that we can use a method on that interface  
B) Implementing the equals method for an object  
C) It's a trick question, you should never use instanceof in your code at all

### 中文逐字翻译
在判断对象类型时，下面哪一项是使用 `instanceof` 而不是 `getClass()` 的合理用例？  

A）检查对象是否实现了某个接口，从而可以调用该接口的方法  
B）在实现 `equals` 方法时  
C）陷阱题：代码里永远不该用 `instanceof`

### 答案
A

### 解析
`instanceof` 判断对象是否是某类型或其子类型，或是否实现了某接口。  
在需要多态调用的场景（如接口方法调用）中，`instanceof` 更合适。  
`getClass()` 检查精确类型，通常用于实现 `equals` 保证对称性。

### 相关知识点
- `instanceof`：多态类型判断。
- `getClass()`：精确类型比较。
- Java 16+ 支持 `instanceof` 模式匹配。

---

## Q5
### Question
The following is taken from a student's Assignment II blog.

“In Assignment II, after I completed Part 1 Task 1 and refactored the code, I started work on Part 1 Task 2 but found I had to go and modify everything because the design didn't work with the new requirements.”

Which SOLID principle is being violated? Select the most suitable answer.  
A) Single Responsibility Principle  
B) Open-Closed Principle  
C) Liskov Substitution Principle  
D) Interface Segregation Principle  
E) Dependency Inversion Principle

### 中文逐字翻译
以下摘自某学生的 A2 博客：  

“在完成 Part 1 Task 1 并重构后，我开始做 Task 2，却发现必须修改很多地方，因为原设计无法适应新需求。”

违反了哪条 SOLID 原则？  
A）单一职责  
B）开闭原则  
C）里氏替换  
D）接口分离  
E）依赖倒置

### 答案
B) Open-Closed Principle

### 解析
开闭原则：对扩展开放，对修改关闭。  
每次有新需求就需要大幅修改旧代码，说明没有遵守 OCP。

### 相关知识点
- OCP：通过抽象、接口预留扩展点。
- 常用模式：策略、模板方法、装饰。

---

## Q6
### Question
Which design patterns are particularly focused on inter-object communication?

A) Creational Patterns  
B) Structural Patterns  
C) Behavioural Patterns  
D) All of the Above

### 中文逐字翻译
哪类设计模式更关注对象之间的通信与协作？  

A）创建型  
B）结构型  
C）行为型  
D）以上全部

### 答案
C) Behavioural Patterns

### 解析
行为型模式（如观察者、命令、中介者、策略等）主要解决对象之间的职责分配和交互方式。

### 相关知识点
- 行为型模式：Observer、Strategy、Command、Mediator、State、Visitor 等。
- 创建型关注对象创建；结构型关注类和对象的组合。

---

## Q7
### Question
Which architectural style is best for quick MVP development with a small team?

A) Event-Driven  
B) Layered Architecture  
C) Microservices  
D) Serverless

### 中文逐字翻译
小团队要快速完成 MVP，最适合的架构风格是？  

A）事件驱动  
B）分层架构  
C）微服务  
D）Serverless

### 答案
B) Layered Architecture

### 解析
MVP 追求快速交付和低复杂度，分层架构简单清晰，部署成本低，易于维护。  
微服务、事件驱动前期架构成本高，Serverless 对云依赖重。

### 相关知识点
- 分层架构：表示层、业务层、数据层。
- MVP 阶段建议单体+分层，预留未来拆分空间。

---

## Q8
### Question
What is a major limitation of event-driven architecture (EDA)?

A) High coupling between services  
B) Poor scalability  
C) Complex debugging and tracing due to asynchronous flows  
D) Slow response time under load

### 中文逐字翻译
事件驱动架构的主要局限之一是？  

A）服务间高度耦合  
B）可扩展性差  
C）由于异步导致的调试与追踪复杂  
D）高负载下响应慢

### 答案
C

### 解析
EDA 优势是解耦和扩展性，但异步和最终一致性会增加调试、链路追踪和故障定位的复杂度。

### 相关知识点
- EDA 的常见问题：异步调试难、消息丢失、顺序保证。
- 常用手段：分布式追踪、幂等处理、死信队列。
