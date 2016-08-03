---
layout: post
title: "extjs类介绍"
date: "2016-08-03 10:27:00 +0800"
category: 前端
tags: extjs
---
# 核心概念(Core concepts)

#### 1.构造方法
constructor

```javascript
Ext.define(className, members, onClassCreated);
```

```javascript
Ext.define('My.sample.Person', {
    name: 'Unknown',

    constructor: function(name) {
        if (name) {
            this.name = name;
        }
    },

    eat: function(foodType) {
        alert(this.name + " is eating: " + foodType);
    }
});

var bob = Ext.create('My.sample.Person', 'Bob');

bob.eat("Salad"); // alert("Bob is eating: Salad");
```

#### 2.初始化方法
config

```javascript
Ext.define('My.own.Window', {
   extend: 'Ext.Component',
   /** @readonly */
   isWindow: true,

   config: {
       title: 'Title Here',

       bottomBar: {
           height: 50,
           resizable: false
       }
   },

   applyTitle: function(title) {
       if (!Ext.isString(title) || title.length === 0) {
           alert('Error: Title must be a valid non-empty string');
       }
       else {
           return title;
       }
   },

   applyBottomBar: function(bottomBar) {
       if (bottomBar) {
           if (!this.bottomBar) {
               return Ext.create('My.own.WindowBottomBar', bottomBar);
           }
           else {
               this.bottomBar.setConfig(bottomBar);
           }
       }
   }
});

/** A child component to complete the example. */
Ext.define('My.own.WindowBottomBar', {
   config: {
       height: undefined,
       resizable: true
   }
});
```

```javascript
var myWindow = Ext.create('My.own.Window', {
    title: 'Hello World',
    bottomBar: {
        height: 60
    }
});

alert(myWindow.getTitle()); // alerts "Hello World"

myWindow.setTitle('Something New');

alert(myWindow.getTitle()); // alerts "Something New"

myWindow.setTitle(null); // alerts "Error: Title must be a valid non-empty string"

myWindow.setBottomBar({ height: 100 });

alert(myWindow.getBottomBar().getHeight()); // alerts 100
```

#### 3.静态成员
静态成员使用```statics```来设置
