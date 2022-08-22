---
title: SpringMVC.Service
author: appstew
date: 2022-08-19 11:33:00 +0800
categories: [codestates, section3]
tags: [codestates]
math: true
mermaid: true
image:
  path: /commons/devices-mockup.png
  width: 800
  height: 500
  alt: Responsive rendering of Chirpy theme on multiple devices.
---


## Prompts

> An example showing the `tip` type prompt.
{: .prompt-tip }

> An example showing the `info` type prompt.
{: .prompt-info }

> An example showing the `warning` type prompt.
{: .prompt-warning }

> An example showing the `danger` type prompt.
{: .prompt-danger }



## title [Spring MVC] API 계층

```mermaid
classDiagram
    Spring MVC <|-- API
    Spring MVC <|-- service
    Spring MVC <|-- Data
    %% Spring MVC : +int age
    %% Spring MVC : +String gender
    %% Spring MVC: +isMammal()
    %% Spring MVC: +mate()
    class API{
      1. Controller
      2. DTO
      -controller과제(~8.26)
      -DTO과제(~8.29)
    }
    class service{
      equals.business
      1.서비스(비즈니스)계층
      2.
      -서비스(비즈니스) 과제(~8.30)
    }
    class Data{
      1.
      2.
    }
click API href "https://google.com"
click c href ".#spring-아키텍처"
click D href "./#controller"
click e href "./"
```

## 개요 및 학습 사전 준비



## 서비스 계층에서의 DI

### 개요

### 기본. DI 를 통한 서비스 계층 <-> API 계층 연동

### 기본. 매퍼(Mapper) 를 이용한 DTO 클래스 <-> 엔터티(Entity) 클래스 매핑

### 실습. 서비스 계층과 API 계층의 연동 실습

