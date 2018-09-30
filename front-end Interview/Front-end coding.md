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
 console.log(output);
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
