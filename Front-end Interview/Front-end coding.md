# js考察
## LinkedIn endorsments 数据整合
* map， array 的考察
* 常用方法： push, set, get, has, sort
* 数据结构


```javascript
var endorsements = [{skill: 'javascript', user: 'user1'}, {skill: 'css', user: 'user2'}, {skill: 'html', user: 'user3'}, {skill: 'javascript', user: 'user2'}, {skill: 'css', user: 'user3'}, {skill: 'javascript', user: 'user3'}];

//输出
var out = [{skill: 'javascript', users:['user1', 'user2', 'user3'], count: 3}, {skill: 'css', users:['user2', 'user3'], count: 2},  {skill: 'html', users: ['user3'], count: 1}];
//follow up: 输出需要按照count排序


var map = new Map();

endorsements.forEach(function(endorsement) {
    let cur_skill = endorsement.skill;
    let cur_user = endorsement.user;
    let arr = [];
    console.log(map);

    if (!map.has(cur_skill)) {
      arr = [cur_user];
    } else {
      arr = map.get(cur_skill);
      arr.push(cur_user);
      console.log(arr);
    }
    map.set(cur_skill, arr);    
});


let output = [];

map.forEach(function(value, key, map) {
    let obj = {};

    obj.skill = key;
    obj.users = value;
    obj.count = value.length;

    output.push(obj);  
});

console.log(output);



function compare(properity) {
   return function (obj1, obj2) {
   return obj1[properity] - obj2[properity];

   }
}

output.sort(compare('count'));

```


## get parameters from URL
* split()考察
* regular express考察

```javascript

// method 1

function getPara(url) {
  if (url === undefined || typeof(url) !== 'string') {
    return null;
  }

  let items = url.split('?')[1].split('&');
  let res = {};

  for(let i = 0; i < items.length; i++) {
    console.log(items[0]);

    if (!items[i].includes('#')) {
      let item = items[i].split('=');
      res[item[0]] = item[1];     
    } else {
      console.log(items[i]);
      let item = items[i].split('#')[0].split('=');
      res[item[0]] = item[1];
    }
  }

  return res;
}

console.log(getPara(url));

// method2 : regular express
let url = http://www.linkedin.com?q1=v1&q2=v2#xxx;
 function getQueryString(name) {
var reg = new RegExp('(^|&)' + name + '=([^&#]*)(&|$)', 'i');
var r = url.match(reg);
if (r != null) {
return unescape(r[2]);
}
return null;
}



```
## map函数和split方法

```JavaScript
function Tuple (str) {
   this.tuple = [];
   this.parse(str);
};

Tuple.prototype.parse = function(str) {
 var str2 = str.substring(1, str.length-1);
 var t = str2.split('),(');
 console.log(t);
 var tps = t.map(function(item) {
    return item.split(',').map(function(i) {return parseInt(i)})
 });
 console.log(tps);
 this.tuple = tps;
}

Tuple.prototype.multiply = function(n) {
if(n<=0 || n>this.tuple[0].length) {
  return null;
}
var output = 1;
for(var i=0; i<this.tuple.length; i++) {
  output *= this.tuple[i][n-1];
}
return output;
}

var t = new Tuple("(1,2,3),(4,5,6),(7,8,9)");
console.log(t.multiply(1));
console.log(t.tuple);

```
## Promise useage example
```JavaScript
function loadScript(src) {
  return new Promise(function(resolve, reject) {
    let script = document.createElement('script');
    script.src = src;

    script.onload = () => resolve(script);
    script.onerror = () => reject(new Error("Script load error: " + src));

    document.head.append(script);
  });
}

let promise = loadScript("https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js");

promise.then(
  script => alert(`${script.src} is loaded!`),
  error => alert(`Error: ${error.message}`)
);

promise.then(script => alert('One more handler to do something else!'));
```
# HTML/CSS/Javascript 实现UI小模块

