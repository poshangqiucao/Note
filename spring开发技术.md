# Spring开发技术

* WebMvcConfigurer接口

* HandlerInterceptorAdapter抽象类
  * 使用HandlerInterceptorAdapter这个适配器来实现自己的拦截器
  * 应用场景
    * 日志记录，可以记录请求信息的日志，以便进行信息监控、信息统计等。权限检查：如登陆检测，进入处理器检测是否登陆，如果没有直接返回到登陆页面。性能监控：典型的是慢日志。
  * 在HandlerInterceptorAdapter中主要提供了以下的方法：
    * preHandle：在方法被调用前执行。在该方法中可以做类似校验的功能。如果返回true，则继续调用下一个拦截器。如果返回false，则中断执行，也就是说我们想调用的方法 不会被执行，但是你可以修改response为你想要的响应。
    * postHandle：在方法执行后调用。
    * afterCompletion：在整个请求处理完毕后进行回调，也就是说视图渲染完毕或者调用方已经拿到响应。
  
* ApplicationListener
  * ApplicationContext事件机制是观察者设计模式的实现，通过ApplicationEvent类和ApplicationListener接口，可以实现ApplicationContext事件处理。
  * 如果容器中有一个ApplicationListener Bean，每当ApplicationContext发布ApplicationEvent时，ApplicationListener Bean将自动被触发。这种事件机制都必须需要程序显示的触发。
  
* WebSecurityConfigurerAdapter
  * WebSecurityConfigurerAdapter 类是个适配器, 在配置的时候,需要我们自己写个配置类去继承他,然后编写自己所特殊需要的配置这段配置，我认为就是配置Security的认证策略, 每个模块配置使用and结尾。
    authorizeRequests()配置路径拦截，表明路径访问所对应的权限，角色，认证信息。
    formLogin()对应表单认证相关的配置
    logout()对应了注销相关的配置
    httpBasic()可以配置basic登录
  
* AbstractGatewayFilterFactory 抽象类
  * 局部过滤器
  
* GlobalFilter 接口

* HandlerFunction 接口

* WebExceptionHandler 接口

* AbstractRoutingDataSource抽象类

* 在WebFlux的函数式开发模式中，我们用HandlerFunction和RouterFunction来实现上边这两点。

  * HandlerFunction相当于Controller中的具体处理方法，输入为请求，输出为装在Mono中的响应：

    > Mono<T extends ServerResponse> handle(ServerRequest request); 

  * RouterFunction，顾名思义，路由，相当于@RequestMapping，用来判断什么样的url映射到那个具体的HandlerFunction，输入为请求，输出为装在Mono里边的

    > Handlerfunction：
    >     Mono<HandlerFunction<T>> route(ServerRequest request);

  * 我们看到，在WebFlux中，请求和响应不再是WebMVC中的ServletRequest和ServletResponse，而是ServerRequest和ServerResponse。后者是在响应式编程中使用的接口，它们提供了对非阻塞和回压特性的支持，以及Http消息体与响应式类型Mono和Flux的转换方法。
  
* WebSecurityConfigurerAdapter

* OncePerRequestFilter

  * 它能够确保在一次请求中只通过一次filter，而不需要重复的执行。

* 