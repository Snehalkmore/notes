## Junit

@Mock
@Mock annotation is used to create and inject mocked instances. We do not create real objects, rather ask mockito to create a mock for the class.



## @Spy
@Spy annotation is used to create a real object and spy on that real object. A spy helps to call all the normal methods of the object while still tracking every interaction, just as we would with a mock.


## @InjectMocks
@InjectMocks marks a field on which injection should be performed. Mockito will try to inject mocks only either by constructor injection, setter injection, or property injection – in this order.


## Difference between @Mock and @Spy
@Mock, mockito creates a bare-bones shell instance of the field type, entirely instrumented to track interactions with it. This is not a real object and does not maintain the state changes to it.

When using @Spy, mockito proxies a real instance of the class and tracks every interaction with it. It maintains the state changes to it.


## Difference between @Mock vs @InjectMock
@Mock annotation creates mocks 
@InjectMocks creates actual objects and injects mocked dependencies into it.
