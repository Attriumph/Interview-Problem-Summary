
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
