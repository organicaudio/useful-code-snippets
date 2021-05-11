# Spring Boot test

For overview of Mockito see the [mockito memory aid](../mockito-memoery-aid.md) on this page.

## @MockBean & @Autowired

@MockBean allows to addd a mocked bean to the spring application context. So when you use @Autowired on another class it will load the mocked bean if it was referenced. It is a convenient way to work with mocks, because **you do not need to mock every field of the (autowired) class under test.** Just the ones you need to behave differently.

## MockRestServiceServer

The MockRestServiceServer allows to intercepts the calls to a RestTemplate. It is handy to mock calls to external APIs.


## @InjectMock & @Mock 

You may want to **avoid using @InjectMock**, because it fails silently without an exception, which is kind of annoying. Alternatively use @MockBean when using spring or just call the constructor of the class under test and mock every parameter of it with @Mock. Remember that a class which is instantiated by a constructor call is not spring managed.
