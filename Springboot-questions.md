
## 1. What is an IOC container?
IoC Container is a framework for implementing automatic dependency injection. It manages object creation and its life-time and also injects dependencies into the class.



## 2. What is dependency Injection?
The process of injecting dependent bean objects into target bean objects is called dependency injection.
1. Setter Injection: The IOC container will inject the dependent bean object into the target bean object by calling the setter method.
2. Constructor Injection: The IOC container will inject the dependent bean object into the target bean object by calling the target bean constructor.
3. Field Injection: The IOC container will inject the dependent bean object into the target bean object by Reflection API.



## 3. @SpringBootApplication
Spring Boot introduces the @SpringBootApplication annotation. This single annotation is equivalent to using @Configuration, @EnableAutoConfiguration, and @ComponentScan.


## How to get the list of all the beans in your Spring boot application?
Spring Boot actuator “/Beans” is used to get the list of all the spring beans in your application.


## How to check the environment properties in your Spring boot application?
Spring Boot actuator “/env” returns the list of all the environment properties of running the spring boot application.


## What Are Possible Sources of External Configuration?
Spring Boot provides support for external configuration, allowing us to run the same application in various environments. We can use properties files, YAML files, environment variables, system properties and command-line option arguments to specify configuration properties.
We can then gain access to those properties using the @Value annotation, a bound object via the @ConfigurationProperties annotation, or the Environment abstraction.

## Why field level autowiring is not recommended ?
1. Field injection creates a risk of NullPointerException if dependencies aren’t correctly initialized.
2. Using the field injection, we are unable to create immutable classes.
```
 We need to instantiate the final fields when they’re declared or through the constructor. Furthermore, Spring performs autowiring once the constructors have been called. Therefore, it’s impossible to autowire the final fields using field injection.
```
3. Single Responsibility Violation
We can easily add more dependencies than necessary and create a class that’s doing more than one job.
4. Circular Dependencies


## @Autowired - we can use autowiring on properties, setters, and constructors.

## @Qualifier - 
1. When there are multiple beans of the same type, it’s a good idea to use @Qualifier to avoid ambiguity.
2. If more than one bean of the same type is available in the container, the framework will throw a fatal exception.
3. To resolve this conflict, we need to tell Spring explicitly which bean we want to inject.


##
