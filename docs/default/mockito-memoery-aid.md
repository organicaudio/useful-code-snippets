# Mockito memory aid

- rule of thumb: Do not mock types you don’t own
- might seem obvious but do not mock the class under test.
- [Overview of mockito annotations](https://www.baeldung.com/mockito-annotations)
- `import static org.mockito.Mockito.*;`
- `import static org.mockito.ArgumentMatchers.*;`

## activate mockito annotations support

- Junit5: add @ExtendWith(MockitoExtension.class) to class
- Junit4: add @RunWith(MockitoJUnitRunner.class) to class
- Programmatically: MockitoAnnotations.initMocks(this);

## mock object

- Inline
    - mock an object: List mockedList = mock(List.class);
    - static import: import static org.mockito.Mockito.*; 
- with annotation: 
    - add @Mock on a object to mock the object
    - use @InjectMocks to mock all fields of the annotated object. All fields of the mocked class needs to be present in the testing class and be annotated with @Mock or 
- define behaviour:
    - given - preconidtion
    - when() - action to call
    - thenReturn() - returned values
    - example: when(mockedList.get(1)).thenReturn("first");

## ArgumentMatchers

- You can use the ArgumentMatchers in the package org.mockito.ArgumentMatchers to pass arbitrary arguments to the mocked method. 
- Example: `when(mockedList.get(any())).thenReturn("first");`.
- When using matchers, all arguments have to be provided by matchers.
- If you want to give some real arguments you need to use wrappers like `eq`

## intercept object/ partially mock

The real methods of a spied object are invoked but the object can still be verified and stubbed, when needed.

- Inline
    - spy an object: List<String> spyList = Mockito.spy(new ArrayList<String>());
    - static import: import static org.mockito.Mockito.*;
- with annotation: 
    - add @Spy on a object to spy the object
- use doReturn/when to mock methods of a spied object

## check behaviour of object

Use verify() to check if certain conditions are met:

- was a mocked method called
- which parameters are passed to a mocked method
- how often is a mocked method called