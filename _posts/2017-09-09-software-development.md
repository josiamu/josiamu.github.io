---
layout: post
title: "เครื่องมือ / เทคนิค ที่ใช้ในการพัฒนา"
description: "loss of technology"
categories: tools
tags: 
redirect_from:
  - /2017/09/09/
---

* Kramdown table of contents
{:toc .toc}

---

# Docker

Build, Ship, and Run Any App, Anywhere => สร้าง environment ที่เหมือนจริง

---

# IntelliJ IDE

focused on your productivity. Full Java EE

---

# JSON

##### JSON (JavaScript Object Notation), is a simple and easy to read and write data exchange format. It’s popular and implemented in countless projects worldwide

  - Jackson
      - A High-performance JSON processor.
  - Google Gson
    - It was originally created for use inside Google, now it is used public projects.
  - JSON.simple
    - Simple Java library for JSON, to read and write JSON data


[Jsonformatter](https://jsonformatter.curiousconcept.com/) The JSON Formatter was created to help with debugging


---

# Slack

platform that connects teams with the apps, services, and resources they need to get work done. 

---

# Feedly

WEB update blog on world wide

---

# Sublime / Atom / VS Code

modern Text Editor

---

# Jenkins

Continuous Integration (CI)

---

# XML

Extensible Markup Language (XML) is a [markup language](https://en.wikipedia.org/wiki/Markup_language) that defines a set of rules for encoding documents in a format which is both human-readable and machine-readable.

In Java JDK, two built-in XML parsers are available (DOM and SAX)

  - DOM XML Parser (Document Object Model)
    - It parses an entire XML document and load it into memory.
  - SAX XML Parser (Simple API for XML)
    - SAX work differently with DOM parser, it does not load any XML document into memory
  - JDOM XML Parser
    - It’s an alternative to DOM and SAX
    - JDOM is not like SAX or DOM, which bundled in JDK., you need to download the manually
  - JAXB (Java Architecture for XML Binding)
    - JAXB, using annotation to convert Java object to / from XML file
    - JAXB is bundled in JDK 1.6.
  - XML & Properties
    - convert properties file into XML file or vice versse.

---

# POSTMAN

Postman Build test, and document your APIs faster.

support REST

    - GET or POST
    - Content-Type `application/json` or `application/xml`

support SOAP

    - POST
    - Content-Type `text/xml; charset=utf-8`

[Advance Postman](http://www.somkiat.cc/effective-postman/)

---

# Sass

**Sass** is the most mature, stable, and powerful professional grade CSS extension language in the world.

#### 1. Set Proxy (optional)
    >SET HTTP_PROXY=http://162.30.10.203:8080
    >SET HTTPS_PROXY=http://162.30.10.203:8080


#### 2. install sass
    >gem install sass


#### 3. go myProject
    >cd myProject

#### 4. create file test (style.scss)
~~~
$bgColor : #f9f9f9;
body {
  background-color: $bgColor;
}  
~~~

#### 5. run
    >sass `<input_file>:<output_file>`

    >sass style.scss:style.css

#### 6. อัพเดทไฟล์ .css ทุกครั้งที่บันทึกไฟล์ .scss
    >sass --watch style.scss:style.css  

#### 7. บีบอัด CSS หลัง compile
    >sass --watch style.scss:style.css --style compressed

---

# Bootstrap


Bootstrap is the most popular HTML, CSS, and JS framework for developing responsive, mobile first projects on the web.
- HTML5 doctype
- Mobile first
- Typography and links
- Normalize.css
- Containers

---

#### ติดตั้ง

- manual downaload (bootstrap,jquery) or
- bower install bootstrap
- npm install bootstrap

---

#### เรียกใช้
`<link rel="stylesheet" type="text/css" href="bower_components/bootstrap/dist/css/bootstrap.min.css">`
`<script type="text/javascript" src="bower_components/jquery/dist/jquery.min.js"></script>`
`<script type="text/javascript" src="bower_components/bootstrap/dist/js/bootstrap.min.js"></script>`

---

#### Container 2 แบบที่เคยใช้
~~~
<div class="container">
  ...
</div>

<div class="container-fluid">
  ...
</div>
~~~

- [่josiamu1](https://github.com/josiamu/TestJS/tree/master/WebContent/test/bootstrap)
- [josiamu2](https://github.com/josiamu/TestJS/tree/master/WebContent/test/republic_bootstrap)
- [codingpedia-bootstrap](http://www.codingpedia.org/udemy/bootstrap-tutorial-a-guide-for-beginners/)

---

# Log

---


# Base64

Base64 is a generic term for a number of similar encoding schemes that encode binary data by treating it numerically and translating it into a base 64 representation. The Base64 term originates from a specific MIME content transfer encoding.

Base64 encoding schemes are commonly used when there is a need to encode binary data that needs be stored and transferred over media that are designed to deal with textual data. This is to ensure that the data remains intact without modification during transport. Base64 is used commonly in a number of applications including email via MIME, and storing complex data in XML.


- [base64decode](https://www.base64decode.org/)
- [base64encode](https://www.base64encode.org/)


---

# Jmeter

โปรแกรม [Jmeter](http://jmeter.apache.org/) เป็นโปรแกรมสารพัดประโยชน์ใช้สำหรับทดสอบประสิทธิภาพการรองรับโหลดจำนวนมาก
Test ในส่วนที่เป็น Web Server

การใช้งาน => [แนะนำภาษาไทย](https://sysadmin.psu.ac.th/2014/05/23/monitor-server-apache-jmeter-windows/)



---


# Hyper-Productivity
  - youtube => [link](https://www.youtube.com/embed/HBSjj1LFDZY?list=PL3opfZU99soltwbe-9CV6DUeVTWd-TCiT)
  - คือ การเพิ่มความสามารถการทำงาน (เข้าใจสมองตัวเองทำงานอย่างไร)
  
  ![](/assets/images/blog/Challenge_vs_skill.svg.png)
  - [Mihaly Csikszentmihalyi](https://en.wikipedia.org/wiki/Mihaly_Csikszentmihalyi) คือคนที่ค้นคว้าเรื่อง ความสุข 
    - Apathy (เฉี่อยฉา)
    - Boredom (เบื่อ)
    - Relaxation (ผ่อนคลาย)
    - Worry (กังวล)            
    - Anxiety (ความวิตกกังวล)
    - Arousal (ความเร้าอารมณ์)
    - Flow (การไหล/จิตวิทยา)
    - Control / Overlearning (เรียนรู้)


#### เปรียบเทียบสมองซีกซ็าย และ ซีกขวา
  - We are elephant riders
  - ซีกขวา => อารมณ์ => ช้าง => ต้องการตอบสนองรวดเร็ว
  - ซีกซ้าย => เหตุผล => ควานช้าง
  - ถ้าควานช้างยอมแพ้ ทำให้เป้าหมายไม่ไปถึงไหน ล้มเลิกกลางทาง

#### 3 ปัจจัย ทำให้เกิดภาวะ Flow (ช้างและควานเช้า ไปในทางเดียวกัน)
  - Responsiveness (ต้องการตอบสนองรวดเร็ว)
  - Motivation (ต้องการกำลังใจ)
    - Sprint up มุ่งมั่น (เชื่อต้องสำเร็จ)
    - Sprint down (ไม่เชื่อมั่น หมดกำลังใจ)  
      - แก้ไขโดย Achievement (ความสำเร็จ โดยตั้งเป้า / ทำให้เสร็จ / ฉลอง)
  - Communication (การสือสารกับคนต่างระดับได้อย่างเหมาะสม)
    - ปรับเปลี่ยนวิธีการพูด เพื่อให้เข้าใจ
    - ไม่พูดเสียงดัง ด้วยประโยคเดิม


---

# Reference

---
