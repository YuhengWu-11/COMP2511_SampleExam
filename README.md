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

### 解析（为什么选 A；B、C 不合适在哪）
- 选 **A 聚合**：描述是“学生拥有许多希望与梦想”。**希望/梦想**作为“部分”，其**存在不依赖于**“学生”这一“整体”的生命周期（学生不在了，希望/梦想这个抽象仍然可被视为独立概念），这符合**弱所有权**与**生命周期不绑定**的特征，因此是聚合。
- **B 组合不合适**：组合要求**强所有权**与**组合生命周期**（整体消亡 ⇒ 部分必消亡），典型如“房屋–房间”“身体–器官”。而“希望/梦想”明显不满足这种强依附关系。
- **C 都不是不合适**：这段话清晰表达了“整体（学生）—部分（希望/梦想）”的拥有关系，属于面向对象建模中的**整体–部分**范畴，不是“都不是”。

### 相关知识点（覆盖所有选项与题面名词）
- **Aggregation（聚合）**：空心菱形；弱所有权；部分可独立存在/复用；如“图书馆–书”“班级–学生”。
- **Composition（组合）**：实心菱形；强所有权；部分与整体同生共死；如“房屋–房间”“订单–订单行”。
- **判断技巧**：问自己——部分是否**必须**依赖整体生存？若必须 ⇒ 组合；若不必须 ⇒ 聚合。  
- **易错点**：很多“has many”都想当然被画成组合；要结合**生命周期**来判断，而不是看语义表面。

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

### 解析（为什么选 B；A、C、D 不合适在哪）
- 选 **B Consumer<String>**：该 lambda 接收一个 `String` 入参 `log`，执行副作用（打印），**没有返回值**。这与 `Consumer<T>` 的签名 `void accept(T t)` 完全匹配。
- **A Function<String, Boolean>** 不合适：`Function<T,R>` 必须返回 `R`，而题干没有返回值。
- **C Predicate<String>** 不合适：`Predicate<T>` 返回 `boolean`，也与题干不符。
- **D Supplier<String>** 不合适：`Supplier<T>` **不接收参数**，只提供一个返回值，和题干相反。

### 相关知识点（覆盖所有选项与题面名词）
- **Java 常用函数式接口**  
  - `Consumer<T>`：消费一个参数、无返回（常用于日志、收集、输出）。  
  - `Function<T,R>`：输入 T、输出 R（常用于映射/转换）。  
  - `Predicate<T>`：输入 T、输出 boolean（常用于过滤/条件判断）。  
  - `Supplier<T>`：无输入、提供 T（常用于懒加载、缓存提供）。  
- **语义优先**：尽管编译器可做类型推断，但**选择题**强调“最语义正确”，即与**副作用+无返回**最匹配的 `Consumer`。  
- **副作用函数的设计**：日志打印、写文件、发送消息等，通常建模为 `Consumer<T>`。

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

你的程序需要在多个方法中打印错误信息，且所有错误都必须写入同一个文件 `error.txt`。

A）工厂  
B）策略  
C）单例  
D）组合  
E）装饰

### 答案
C) Singleton

### 解析（为什么选 C；A、B、D、E 不合适在哪）
- 选 **C 单例**：要求“所有方法都写入同一个文件”，这是**全局唯一资源**（日志器/文件输出通道）的经典场景。单例保证只存在一个日志器实例，集中管理文件句柄、格式、并发写。
- **A 工厂** 不解决“唯一性/共享”的问题，它只负责**创建**对象，而不是保证单一实例或集中写入。
- **B 策略** 是切换算法/行为（例如不同日志格式/输出策略），可作为**补充**，但不解决“全局共享唯一日志器”的需求。
- **D 组合** 解决“整体–部分”结构，与日志场景无关。
- **E 装饰** 用于**动态叠加行为**（比如在写日志前后增加打点、加密），是增强手段，不负责全局唯一。

### 相关知识点（覆盖所有选项与题面名词）
- **Singleton（单例）**：全局唯一、集中配置、避免重复打开文件；注意**线程安全**（懒汉/饿汉/枚举）、**可测试性**（可用依赖注入替代硬单例）。
- **Factory（工厂）**：解耦创建；可与单例结合（单例工厂），但**仅工厂**无法保证唯一。
- **Strategy（策略）**：可让日志器在**同一实例**内切换不同输出策略（控制台/文件/远端）。
- **Decorator（装饰）**：在不改动核心日志器的情况下，叠加“打点/缓存/重试/加密”等责任。
- **日志设计的组合拳**：**单例日志器** + 可插拔**策略** + 可选**装饰**增强，是常见且优雅的组合。

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

