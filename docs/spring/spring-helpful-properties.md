# Spring Boot useful properties

```properties
# show executed sql statement in logs
spring.jpa.show-sql=true 

# creates the tables from provided entities
spring.jpa.generate-ddl=true

# deletes old tables before recreating them
spring.jpa.hibernate.ddl-auto=create-drop

# activate h2  console (automatically set by developer tools, when app is started in exploded form)
spring.h2.console.enabled=true

# access of h2 console from other client
spring.h2.console.settings.web-allow-others=true

```