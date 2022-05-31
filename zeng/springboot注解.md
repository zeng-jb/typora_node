# springboot注解





## springboot-- @Value

### 一、从配置文件获取值

1. 获取配置值，配置不存在时抛出异常

~~~java
@Value("${jdbc.name}")
private String name
~~~

2. 获取配置值，配置不存在时使用指定的默认值

~~~java
@Value("${jdbc.name:}") //：后，当不存在赋值为空串
private String name
~~~

~~~java
@Value("${jdbc.name:root}") //：root，不存在赋值为指定的（root），字符串无需加引号
private String name
~~~

~~~java
@Value("${jdbc.name:#{null}}")//不存在赋值为null，null需要用#{}包裹
private String name
~~~

### 二、通过SpEL表达式赋值

1. 赋值为指定数字

~~~java 
@Value("#{10}")  
private int number; 
~~~

2. 赋值为指定字符串；字符串需要加引号包裹

`@Value("#{'Spring Demo'}")` 
`private String title;`

3. 赋值为指定对象的属性的值

``@Value("#{jdbcConfig.url}")`
private String jdbcUrl;` 

4. 赋值为指定对象的属性的值，并指定为空时的默认值

`@Value("#{jdbcConfig.name ?: 'root'}")`
`private String name;`

### 三、其他用法

1. 指定字符串值

@Value("Static Message!")
private String msg;

2. 注入本地资源

@Value("classpath:comm/about.txt")
private Resource locSrc;

3. 注入远程资源

@Value("https://www.abc.com/about.txt")
private Resource retSrc;

4. 注入系统属性

@Value("#{systemProperties['os.name']}")
 private String sysOsName

### 四、附

1. SpEL为注解属性赋值

`@Document(indexName = "#{elasticConfig.indexName}", type = "_doc")`





## @ResponseBody

@ResponseBody的作用其实是将java对象转为json格式的数据。

@responseBody注解的作用是将controller的方法返回的对象通过适当的转换器转换为指定的格式之后，写入到response对象的body区，通常用来返回JSON数据或者是XML数据。
注意：在使用此注解之后不会再走视图处理器，而是直接将数据写入到输入流中，他的效果等同于通过response对象输出指定格式的数据。

@ResponseBody是作用在方法上的，@ResponseBody 表示该方法的返回结果直接写入 HTTP response body 中，一般在异步获取数据时使用【也就是AJAX】。
注意：在使用 @RequestMapping后，返回值通常解析为跳转路径，但是加上 @ResponseBody 后返回结果不会被解析为跳转路径，而是直接写入 HTTP response body 中。 比如异步获取 json 数据，加上 @ResponseBody 后，会直接返回 json 数据。@RequestBody 将 HTTP 请求正文插入方法中，使用适合的 HttpMessageConverter 将请求体写入某个对象。
@ResponseBody并不是以json返回。不加@ResponseBody，是将方法返回的值作为视图名称，并自动匹配视图去显示，而加上@ResponseBody就仅仅是将方法返回值当作内容直接返回到客户端，并且会自适应响应头的content-type，返回的字符串符合json，那么content-type就是application/json，如果是普通字符串，就是text/plain，但是加上注解属性produces=application/json，那么不管内容是什么格式，响应头的content-type就一直是application/json，不再去做自适应，至于内容是不是json都不重要了

## @RequestBody

@RequestBody 注解则是将 HTTP 请求正文插入方法中，使用适合的 HttpMessageConverter 将请求体写入某个对象。
