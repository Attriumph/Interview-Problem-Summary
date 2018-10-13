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

// Move to right smoothly
function moveToRight(ele, dis, time) {
   let d = dis/(1000*time) * 10;

   let cur = 0;
   let myInterval;

   myInterval = setInterval(function(){
      cur += d;
      if (cur <= dis) {
        ele.style.transform = "translate(" + cur +"px, 0)";
      } else {
         clearInterval(myInterval);
         console.log("stop");
      }

  }, 10);  
}


```
## F&B coding practice1
[Details from here](https://caomingkai.github.io/2018/10/07/Search-for-a-Symmetric-Node/)
-----------------------------------------------------

    A            B

   / \           / \
  O   O         O   O
     /|\          /|\
    x O O        y O O

* y = find(A, B, x);
* 有两个dom，A和B，要求返回B中所对应的(x在A中的值)，也就是说，找出x在A中的位置，然后返回在B中对应位置的值。
* 另外一个就是node.children是一个类似于array但又不是array(Nodelist)，如何变成array？
  - Array.prototype.slice.call(node.childNodes)
  - Array.from(arguments)
  - use bind to create a new function slice() function on array-like object, so we can reuse it
* Followup：如果只是找index的话，不需要生成新array，在node.children里面如何找到某个点的index？
  - forEach遍历
* “Array-like” means that arguments has a length property and properties indexed from zero, but it doesn't have Array's built-in methods like forEach and map.
* 代码如下：
 ```javascript

 // Method1:
 // if we do not know the dom api: parentNode, childNodes, we could traverse two trees at same time
  function getSymmetricNode(target, root1, root2){
    if( target === root1 ) return root2

    for( let i = 0; i < root1.childNodes.length; i++){
        let node1 = root1.childNodes[i]     
        let node2 = root2.childNodes[i]
        if( node1 === target ) return node2
		    getSymmetricNode(target, node1, node2 )
    }
    return null
}
  //method2
  // if we use dom API:
  function getSymmetricNode(target, root1, root2){
      let path = getIndexPath( target, root1 )
      return getNode( path, root2 )
  }

  // transform a nodelilst to a array
  function getChildNodesArray(node){
      return Array.prototype.slice.call(node.childNodes)
  }

  // find the path    
  function getIndexPath(target, root1){
      let path = []
      let curNode = target

      while( curNode !==root1 && curNode && curNode.parentNode ){
          let index = getChildNodesArray(curNode.parentNode).indexOf(curNode)
          path.push(index)
          curNode = curNode.parentNode
        }
      return path
    }

  // find the node
  function getNode(path, root){
      let node = root
      while( path.length > 0 ){
            node = getChildNodesArray(node)[path.pop()]
      }
      return node
   }
 ```
## F&B pratice 2
* debounce 应用
* 在callback中传入参数的两种方法：the idea is to let the callback function return a function, so the returning function can pass into the o   
  origin function
  - bind函数
  - closure: remember the Parameters
```javascript
function debounce(foo, delay) {
  let timeout;

  return ()=> {
    clearTimeout(timeout);
    timeout = setTimeout(function() {
     foo();
   }, delay*1000);
  }

}
function foo(x, y) {
  return () => {
      console.log("lai offer la!!"+x+y);
  }
}
// or
function foo(x, y) {
    console.log("haha","hah" + x + y)
    return foo.bind(null, x, y)

}
const foo1 = debounce(foo("ni", "hao"), 5);
foo1();
foo1();
foo1();
foo1();


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
