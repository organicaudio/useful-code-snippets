# Spring Boot rest (with HATEOAS)

## rest general principles 

Representational State Transfer (REST) is a collection of (six) architectural constraints:

1. Client-server architecture
2. Statelessness
3. Cacheability
4. Layered system
5. Code on demand 
6. **Uniform interface**
     1. Resource identification in requests (e.g. URI)
     2. Resource manipulation through representations (client can use crud on a resource via one of its representations)
     3. Self-descriptive messages (e.g. MediaType)
     4. Hypermedia as the Engine of Application State (HATEOAS)

Hypermedia as the Engine of Application State (HATEOAS): you can find all available resources through the publication of links which point to these resources. Like a landing page of a website which leads to all further links on the website.  


## spring rest (via spring mvc)

[Official hands on guide with emphasis on hateoas](https://spring.io/guides/tutorials/rest/)
[Nice overview of topic related to rest](https://www.baeldung.com/rest-with-spring-series)

- needs **spring-boot-starter-web** as dependecy (not spring-boot-starter-jersey which is Jax_RS (Java EE))
- annotate class with **@RestController** (shorthand for @ResponseBody and @Controller) and **@RequestMapping("/")**
- use following annotations to mark a method to be exposed via 
    - @GetMapping
    - @PostMapping
    - @PutMapping
    - @DeleteMapping
    - @PatchMapping
    - RequestMapping (generic mapper/ old way)
- the @*Mapping annotations allow: 
    - to define which http verb is used
    - `value=""`. to define under which path the method is called (based on the path defined in @RequestMapping on the class) 
    - `produces=`: to define which representation formats are allowed
    - to to define path parameters e.g. @GetMapping("/{id}/specialpath")
- @ResponseStatus on a method defines the http code for a successful call
- On method parameters:
    - @RequestParam defines it to be a query-string (?id=...&name=...)
    - @PathVariable defines it as a path variable (http://rooturl.de/books/myPathVariable/)
    - @RequestBody binds the parameter to the body of the HTTP (usually used by http post)
    - note: *@PathParam and @QueryParam,* are the jax-rs annotations

## spring hateoas (HAL by default)

- add **spring-boot-starter-hateoas** dependency to add HATEOAS support.
- You have multiple options to create a RepresentationModel<T> which can hold links:
    - create a class which extends **RepresentationModel<T>**. (to set the name of the entity in the representation  use the org.springframework.hateoas.server.core.Relation Annotation)
    - wrap a collection in a **CollectionModel<T>** 
    - use **EntityModel** to wraps an existing class (`EntityModel.of(person)`)
- add a selfLink and optional further links to the RepresentationModels you want to return
- use Methods from WebMvcLinkBuilder like linkTo() to return `_links` to relevant operations
- implement RepresentationModelAssembler and the toModel method for every entity (in order to remove the code from the RestController)

*LEGACY: Spring HATEOAS Version 1.0 dropped the [resourceSupport/Resource/Resources/PagedResources group of classes](https://docs.spring.io/spring-hateoas/docs/current/reference/html/#migrate-to-1.0)*

## error handling 

- @ControllerAdvice works on **global** level for all controller beans and allows to save all @ExceptionHandler in one place
- ResponseStatusException allows to define error handling for one **method**
- [@ExceptionHandler](https://spring.io/blog/2013/11/01/exception-handling-in-spring-mvc) works only for the **class** where a method is annotated with. 
- HandlerExceptionResolver can be extended or just use [predefined implementations](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/servlet/HandlerExceptionResolver.html)

## parsing date query parameters

### on parameter level

- `@DateTimeFormat(pattern="MM/dd/yyyy")` before the parameter 
- or `@DateTimeFormat( iso=DateTimeFormat.ISO.<>)`  before the parameter 

### on application level

```java
@Configuration(proxyBeanMethods = false)
class RestConfiguration {

    public DateTimeFormatterRegistrar registrar() {
        DateTimeFormatterRegistrar registrar = new DateTimeFormatterRegistrar()
        registrar.setDateFormatter(DateTimeFormatter.ofPattern("yyyy-MM-dd"));
        registrar.setTimeFormatter(DateTimeFormatter.ofPattern("HH:mm:ss"));
        registrar.setDateTimeFormatter(DateTimeFormatter.ofPattern("yyyy-MM-dd'T'HH:mm:ss"));
        return registrar;
    }
}
```
- Set default value for a LocalDate param
    - `methodname(@RequestParam(defaultValue="#{T(java.time.LocalDate).now()}") LocalDate date)` 
    - calls to `<resturl>?requestParam=` or `<resturl>?requestParam=&requestParam2=bla` or just `<resturl>` would trigger the default value


## cache control

[Nice overview](https://www.baeldung.com/spring-security-cache-control-headers)

## evolving api

Add new fields to your JSON representations, but do not take any away (Never delete a column in a database)

## Test RestController

Use TestRestTemplate and just call the endpoints. Only make rudimentary assertions or such which can only be done on Rest like error page. Test the real logic in the service classs which provides the information to the restcontroller.

## spring data rest

[official documentation](https://docs.spring.io/spring-data/rest/docs/current/reference/html/)

When adding **spring-boot-starter-data-rest** as dependency to your spring boot project all spring data repositories will be exposed via rest api.

- by default api root is under /
- root can be changed via spring.data.rest.basePath property
- A domain class is reachable on the path under its: *(example Order is reachable under /orders)*
    1. uncapitalized
    2. pluralized (added s)
    3. simple class name 
- to prevent spring from exporting a repository add @RestResource(exported = false) to class or to a query method (you may overwrite them in your interface in order to annotate them)
- by default spring data rest uses HATEOS via HAL. When you call the basePath of spring data rest in a browser you get a overview of the exposed rest api.
- Paging and sorting is supported via query parameters when a PagingAndSortingRepository is used 
    - ?size=5
    - ?page=2
    - ?sort=name,desc
- custom query methods in Repository classes are exposed as well
    - you can configure these  with @RequestParam and @PathVariable as you would do with regular methods in a RestController 
    - if you want to use a @Query annotation at the same time use @Param and reference the paramname with leading colons (e.g. :date).
    - if you do not configure a @PathVariable they are exposed under `<host>/<entityPlural>/search/<queryMethodName>` (they appear in the hal browser!)
- you can define generic rest query urls for a spring data repository with [the Specification interface](https://www.baeldung.com/rest-api-search-language-spring-data-specifications)

## add basic auth

```java
@Configuration
public class WebserviceConfig {
    @Value("${})
    private String user;

    @Value("${})
    private String password;

    // is used for all restTemplates! You need to name the bean if you want to call mltiple domains
    @Bean
    public RestTemplate myRestTemplate(RestTemplateBuilder builder) {
        return builder.basicAuthorization(user, password).build();
    }

}
```

## Misc

General adive on spell you can: 
- call a static Method with spell: #{T(java.time.LocalDate).now()}
- call a constructor with spell: #{new java.util Date()}