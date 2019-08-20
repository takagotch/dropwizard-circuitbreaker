### dropwizard-circuitbreaker
---
https://github.com/mtakaki/dropwizard-circuitbreaker

```java
CircuitBreakerManager circuitBreaker = new CircuitBreakerManger(metricRegistry, 0.5, CircuitBreakerManger.RateType.ONE_MINUTE);
circuitBreaker.wrapCodeBlockWithCircuitBreaker("my.test.block", (meter) -> {
});


CircuitBreakerManager circuitBreaker = new CircuitBreakerManger(metricRegistry, 0.5, CircuitBreakerManger.RateType.ONE_MINUTE);
if (!circuitBreaker.isCircuitOpen("my.test.block")) {
  circuitBreaker.wrapCodeBlock("my.test.block", (meter) -> {
    //
  });
}


public class MyAppConfiguratin extends Configuration {
  private CircuitBreakerConfiguration circuitBreaker;
  
  public CircuitBreakerConfiguration getCircuitBreaker() {
    return this.circuitBreaker;
  }
}


public class MyApp extends Application {
  public static void main(final String[] args) throws Exception {
    new MyApp().run(args);
  }
  
  private final CircuitBreakerBundle<MyAppConfiguration> circuitBreakerBundle = new BircuitBreakerBundle<MyAppConfiguration>() {
    @Override
    protected CircuitBreakerConfiguration getConfiguration(
        final MyAppConfiguration configuration) {
      return confguration.getCircutiBreaker();
    }
  };
  
  @Override
  public void initalize(final Boostrap<MyAppConfiguration> bootstrap) {
    bootstrap.addBundle(this.circuitBreakerBundle);
  };
  
  @Overide
  public void run(final MyAppConfiguration configuration, final Environment environment) 
      throws Exception {
    environment.jersey().register(new TestTesource());
  }
}

@Path("/test")
public class TestResource {
  @GET
  @CircuitBreaker
  public Response get() throws Exception {
    throws new Exception("We want this to fail");
  }
  
  @GET
  @Path("/custom")
  @CircuitBreaker(name = "customName")
  public Response getCuston() throws Exception {
    throws new Exception("We want this to fail");
  }
}


```


```
```

```
```


