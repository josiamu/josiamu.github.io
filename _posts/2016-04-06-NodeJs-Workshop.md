---
layout: post
title: "NodeJs Workshop"
description: ""
categories: nodejs
tags: [javascript,nodejs]
---


#### [NodeJSEnterprise](/book/NodeJSEnterprise_Day1_V1_2.pdf)

#### [Home Work](https://github.com/josiamu/nodejs_workshop)

---

#### What is NODEJS ?

- Use Google JavaScript V8 Engine for Compile
- Develop Server and Client Side
- Event Driven / Non Blocking I/O

#### [Install NodeJS](www.nodejs.org)

- Check `node -v`

#### Workshop 2 Hello NodeJS

- workshop2.js

  ```
  var http = require('http');
  http.createServer(function (req, res) {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hello NodeJS');
  }).listen(1337, '127.0.0.1');
  console.log('Server running at http://127.0.0.1:1337/');
  ```

- `node workshop2.js`
- browser => [http://localhost:1337](http://localhost:1337)

#### Workshop 3

- aggregation.js

  ```
  exports.sum = function(){
    this._sum = 0;
    for (var i = 0; i < arguments.length; i++) {
          this._sum+=arguments[i];
      }
  }

  exports.avg = function(){
    this._sum = 0;
    for (var i = 0; i < arguments.length; i++) {
          this._sum+=arguments[i];
      }
    this._avg = this._sum / arguments.length;
  }
  ```

- workshop3.js

  ```
  var a = require('./aggregation');

  a.sum(1,2,4,5,6,7);
  console.log(a._sum);
  a.avg(4,2,5,6,7,9,18,11);
  console.log(a._avg);
  ```

- `node workshop3.js`

#### Workshop 4 (Asynchronous Callback)

- workshop4.js

  ```
  var fs = require('fs');
  function readTotalLines(filePath,callback){
    var fileBuffer =  fs.readFileSync(filePath);
    var to_string = fileBuffer.toString();
    var split_lines = to_string.split("\n");
    //console.log(split_lines.length-1);
    callback(split_lines.length);
  }

  readTotalLines('./resources/contacts.txt',function(totalLines1){
    readTotalLines('./resources/contacts2.txt',function(totalLines2){
      readTotalLines('./resources/contacts3.txt',function(totalLines3){
        console.log(totalLines1 + totalLines2 + totalLines3);
      });
    });
  })

  ```

#### PROMISE

![](/assets/images/blog/promises.png)
- Pending
- Fulfilled
- Rejected

#### Workshop 5

- workshop5.js

  ```
  var fs = require('fs');
  function readTotalLines(filePath){
    return new Promise( function(resolve, reject) {
      fs.exists(filePath,function(exists){
        if(exists){
          var fileBuffer =  fs.readFileSync(filePath);
          var to_string = fileBuffer.toString();
          var split_lines = to_string.split("\n");
          console.log(split_lines.length);
          resolve(split_lines.length);
        }
        else {
          reject("Not found " + filePath );
        }
      });
    });
  }

  Promise.all([readTotalLines('./resources/contacts.txt')
  ,readTotalLines('./resources/contacts2.txt')
  ,readTotalLines('./resources/contacts3.txt')
  ,readTotalLines('./resources/contacts4.txt')
  ]
  ).then(function(values){
    console.log(values);
  },function(errors){
    console.log(errors);
  })
  ```

- Promise - Pending
- Fulfilled - Resolve
- Rejected - Rejected


#### Workshop 6 (npm install)

- package.json

  ```
  {
    "name": "myservice",
    "description": "Rest Api for my Enterprise.",
    "author": "Apaichon Punopas <apaichon@gmail.com>",
    "dependencies": {
      "body-parser": ">= 1.14.2",
      "crypto-js": ">= 3.1.5",
      "express": ">= 4.13.3",
      "guid":"latest",
      "orientjs": ">= 2.1.0",
      "oauth2-server": "latest",
      "rootpath": ">= 0.1.2",
      "winston": ">= 2.1.1",
      "underscore": ">=1.8.3",
      "useragent":"latest"
    }
  }
  ```

- [uninstall all modules](http://stackoverflow.com/questions/9283472/command-to-remove-all-npm-modules-globally)
  ```
  npm uninstall `ls -1 node_modules | tr '/\n' ' '`
  ```

#### Workshop 7 Express startup

- myservice.js

  ```
  var express = require("express");

  var app = express();

  app.get('/', function (req, res) {
    console.log("Hello World!");
    res.send('Hello World');
  })

  app.listen(3000);
  console.log("My Service is listening to port 3000.");

  process.on('uncaughtException', function (err) {
    console.error((new Date).toISOString() + ' uncaughtException:', err.message);
  });  
  ```

#### Workshop 8 ติดตั้ง OrientDB

#### Workshop 9 Create Database Social Network

#### Workshop 10 http Post Method

- copy folder `dao` , `biz` and file `config.js`
- myservice_ws10.js

  ```
  var express = require("express");

  var app = express();
  var bodyParser = require('body-parser');
  app.use(bodyParser.json());
  require('rootpath')();
  app.post('/crm/contacts/add',function(req,res){
  	var contactBiz = require('biz/contactBiz');
  	contactBiz.add(req.body,function(result){
  		res.send(result);
  		delete contactBiz;
  	});
  });

  app.listen(3000);
  console.log("My Service is listening to port 3000.");

  process.on('uncaughtException', function (err) {
    console.error((new Date).toISOString() + ' uncaughtException:', err.message);
  });  
  ```

- test Postman (POST)
  - http://localhost:3000/crm/contacts/add
    ```
    {
        "firstName":"prasert",
        "nikname" : "josiamu"
    }  
    ```

#### Workshop 11 http Get Method

- myservice_ws11.js

  ```
  app.get('/crm/contacts/getAll',function(req,res){
  	var contactBiz = require('biz/contactBiz');
  	contactBiz.getAll(function(result){
  		res.send(result);
  		delete contactBiz;
  	});
  });  
  ```

- test Postman (GET)
  - http://localhost:3000/crm/contacts/update
  ```
  {"item" :
      {
          "firstName":"jeen"
      },
      "condition" : {"@rid":"#12:11"}
  }  
  ```


#### Workshop 12 http Put Method

- myservice_ws12.js

  ```
  app.put('/crm/contacts/update',function(req,res){
    var contactBiz = require('biz/contactBiz');
    contactBiz.update(req.body,function(result){
      res.send(result);
      delete contactBiz;
    });
  });  
  ```

- test Postman (PUT)

#### Workshop 13 http Delete Method

- myservice_ws13.js

  ```
  app.delete('/crm/contacts/delete',function(req,res){
  	var contactBiz = require('biz/contactBiz');
    console.log(req.body);
  	contactBiz.delete(req.body,function(result){
  		res.send(result);
  		delete contactBiz;
  	});
  });  
  ```

- test Postman (PUT)  
  - http://localhost:3000/crm/contacts/delete
  ```
  {
      "surname": "bumphen"
  }  
  ```

#### Workshop 14 Routing Centre

- myservice_ws14.js  
- add folder api/*

  ```
  function execGet(req,res,next){
    var params = req.params[0].split('/');
    console.log('params',params);
    //[0]- empty,[1]-module,[2]-object,[3]-function,[4-n] params..n
    if(params.length <4)
      res.send({code:530,status:"error",message:"Invalid parameters!"});
    else{
      var obj = require('api/'+params[1]+'/' +params[2]);
      obj = new obj(app);
      var func =obj[params[3]];
      var inputs =[];
      for(var i=4;i<params.length;i++){
        if(params[i])
          inputs.push(params[i]);
      }

      console.log('inputs:',inputs);
      func(inputs,function(result){
        res.send(result);
      });
    }
  }

    function execPost(req,res,next){
    var params = req.params[0].split('/');
    console.log(params);
    //[0]- empty,[1]-module,[2]-object,[3]-function,[4-n] params..n
    if(params.length <4)
      res.send({code:530,status:"error",message:"Invalid parameters!"});
    else{
      try{
        var obj = require('api/'+params[1]+'/' +params[2]);
        obj = new obj(app);
        var func =obj[params[3]];
        func(req.body,function(result){
          res.send(result);

        });
      }
      catch(err){
        res.send({code:500,status:"error",message:JSON.stringify(err) });
      }
    }
  }

  function executeApi(req,res,next){
      switch(req.method){
        case "GET":
          execGet(req,res,next);
        break;
        case "POST":
          execPost(req,res,next);
        break;
        case "PUT":
          execPost(req,res,next);
        break;
        case "DELETE":
          execPost(req,res,next);
        break;
      }
  }

  app.all('*',executeApi);  
  ```
  - test Postman (GET)
    - http://localhost:3000/crm/contacts/update
    ```
    {"item" :
        {
            "firstName":"jeen"
        },
        "condition" : {"@rid":"#12:11"}
    }  
    ```
