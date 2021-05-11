# java templates

## junit 5 + hamcrest static imports

```java
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.Matchers.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.*;

class TestExample {

    ObjectUnderTest out;

    @BeforeAll
    public static void setup() {
        System.out.println("BeforeAll");
    }

    @BeforeEach
    public void init() {
        System.out.println("BeforeEach");
        this.out = new ObjectUnderTest();
    }

    @AfterEach
    void terminate() {
        System.out.println("AfterEach");
    }

    @AfterAll
    public static void tearDown() {
        System.out.println("AfterAll");
    }

    @Test
    void methodUnderTest_shouldReturnAllFields() {
        System.out.println("methodUnderTest_shouldReturnAllFields");
        Integer count = out.methodUnderTest();
        assertNotNull(count);
        assertThat(count, is(greaterThan(300)));
    }

    @Test
    void methodUnderTest_expectsException() {
        System.out.println("methodUnderTest_expectsException");
        Exception exception = assertThrows(
			RuntimeException.class,
			() -> out.methodUnderTest("NOT VALID"));
        assertTrue(exception.getMessage().contains("NOT VALID"));
    }

    @Disabled
    @Test
    void methodUnderTest_shouldNotRun() {
        System.out.println("I will not run.");
    }


    // inner class
    class ObjectUnderTest {

        public int methodUnderTest(){
            return 301;
        }

        public int methodUnderTest(String notValid) {
            throw new RuntimeException(notValid);
        }
    }
}
}

```

## jackson: java -> json & json -> java

```xml
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-databind</artifactId>
	<version></version>
</dependency>
```
```java
import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.ObjectWriter;

...
//java to json
ObjectWriter ow = new ObjectMapper().writer().withDefaultPrettyPrinter();
String json = ow.writeValueAsString(object);
String jsonWithType = String.format("\"%s\": %s", object.getClass().getSimpleName(), json);

// json to java
ObjectMapper objectMapper = new ObjectMapper();
Object object2 = objectMapper.readValue(jsonWithType, Object.class);
```
