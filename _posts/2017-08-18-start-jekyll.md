---
layout: post
title: "เริ่มเขียน blog (อีกครั้ง) กับ jekyll"
description: "The first 'write blog' "
categories: [blog]
tags: [ruby,jekyll]
redirect_from:
  - /2017/08/18/
---
หลังจากห่างหายไปนาน กลับมาเขียน start jekyll ไม่เป็นซะงั้น งั้น note ไว้หน่อย ([Jekyll Home](http://jekyllrb.com/))

~~~~~~~~~~~~
bundle exec jekyll serve
~~~~~~~~~~~~

---
ต่อมา Jekyll Bootstrap ที่ใช้มาตลอด ไม่พัฒนาต่อล่ะ เลยต้องหาเจ้าใหม่มาลองเล่น 

เจออันนี้ [simple-texture](http://jekyllthemes.org/themes/simple-texture/) -> clone ปุ๊บ -> start ปั๊บ -> error (สัด)

ปัญหาคือ ต้อง update version RubyGems
> [ssl-certificate-update](http://guides.rubygems.org/ssl-certificate-update/#installing-using-update-packages)

---
มาถึง Installation [simple-texture](http://jekyllthemes.org/themes/simple-texture/) 

ก็ตามนั้นเลย แต่ให้เลือก As a fork ประหยัดเวลาหน่อย

~~~~~~~~~~~~
git clone https://github.com/yizeng/jekyll-theme-simple-texture.git
~~~~~~~~~~~~

---
ถ้าอยากเปลี่ยน port ล่ะ 

~~~~~~~~~~~~
bundle exec jekyll serve --port 8888
~~~~~~~~~~~~

---

ถ้าอยากแก้ปุ๊บ เห็นจอเปลี่ยนปั๊บ ใช้ตัวนี้ [Jekyll::Livereload](https://github.com/RobertDeRose/jekyll-livereload)

แล้วใช้งัยหล่ะ จัดไป

~~~
bundle exec jekyll serve --livereload
~~~