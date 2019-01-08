# Testing in Spring Boot


---
## Unit Testing a simple Rest Endpoint


+++
## Implementation

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
## Unit Test Method


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
@[4-6](Create a stubbed request)
@[8,9](Execute the request and safe it)
@[11,12](Declare expected output)
@[14,15](Compare the expected value to the actual result)




---
## Mocking a Service
+++
## Implementation

``` java
  @GetMapping("/Customer/name/{id}")
  public String getCustomerName(@Pathvariable("id") long id){
        return customerService.getCustomerName(id);
    }

```

+++
## Unit Test

```java
 @Test
    public void customerTest() throws Exception {
        String expected = "Steve"
        Mockito.when(customerService.getCustomerName(Mokito.anyLong())).thenReturn(expected);

        RequestBuilder requestBuilder = MockMvcRequestBuilders.get(
                "/Customer/name/2").accept(MediaType.APPLICATION_JSON);

        MvcResult result = mockMvc.perform(requestBuilder).andReturn();

        Assert.assertEquals(exptected,result.getResponse().getContentAsString());

    }
```

---
## Mocking a Rest API


+++
#Unit Test

``` java
   public String getCustomerBalance(String id){
        ResponseEntity<String> responseEntity = restTemplate.getForEntity("http://financialservice:8080/balance/"+id, String.class);
        return responseEntity.getBody();
    }
```
+++

## Unit Test

``` java
    @Test
    public void customerBalanceTest(){

        String expectedBalance = "100";


        Mockito
                .when(restTemplate.getForEntity("http://financialservice:8080/balance/"+expectedBalance ,String.class))
                .thenReturn(new ResponseEntity<>(expectedBalance, HttpStatus.OK));

        String actualBalance =customerService.getCustomerBalance(expectedBalance);
        Assert.assertEquals((expectedBalance), actualBalance);
    }
```


---
## Test Driven Development(DDD)

+++?image=assets/img/tdd.jpeg&size=80%