### 解析（为什么选 A；B、C 不合适在哪）
- 选 **A**：`instanceof` 的语义是“是否为某类型**或其子类型**/是否实现接口”。当我们只关心“**能否当作接口用**”（以便安全地多态调用接口方法）时，`instanceof` 是正确工具。
- **B** 不合适：实现 `equals` 时一般推荐用 `getClass()` 做精确类型比较，避免**跨子类比较**破坏对称性/传递性。若用 `instanceof`，`A.equals(B)` 可能与 `B.equals(A)` 语义不对称。
- **C** 不合适：`instanceof` 是正常的语言特性，在多态落地、适配器、访问者等场景中是合理工具；关键是**用得对**。

### 相关知识点（覆盖所有选项与题面名词）
- **`instanceof`**：检查“是否为某类型或其子类型”；Java 16+ 支持**模式匹配**：`if (o instanceof Foo f) { f.bar(); }`。
- **`getClass()`**：返回对象运行时**精确类**；在 `equals` 实现中常用于严格保证等价关系。
- **`equals` 的等价关系**：自反、对称、传递、一致、与 `hashCode` 约定；错误的类型判断易破坏这些性质。
- **接口合规检查**：当目标是“能否当作某接口使用”，优先考虑 `instanceof 接口` + 多态调用。

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

“在完成 Part 1 Task 1 并重构后，我开始做 Task 2，却发现必须把很多地方都改掉，因为原设计无法适应新需求。”

违反了哪条 SOLID 原则？（选择最合适的一个）  
A）单一职责  
B）开闭原则  
C）里氏替换  
D）接口分离  
E）依赖倒置

### 答案
B) Open-Closed Principle

### 解析（为什么选 B；A、C、D、E 不合适在哪）
- 选 **B 开闭原则**：OCP 要求**对扩展开放、对修改关闭**。若新需求一来就要**大面积修改**既有代码，说明抽象未能承载变化，违反 OCP。
- **A 单一职责**：SRP 是“一个类只对一种引起变化的原因负责”。文段强调“无法适应新需求导致处处修改”，**指向的是扩展性问题**，而非职责数目问题。
- **C 里氏替换**：关注子类型替换父类型的行为一致性；没有迹象表明存在“子类不能替换父类”的问题。
- **D 接口分离**：关注接口是否过胖/强迫实现无关方法；文段未体现“接口过大”的困扰。
- **E 依赖倒置**：面向抽象而非细节；虽然有时能改善扩展性，但文段直接反映的是“修改旧代码”，更直接对应 OCP。

### 相关知识点（覆盖所有选项与题面名词）
- **OCP（开闭原则）**：稳定点在抽象，变化通过新增实现类、策略、装饰等**扩展**承载；**不要修改**已稳定、被广泛依赖的核心类。
- **SRP（单一职责）**：识别“变化的原因”，聚合相同变化，分离不同变化；提高可维护性。
- **LSP（里氏替换）**：子类必须遵守父类契约；违例通常表现为**违反前置/后置条件或不变式**。
- **ISP（接口分离）**：优先小接口、角色接口；避免“胖接口”造成不必要依赖。
- **DIP（依赖倒置）**：高层与低层都依赖抽象；通过接口、依赖注入削弱耦合，促进可测试性与可替换性。

## Q6
### Question
Which design patterns are particularly focused on inter-object communication?

A) Creational Patterns  
B) Structural Patterns  
C) Behavioural Patterns  
D) All of the Above

### 中文逐字翻译
哪一类设计模式更关注对象之间的通信/协作？

A）创建型  
B）结构型  
C）行为型  
D）以上全部

### 答案
C) Behavioural Patterns

### 解析（为什么选 C；A、B、D 不合适在哪）
- 选 **C 行为型**：这类模式（Observer、Mediator、Command、Strategy、State、Visitor…）核心关注**对象间的职责分配与交互协议**。
- **A 创建型**：关注**如何创建**对象（如工厂、建造者、单例），不是通信本身。
- **B 结构型**：关注**如何组合**类与对象（如适配器、桥接、装饰、组合、门面、享元、代理），也非通信焦点。
- **D 以上全部** 不准确：虽然所有模式会涉及协作，但**“特别关注通信”**是行为型的特征定位。

