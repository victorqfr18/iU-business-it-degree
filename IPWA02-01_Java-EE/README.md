# Programming Information Systems with Java EE (IPWA02-01)

> B.Sc. Business IT — IU International Hochschule
> Module passed: April 2026 (estimated ~74%)

A study log and reference of the concepts I worked through to pass this module's exam. This isn't a project repo — it's documentation of what I learned, the concepts I had to wrestle with, and code patterns I drilled until I could reproduce them under exam conditions.

---

## About the Module

This module covers building **server-side Java web applications** using the Java EE / Jakarta EE stack. The main components:

- **JSF (JavaServer Faces)** — component-based web UI framework
- **CDI (Contexts and Dependency Injection)** — bean management
- **PrimeFaces** — third-party JSF component library
- **JPA (Java Persistence API)** + **Hibernate** — object-relational mapping for databases

The course follows a layered MVC stack: the user's browser sends an HTTP request → JSF processes it through a 6-phase lifecycle → CDI beans handle data and logic → JPA persists data to a relational database → JSF renders an HTML response back to the browser.

---

## Exam Format

- 15 multiple-choice questions (3 points each = 45 points)
- 5 written questions (6–10 points each = 35 points)
- 80 points total, 50% to pass
- Online proctored

---

## What I Learned

### Unit 1 — Component-Based Web User Interfaces
- The **JSF lifecycle** has 6 phases in this exact order:
  1. Build component tree
  2. Read input from HTTP request
  3. Input fields validation
  4. Data model update
  5. Invoke application
  6. Render HTML response
- The browser never sees JSF tags — the server converts XHTML to plain HTML before sending the response.
- **Namespaces** unlock different tag libraries:
  - `xmlns="http://www.w3.org/1999/xhtml"` — standard HTML
  - `xmlns:h="http://xmlns.jcp.org/jsf/html"` — JSF HTML components
  - `xmlns:f="http://xmlns.jcp.org/jsf/core"` — JSF core utilities
- The **component tree** holds one Java object for every HTML component on the page.
- `<h:dataTable>` iterates over a list of objects — the `var` attribute is the loop variable, the `value` attribute is the collection.

### Unit 2 — Connecting View and Model
- **CDI beans** are managed by the **CDI container**.
- A valid bean needs: `@Named`, a scope annotation, `Serializable`, a parameterless constructor, and getters/setters.
- **Bean scopes** (in order of lifespan, shortest to longest):
  - `@Dependent` — default if no scope is given
  - `@RequestScoped` — single HTTP request
  - `@ViewScoped` — while user stays on the same page
  - `@SessionScoped` — entire user session
  - `@ApplicationScoped` — entire application lifetime, shared across all users
- **Convention over configuration**: a class named `ProductController` is accessed in UEL as `productController` (only the first letter lowercases — internal capitals stay).
- Override the convention with `@Named("customName")`.
- Controller navigation: `<h:commandLink action="#{controller.method}"/>` — the method returns a String that JSF interprets as the target page.

### Unit 3 — Component Libraries
- **PrimeFaces** is a third-party library with 100+ JSF components, used because building custom components is slow, error-prone, and requires design experience.
- Three steps to include PrimeFaces:
  1. Add the dependency in `POM.XML` (Maven), with `<classifier>jakarta</classifier>` for JSF projects
  2. Import the namespace: `xmlns:p="http://primefaces.org/ui"`
  3. Add components using the `p:` prefix
- Useful components: `p:datePicker`, `p:dialog`, `p:confirmDialog`, `p:breadCrumb`, `p:textEditor`, `p:colorPicker`, `p:fileUpload`, `p:tooltip`.
- **`widgetVar`** gives a component a JavaScript-accessible name. **`PF('name')`** retrieves it from JavaScript.

### Unit 4 — Programming of Business Logic
- **Four types of input validation**:
  - Mandatory: `required="true"`
  - Format: `<f:validateRegex pattern="..."/>`
  - Technical (range/length): `<f:validateLongRange>`, `<f:validateDoubleRange>`, `<f:validateLength>`
  - User-defined: `validator="#{bean.method}"`
- **Conversion**:
  - `<f:convertNumber type="number|currency|percent"/>` for numbers
  - `<f:convertDateTime type="date|time"/>` for dates and times
