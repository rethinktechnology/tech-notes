# Spring framework

## Modules
- Spring framework underlying architecture modules
	- spring core
	- spring bean
	- spring context
	- spring EL
- Spring Data
- Spring Web
- Spring AoP

### Spring's Stereotype
#####  org.springframework.stereotype.Component
Indicates that an annotated class is a "component". Such classes are considered as candidates for auto-detection when using annotation-based configuration and classpath scanning.

Other class-level annotations may be considered as identifying a component as well, typically a special kind of component: e.g. the  `@Repository`  annotation or AspectJ's  `@Aspect`  annotation.

##### org.springframework.stereotype.Repository
Indicates that an annotated class is a "Repository", originally defined by Domain-Driven Design (Evans, 2003) as "a mechanism for encapsulating storage, retrieval, and search behavior which emulates a collection of objects".

Teams implementing traditional J2EE patterns such as "Data Access Object" may also apply this stereotype to DAO classes, though care should be taken to understand the distinction between Data Access Object and DDD-style repositories before doing so. This annotation is a general-purpose stereotype and individual teams may narrow their semantics and use as appropriate.

A class thus annotated is eligible for Spring  `DataAccessException`  translation when used in conjunction with a  `PersistenceExceptionTranslationPostProcessor`. The annotated class is also clarified as to its role in the overall application architecture for the purpose of tooling, aspects, etc.

##### org.springframework.stereotype.Service
Indicates that an annotated class is a "Service", originally defined by Domain-Driven Design (Evans, 2003) as "an operation offered as an interface that stands alone in the model, with no encapsulated state."

May also indicate that a class is a "Business Service Facade" (in the Core J2EE patterns sense), or something similar. This annotation is a general-purpose stereotype and individual teams may narrow their semantics and use as appropriate.

##### org.springframework.beans.factory.annotation.Value
Annotation at the field or method/constructor parameter level that indicates a default value expression for the affected argument.

Typically used for expression-driven dependency injection. Also supported for dynamic resolution of handler method parameters, e.g. in Spring MVC.

A common use case is to assign default field values using "#{systemProperties.myProp}" style expressions.

Note that actual processing of the  `@Value`  annotation is performed by a  `BeanPostProcessor`  which in turn means that you  _cannot_use  `@Value`  within  `BeanPostProcessor`  or  `BeanFactoryPostProcessor`  types. Please consult the javadoc for the  `AutowiredAnnotationBeanPostProcessor`  class (which, by default, checks for the presence of this annotation).

### Spring Cloud Config
-   Spring Cloud configuration server allows you to set up application properties with environment specific values.
    
-   Spring uses Spring profiles to launch a service to determine what environment properties are to be retrieved from the Spring Cloud Config service.
    
-   Spring Cloud configuration service can use a file-based or Git-based application configuration repository to store application properties.
    
-   Spring Cloud configuration service allows you to encrypt sensitive property files using symmetric and asymmetric encryption.