### 相关知识点（覆盖所有选项与题面名词）
- **行为型**：Observer（发布订阅）、Mediator（中介协调）、Command（请求封装）、Strategy（算法切换）、State（状态驱动）、Visitor（分发算法）。
- **结构型**：Adapter（接口转换）、Bridge（抽象与实现分离）、Decorator（叠加职责）、Composite（树形结构）、Facade（统一外观）、Flyweight（共享细粒度对象）、Proxy（代理访问）。
- **创建型**：Factory Method、Abstract Factory、Builder、Prototype、Singleton。
- **复习建议**：按“**动机—结构—适用性—权衡**”来记忆，每个模式至少有一个现实类比和代码雏形。

## Q7
### Question
Which architectural style is best for quick MVP development with a small team?

A) Event-Driven  
B) Layered Architecture  
C) Microservices  
D) Serverless

### 中文逐字翻译
小团队要快速做出 MVP，最合适的架构风格是？

A）事件驱动  
B）分层架构  
C）微服务  
D）Serverless

### 答案
B) Layered Architecture

### 解析（为什么选 B；A、C、D 不合适在哪）
- 选 **B 分层架构**：目标是**快速产出**与**降低复杂度**。单体应用 + 清晰分层（表示/业务/数据）上手快、部署简单、观察性与调试成本低，**最匹配小团队的 MVP**。
- **A 事件驱动**：需要引入消息中间件、异步一致性、事件治理（幂等、重试、死信队列、追踪），对**基础设施与经验**要求较高。
- **C 微服务**：带来团队/发布/扩缩容的优势，但前期需要**服务拆分、服务发现、网关、配置中心、链路追踪、CI/CD** 等较重投入，**性价比低**。
- **D Serverless**：能加速上线，但**冷启动、平台绑定、可观测性、状态管理**等都需权衡；课程场景默认一般不首选。

### 相关知识点（覆盖所有选项与题面名词）
- **分层架构实践**：Controller（表示）/Service（业务）/Repository（数据）；边界清晰、易于单元测试；后续可按模块做“**逐步服务化**”。
- **事件驱动（EDA）**：高解耦、高扩展；但要解决**异步调试**、**最终一致性**、**顺序语义**。
- **微服务**：组织与架构匹配（康威定律）；适合**足够大**的团队规模和**稳定的运维能力**。
- **Serverless**：函数即服务（FaaS）、后端即服务（BaaS）；适合事件触发型、小而离散的任务。

## Q8
### Question
What is a major limitation of event-driven architecture (EDA)?

A) High coupling between services  
B) Poor scalability  
C) Complex debugging and tracing due to asynchronous flows  
D) Slow response time under load

### 中文逐字翻译
事件驱动架构（EDA）的主要局限之一是？

A）服务间高度耦合  
B）可扩展性差  
C）由于异步流程导致的调试与追踪复杂  
D）在负载下响应缓慢

### 答案
C

### 解析（为什么选 C；A、B、D 不合适在哪）
- 选 **C 异步调试与追踪复杂**：EDA 通过事件异步解耦，但**跨服务链路**变长且非线性，导致问题定位、因果还原、幂等保障更难，需要分布式追踪（trace id）、日志关联、死信队列、重放机制等。
- **A 高耦合** 不成立：EDA 的优势恰恰是**降低耦合**（发布者与订阅者解耦）。
- **B 可扩展性差** 不成立：EDA 往往更易水平扩展（消费者实例数可弹性伸缩）。
- **D 响应慢** 不准确：异步往往**改善**峰值吞吐和用户体验（前端快速 ACK），瓶颈更多来自错误的设计/实现，而非 EDA 本身。

### 相关知识点（覆盖所有选项与题面名词）
- **EDA 的治理要点**：分布式追踪（trace/span）、幂等键、去重、重试与退避、死信队列、顺序保证（分区/键控）、补偿事务（Saga）。
- **耦合类型**：时间耦合/空间耦合/语义耦合；消息中间件可打破时间耦合，但语义耦合仍需良好事件建模（事件名、负载 schema、版本化）。
- **可扩展性**：消费者横向扩容 + 分区并行；注意“至少一次/至多一次/恰好一次”的交付语义与成本。
