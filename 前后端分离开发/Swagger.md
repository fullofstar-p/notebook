# Swagger

## 介绍

使用Swagger你只需要按照它的规范去定义接口及接口相关的信息，再通过Swagger衍生出来的一系列项目和工具，就可以做到生成各种格式的接口文档，以及在线接口调试页面等等。官网：https://swagger.io/

knife4j是为Java MVC框架集成Swagger生成Api文档的增强解决方案。

```
<dependency>
    <groupld>com.github.xiaoymin</groupld>
    <artifactld>knife4j-spring-boot-starter</artifactld>
    <version>3.0.2</version>
</dependency>
```

## 使用方式

操作步骤:

1. 导入knife4j的maven坐标

2. 导入knife4j相关配置类(WebMvcConfig)

   ```
   @EnableSwagger2
   @EnableKnife4j
   
   @Bean
       public Docket createRestApi() {
           //文档类型
           return new Docket(DocumentationType.SWAGGER_2)
                   .apiInfo(apiInfo())
                   .select()
                   .apis(RequestHandlerSelectors.basePackage("com.itheima.reggie.controller"))
                   .paths(PathSelectors.any())
                   .build();
       }
   
   
       private ApiInfo apiInfo() {
           return new ApiInfoBuilder()
                   .title("瑞吉外卖")
                   .version("1.0")
                   .description("瑞吉外卖接口文档")
                   .build();
       }
   ```

3. 设置静态资源映射（WebMvcConfig类中的addResourceHandlers方法），否则接口文档页面无法访问

   ```
   registry.addResourceHandler("doc.html").addResourceLocations("classpath:/META-INF/resources/");
   registry.addResourceHandler("/webjars/**").addResourceLocations("classpath:/META-INF/resources/webjars/");
   ```

4. 在LoginCheckFilter中设置不需要处理的请求路径

   ```
   "/doc.html",
   "/webjars/**",
   "/swagger-resources",
   "/v2/api-docs"
   ```

## 常用注解

| 注解               | 说明                                                      |
| ------------------ | --------------------------------------------------------- |
| @Api               | 用在请求的类上，例如Controller，表示对类的说明            |
| @ApiModel          | 用在类上，通常是实体类，表示一个返回响应数据的信息        |
| @ApiModelProperty  | 用在属性上，描述响应类的属性                              |
| @ApiOperation      | 用在请求的方法上，说明方法的用途、作用                    |
| @ApilmplicitParams | 用在请求的方法上，表示一组参数说明                        |
| @ApilmplicitParam  | 用在＠ApilmplicitParams注解中，指定一个请求参数的各个方面 |