```JavaScript

<DOCTYPE! html>
<html>
  <head>
    <title>
    写一个类似于点赞功能的ui，点赞之后旁边的数字+1，取消之后-1
    写html的时候问了怎么改进accessiblity和symentic？用了一些 header footer之类的标签，加了role属性。
    写了个js函数来处理button toggle，事件绑定在外层容器上用了事件代理来处理点击操作

    </title>
    <style>
      p {
        color: white;
      }

    </style>
  </head>

  <body>
    <div id="container">
      <p id="display">0</p>
      <button id="good" >Good</button>
      <button id="cancel">Cancel</button>
    </div>


    <script >
      let display = document.getElementById("display").innerHTML;
      let times = 0;


      document.getElementById("good").addEventListener("click", good);
      document.getElementById("cancel").addEventListener("click", cancel);


      function good() {
        console.log("good");
        if (times === 0) {
          times = 1;
          display = 1;
          document.getElementById("display").innerHTML = display;
        }


      }

      function cancel() {
        if (times === 1) {
          times = 0;
          display = 0;       
          document.getElementById("display").innerHTML = display;
        }
      }

    </script>

  </body>


</html>



// tooltip

.container {
      text-align: center;  
      position: relative;
      display: flex;
      justify-content: center;
     }

     .toolkit {
      visibility: hidden;
      position: absolute;
      left: 50%;
      top: 100%;
      transform: translate(-50%,10%);
      width: 45px;
      background-color: gray;
      border-radius: 5px;
     }

     .name {

       width: 200px;
       background-color: blue;
       border-radius: 5px;
     }
     .profile{
       padding-top: 5px;
       width: 80%;

     }

     p {
       line-height: 50%;
     }

     .container:hover .toolkit {
       visibility: visible;
     }

<div class="container">
  <div class="name">
    LinkedIn_Name
  </div>

  <div class="toolkit">
      <img class="profile" src="https://tinyurl.com/yddhds52" alt="avator">
      <p class="username">Name</p>
      <p class="title">title</p>
  </div>
</div>



// judge if parent-children relationship
function isParent(parent, ele) {
     console.log(ele.parentElement.nodeName);

     while (ele.parentElement.nodeName !== "BODY") {

       if (ele.parentElement === parent) {
         return true;
       }
       ele = ele.parentElement;
     }

     return false;
   }

   let img = document.getElementsByClassName("profile")[0];
   let container = document.getElementsByClassName("container")[0];

   console.log(isParent(container, img));

// judge results   
let Fun = function(a){
      this.a = a;

         this.print = function(){
           return this.a;
      };

         this.addOne  = function(){  
          return this.a = this.a + 1;

      };
    };


       Fun.prototype = { mutiply: function(k) {
        return this.a *= k;
      }
    };


    let obj = new Fun(2);

       console.log(obj.print());   // 2
       console.log(obj.addOne()); // a=3
       console.log(obj.print()) ;   // 3
       console.log("mutiply:"+obj.mutiply(3));// 9
       console.log(obj.print());   // 9       c
        console.log(obj); //9

// isPalindrome

function isPalindrome(str) {
  if (str === null) {
    return false;
  }

  let len = str.length;

  if (len < 2) {
    return true;
  }

  for (let i = 0; i < parseInt(len/2); i++) {

    if (str.charAt(i) !== str.charAt(len - 1 - i)) {
      return false;
    }
  }

  return true;
}

console.log("---isPalindrome:", isPalindrome("aba"));

let foo = str=>{ return str === str.split("").reverse().join("");;}
console.log("new method:", foo("ababa"));


```

## 网页布局
* 不用flexbox，使用box-sizing和float来布局
* clear float
* 导航栏的制作
```HTML
<!DOCTYPE html>
<html>
<head>
<style>
* {
    box-sizing: border-box;
}
.header, .footer {
    background-color: grey;
    color: white;
    padding: 15px;
}
.column {
    float: left;
    padding: 15px;
}
.clearfix::after {
    content: "";
    clear: both;
    display: table;
}
.menu {
    width: 25%;
}
.content {
    width: 75%;
}
.menu ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}
.menu li {
    padding: 8px;
    margin-bottom: 8px;
    background-color: #33b5e5;
    color: #ffffff;
}
.menu li:hover {
    background-color: #0099cc;
}
</style>
</head>
<body>

<div class="header">
  <h1>Chania</h1>
</div>

<div class="clearfix">
  <div class="column menu">
    <ul>
      <li>The Flight</li>
      <li>The City</li>
      <li>The Island</li>
      <li>The Food</li>
    </ul>
  </div>

  <div class="column content">
    <h1>The City</h1>
    <p>Chania is the capital of the Chania region on the island of Crete. The city can be divided in two parts, the old town and the modern city.</p>
    <p>You will learn more about web layout and responsive web pages in a later chapter.</p>
  </div>
</div>

<div class="footer">
  <p>Footer Text</p>
</div>

</body>
</html>
```
