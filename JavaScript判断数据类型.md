# 常见JS判断数据类型方法

## 判断js中的数据类型有一下几种方法：
  * typeof
  * instanceof
  * constructor
  * prototype
  * jquery.type()

 ## 假设我们有：
      var a = "string.";
      var b = 123;
      var c= [1,2,3];
      var d = new Date();
      var e = function(){
              alert(111);
              };
      var f = function(){
             this.name="22";
             };

## 1.最常见的判断方法：typeof
      六种数据返回类型：String， Number， boolean，Object， function， undefined

        alert(typeof a)   ------------> string
        alert(typeof b)   ------------> number
        alert(typeof c)   ------------> object
        alert(typeof d)   ------------> object
        alert(typeof e)   ------------> function
        alert(typeof f)   ------------> function

        其中typeof返回的类型都是字符串形式，需注意，例如：
        alert(typeof a == "string") -------------> true
        alert(typeof a == String) ---------------> false

## 2.判断已知对象类型的方法： instanceof

    alert(c instanceof Array) ---------------> true
    alert(d instanceof Date)
    alert(f instanceof Function) ------------> true
    alert(f instanceof function) ------------> false

    **注意：instanceof 后面一定要是对象类型，并且大小写不能错，该方法适合一些条件选择或分支。**

## 3.根据对象的constructor判断： constructor
    alert(c.constructor === Array) ----------> true
    alert(d.constructor === Date) -----------> true
    alert(e.constructor === Function) -------> true
    注意： constructor 在类继承时会出错
     eg：
      function A(){};
      function B(){};
      A.prototype = new B(); //A继承自B
      var aObj = new A();
      alert(aobj.constructor === B) -----------> true;
      alert(aobj.constructor === A) -----------> false;

## 4.通用但很繁琐的方法： prototype.toString.call
    alert(Object.prototype.toString.call(a) === ‘[object String]’) -------> true;
    alert(Object.prototype.toString.call(b) === ‘[object Number]’) -------> true;
    alert(Object.prototype.toString.call(c) === ‘[object Array]’) -------> true;
    alert(Object.prototype.toString.call(d) === ‘[object Date]’) -------> true;
    alert(Object.prototype.toString.call(e) === ‘[object Function]’) -------> true;
    alert(Object.prototype.toString.call(f) === ‘[object Function]’) -------> true;
    ** 大小写不能写错，比较麻烦，但胜在通用。

## 5.万金油：jquery.type()

    如果对象是undefined或null，则返回相应的“undefined”或“null”。
    jQuery.type( undefined ) === "undefined"
    jQuery.type() === "undefined"
    jQuery.type( window.notDefined ) === "undefined"
    jQuery.type( null ) === "null"
    如果对象有一个内部的[[Class]]和一个浏览器的内置对象的 [[Class]] 相同，我们返回相应的 [[Class]] 名字。 (有关此技术的更多细节。 )
    jQuery.type( true ) === "boolean"
    jQuery.type( 3 ) === "number"
    jQuery.type( "test" ) === "string"
    jQuery.type( function(){} ) === "function"
    jQuery.type( [] ) === "array"
    jQuery.type( new Date() ) === "date"
    jQuery.type( new Error() ) === "error" // as of jQuery 1.9
    jQuery.type( /test/ ) === "regexp"
    其他一切都将返回它的类型“object”。


 参考：https://www.cnblogs.com/dushao/p/5999563.html
