---

layout: post 
title: "Spring Cloud Feign开发流程" 
date: 2019-05-07 10:00:00 +0800
categories: Java
---

## Server端
### pom配置

### 定义接口与实现
```java
public interface CountryFeign {

    @GetMapping(value = "/api/studying/feign/getCountrys")
    ResponsePageBean<GetCountryResp> getCountryPage(@RequestParam("pageNo") int pageNo,@RequestParam("pageSize") int pageSize);

}

```

```java

@RestController
public class CountryFeignController implements CountryFeign {

    private static final Logger LOGGER = LoggerFactory.getLogger(CountryFeignController.class);

    @Autowired
    private CountryService countryService;

    @Override
    public ResponsePageBean<GetCountryResp> getCountryPage(@RequestParam("pageNo") int pageNo, @RequestParam("pageSize") int pageSize){
        //代码实现
    }
	
}

```

### 增加注解

```java

@EnableFeignClients
public class StudyingApplication {

    public static void main(String[] args){
        SpringApplication.run(StudyingApplication.class,args);
    }

}
```

## Client端

### 代码实现

```java

@FeignClient(name = "studying")
public interface CountryFeignService extends CountryFeign {

}

```

```java

@Controller
@RequestMapping("/country")
public class AdminCountryController extends BaseController {


    private static final Logger LOGGER = LoggerFactory.getLogger(AdminCountryController.class);


    @Autowired
    private CountryFeignService countryService;
}



```