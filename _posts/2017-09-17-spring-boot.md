---
layout: post
title: "Spring boot"
description: "Spring boot"
categories: spring
tags:
redirect_from:
  - /2017/09/17/
---

* Kramdown table of contents
{:toc .toc}


# Spring boot

---

# Config

---

# Profile

---

# Controller - Service - Repository

---

# Database with iBatis

---

# Logging

---

# i18n

---

# Build and run

---

# Testing (edited)

---

# Old blog

[Spring Boot](http://projects.spring.io/spring-boot/) makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run". We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.

---

#### [@RestController vs. @Controller](https://dzone.com/articles/spring-framework-restcontroller-vs-controller)

#### [Intro to Spring Boot - Video](https://dzone.com/articles/springone-platform-2016-replay)

#### [จัดการ Spring boot application ด้วย Docker](http://www.somkiat.cc/docker-with-spring-boot/)

#### [dzone Why Spring Boot?](https://dzone.com/articles/why-springboot)

#### Download => [Spring Tool Suite™](http://spring.io/tools/sts)

#### Guides => [Spring Tool](http://spring.io/guides)

#### Training Course
  - [nextzy.me](http://nextzy.me/javaee-with-spring-framework/)
  - [linksinnovation](http://www.linksinnovation.com/user-training-spring-boot-application/)

---

#### Howto

  - Config POM.xml
    - `<start-class>`  คลาสที่จะให้รัน Initialize ขึ้นมา จาก Config
  - @SpringBootApplication => Class สำหรับ run
  - SpringApplication.run => main method
  - สร้าง @Controller ไว้เป็น Spring bean สำหรับการใช้งาน
  - Web Framework => Thymeleaf
    - html => `<html xmlns="http://www.w3.org/1999/xhtml" xmlns:th="http://www.thymeleaf.org">`
  - Database Embeded
    - POM.xml
    - JPA
  - Database Others
    - POM.xml
    - JPA
    - src/main/resources/application.properties
  - Security
    - POM.xml
    - สร้าง Class สำหรับใช้ @Configuration และ extends WebSecurityConfigurerAdapter
      - implements configure(HttpSecurity http) และ configGlobal(AuthenticationManagerBuilder auth)
  - Test (wait)
  - Banner (wait)

---  


#### [Yashima-Faq](http://yashima.blogspot.com/2015/06/spring-boot-1-spring-boot.html)
  - ก่อนหน้านี้มีทั้งแบบ XML/ Annotation และผสมกันได้ อาจจะงง แต่ Spring Boot จะจัดการ Config ให้หมด


#### [Spring Boot ตอนที่ 2 Hello World](http://yashima.blogspot.com/2015/06/spring-boot-2-hello-world.html)
  - Spring Boot ใช้ Servlet 3.0 เพราะฉะนั้นจะไม่มี web.xml


#### [Spring Boot ตอนที่ 4 Spring Boot กับ Thymeleaf](http://yashima.blogspot.com/2015/06/spring-boot-4-spring-boot-thymeleaf.html)
  - Web Framework

#### [Spring Boot ตอนที่ 5 Spring Boot กับ Database [แบบ Embeded]](http://yashima.blogspot.com/2015/06/spring-boot-5-spring-boot-database.html)
  - Spring Boot มี [Spring Data JPA](http://projects.spring.io/spring-data-jpa/) ในการติดต่อฐานข้อมูล เหมือน hibernate

#### [Spring Boot ตอนที่ 6 กับ Production Database](http://yashima.blogspot.com/2015/06/spring-boot-6-production-database.html)
  - Database อื่นๆ

#### [Spring Boot ตอนที่ 7 Security](http://yashima.blogspot.com/2015/06/spring-boot-7-security.html)
  - Spring Security เกี่ยวกับ Login และ สิทธิ์ (Config)

#### [Spring Boot ตอนที่ 8 Testing](http://yashima.blogspot.com/2015/06/spring-boot-7-testing.html)
  - Integration Testing


---
#### Reference

  - [spring.io/guides](http://spring.io/guides)