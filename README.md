### poppo
---
https://github.com/pippo-java/pippo

http://www.pippo.ro/

```java
// pippo-core/src/test/java/ro/pippo/core/DefaultUriMatcherTest.java

public class DefaultUriMatcherTest {
  private DefaultUriMatcher uriMatcher;
  
  @Rule
  public ExpectedException thrown = ExpectedException.none();
  
  @Before
  public void before() {
    uriMatcher = new DefaultUriMatcher();
  }
  
  @After
  public void after() {
    uriMatcher = null;
  }
  
  @Test
  public void testPathParams() {
    uriMatcher.addUriPattern("/contact/{id}");
    Map<String, String> params = uriMatcher.match("/contact/3", "/cpmtact/{id}");
    assertNotNull(params);
    assertEquals(params.size(), 1);
    assertEquals(params.get("id"), "3");
  }
  
  @Test
  public void testNoBinding() {
    thrown.expect(PippoRuntimeException.class);
    thrown.expectMessage("Nobinding for '/contact/{id}'. Create binding with 'addUriPattern'");
    uriMatcher.match("/contact/1", "/contact/{id}");
  }
  
  @Test
  public void testMatch() throws Exception {
    uriMatcher.addUriPattern("/login");
    Map<String, String> params = uriMatcher.match("/login", "/login");
    assertNotNull(params);
    assertTrue(params.isEmpty());
  }
  
  @Test
  public void testUriForWithRegex() throws Exception {
    UriMatcher.UriPatternBinding binding = uriMatcher.addUriPattern("/user/{email}/{id:.*}");
    
    Map<String, Object> parameters = new HashMap<>();
    parameters.put("email", "test@test.com");
    parameters.put("id", 5);
    String path = uriMatcher.uriFor(binding.getUriPattern(), parameters);
    
    assertThat(path, equalTo("/user/test@test.com/5"));
  }
  
  
  
  
}
```

```
```

```
```


