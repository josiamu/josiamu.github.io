---
layout: post
title: "Bundler"
description: ""
categories: ruby
tags: [gem,bundler]
---

Bundler provides a consistent environment for Ruby projects

Bundler is an exit from dependency hell

---

#### Getting Started

~~~
gem install bundler
~~~

---

#### Gemfile in your project's root

~~~
source 'https://rubygems.org'
gem 'github-pages'
~~~

---

#### Install all of the required gems from your specified sources

~~~
bundle install
~~~

---

#### Run an executable
~~~
bundle exec rspec spec/models
~~~

---

Gemfile คือ ไฟล์ที่จะบอกว่าต้องการอะไร (เช่นเดียวกับ package.js ใน NodeJS)

Bundler คือ สิ่งที่ใช้ในการจัดการ Gem ใน Ruby (เช่นเดียวกับ bower ใน NodeJS)

Gem ใน Ruby เปรียบเสมือน Plugin (เช่นเดียวกับ npm ใน NodeJS)


---

>Referrence

  [swiftlet.co.th](https://swiftlet.co.th/gem_bundler/)
