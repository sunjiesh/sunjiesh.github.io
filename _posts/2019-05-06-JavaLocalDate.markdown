---

layout: post 
title: "Java8中 Date和LocalDate的相互转换" 
date: 2019-05-06 10:00:00 +0800
categories: Java
---

## Date转LocalDate
```java
Date date = new Date();
Instant instant = date.toInstant();
ZoneId zoneId = ZoneId.systemDefault();
LocalDate localDate = instant.atZone(zoneId).toLocalDate();
System.out.println("Date = " + date);
System.out.println("LocalDate = " + localDate);
```

## LocalDate转Date
```java
ZoneId zoneId = ZoneId.systemDefault();
LocalDate localDate = LocalDate.now();
ZonedDateTime zdt = localDate.atStartOfDay(zoneId);
Date date = Date.from(zdt.toInstant());
System.out.println("LocalDate = " + localDate);
System.out.println("Date = " + date);
```