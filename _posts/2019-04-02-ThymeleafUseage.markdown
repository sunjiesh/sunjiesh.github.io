---

layout: post 
title: "Thymeleaf使用" 
date: 2019-04-02 10:00:00 +0800
categories: Java
---

### Formatting date in Thymeleaf

```java
<td th:text="${#dates.format(sprint.releaseDate, 'dd-MMM-yyyy')}"></td>
```