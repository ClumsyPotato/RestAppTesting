# Testing in Spring Boot


---
## Unit Testing a Rest Interface



+++
## Simple GET Request 


Implementation

```java

@RestController
public class CustomerController {

    @GetMapping("/customer")
    public String getCustomer(){
        return "Unique Customer";
    }

}

```
+++

## Test class

```java

@RunWith(SpringRunner.class)
@WebMvcTest(value=CustomerController.class, secure = false)
public class CustomerControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void customerTest(){}
}
```

+++
## UnitTest implementation


```java
@Test
public void customerTest() throws Exception {

        //Build request
        RequestBuilder requestBuilder = MockMvcRequestBuilders.get(
                "/customer").accept(MediaType.APPLICATION_JSON);

        // Execute Request
        MvcResult result = mockMvc.perform(requestBuilder).andReturn();

        //Execpted String
        String expected = "Unique Customer";

        //Check if result and expected output are the same
        Assert.assertEquals(expected,result.getResponse().getContentAsString());

    }
}
```
@[4-6](darn)
@[8-10](oiii)




+++
##Moking a Service

+++
##Moking a Rest API


---
##Test Driven Development(DDD)

