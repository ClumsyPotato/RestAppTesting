# Testing in Spring Boot


---
## Unit Testing a Rest Interface



+++
## Simple GET Request 



´´´java

@RestController
public class CustomerController {

    @GetMapping("/customer")
    public String getCustomer(){
        return "Customer";
    }

}

```

hmm

´´´java


@RunWith(SpringRunner.class)
@WebMvcTest(value=CustomerController.class, secure = false)
public class CustomerControllerTest {


    @Autowired
    private MockMvc mockMvc;


 @Test
    public void customerTest() throws Exception {

        RequestBuilder requestBuilder = MockMvcRequestBuilders.get(
                "/customer").accept(MediaType.APPLICATION_JSON);

        MvcResult result = mockMvc.perform(requestBuilder).andReturn();

        System.out.println(result.getResponse().getContentAsString());
        String expected = "Customer";

        Assert.assertEquals(expected,result.getResponse().getContentAsString());

    }
}
´´´

+++
##GET Request with Path Variables


+++
##Moking a Service

+++
##Moking a Rest API


---
##Test Driven Development(DDD)