- **Error messages**:
  - `<h:message for="fieldId"/>` — error for one specific field
  - `<h:messages/>` — errors for the whole form
  - Custom error texts go in **properties files** (not in beans), which override the system standard messages
- **JSF events** fall into three categories: action events, value change events, phase events.

### Unit 5 — Database Connections
- **ACID** — the four properties of a reliable persistence solution:
  - Atomicity — all or nothing
  - Consistency — data stays valid before and after a transaction
  - Isolation — concurrent transactions don't interfere
  - Durability — committed data survives system failure
- **Object-relational mapping (ORM)** translates between Java objects and database tables:
  - Class → Table
  - Object → Row (data record)
  - Attribute → Column
- **Hibernate** is the most popular ORM library; it implements the JPA specification.
- **5 JPA core classes/interfaces**:
  - `EntityManager` — searches and manages database objects
  - `EntityTransaction` — handles begin/commit/rollback
  - `EntityManagerFactory` — creates EntityManagers
  - `Persistence` — static class that creates the factory
  - `Query` — runs SELECT/UPDATE/DELETE queries
- **CRUD with EntityManager**:
  - `persist(entity)` — create
  - `find(Class, id)` — read
  - `merge(entity)` — update
  - `remove(entity)` — delete
- **Lock-based concurrency**:
  - Shared lock — read-only
  - Exclusive lock — read and write
  - Two-phase lock method — request, obtain, release

---

## Code Patterns I Drilled Until I Could Write Them From Memory

### JSF tags linked to a CDI bean via deferred UEL
```xml
<h:outputText value="#{product.name}"/>
<h:inputText value="#{person.email}"/>
```

### `h:dataTable` displaying a list
```xml
<h:dataTable var="product" value="#{store.products}">
    <h:column>
        <f:facet name="header">Name</f:facet>
        <h:outputText value="#{product.name}"/>
    </h:column>
    <h:column>
        <f:facet name="header">Price</f:facet>
        <h:outputText value="#{product.price}"/>
    </h:column>
</h:dataTable>
```

### Number formatted as a percentage
```xml
<h:outputText value="#{bean.number}">
    <f:convertNumber type="percent" minFractionDigits="2" maxFractionDigits="2"/>
</h:outputText>
```

### Input field with validation and error display
```xml
<h:inputText id="price" value="#{controller.price}">
    <f:validateDoubleRange minimum="0.00"/>
</h:inputText>
<h:message for="price"/>
```

### Controller-driven navigation
```java
public String validateUserInfo() {
    if (username.isEmpty() || password.isEmpty()) {
        return "error";
    } else {
        return "result";
    }
}
```

### A complete JPA entity
```java
@Entity
@Table(name="PERSONS")
public class Person {
    @Id
    private int personID;

    @Column(name="PERSON_NAME")
    private String name;
}
```

### The transaction wrapper for any database write
```java
em.getTransaction().begin();
em.persist(entity);     // or em.merge(entity), em.remove(entity)
em.getTransaction().commit();
```

---

## Honest Notes on My Process

- **The hard lesson from this module**: reading the course book without actively drilling does not work. After the first two units, my unit-test scores were only 2/5 because I was learning concepts but not memorising the specific tag names, attribute names, and exact terminology that the exam tests. Once I corrected that — reading every detail of the slides + course book and drilling them rapid-fire — scores climbed to 3/5 and 4/5.
- **MC questions and written questions need separate preparation.** Recognising the right answer in a list is much easier than producing code on a blank page. I wrote the JPA entity class out from scratch multiple times until it was automatic.
- **The exam includes deliberate trap options** that only differ by one or two characters from the correct answer (`h:image` vs `h:graphicImage`, `@PrimaryKey` vs `@Id`, `xmlns:pf` vs `xmlns:p`). Slowing down by five seconds on each MC question to check for traps was the single biggest behavioural fix I made.
- **My biggest miss on the actual exam** was misunderstanding "areas of validity" as the validation phase, when it actually refers to bean scopes (`@RequestScoped`, `@SessionScoped`, etc.). The term comes from how long a bean is "valid" in memory.
- **What I'd do differently next time**: start from the practice exam much earlier, not as a final check. Working backwards from the questions reveals which details actually matter and avoids wasting time on parts of the book that don't get tested.

---

## Final Result

Passed on the first attempt. Estimated score ~59/80 (74%). 12/14 on multiple choice; written questions varied from solid to weak depending on whether I'd drilled the specific terminology beforehand.
