In the <body>
<HTML>
<HEAD>
</HEAD>
<BODY>
<SCRIPT LANGUAGE="JavaScript">
//the Javascript here produces content for the BODY on loading
</SCRIPT>
</BODY>
</HTML>
or in the <head> as a deferred script
<HTML>
<HEAD>
<SCRIPT LANGUAGE="JavaScript">
//the Javascript here creates functions for later use


JavaScript  Event Handlers
Mouse Events
onclick		user clicks an HTML element
ondblclick	user double-clicks an element
onmouseover	user moves the mouse over an HTML element
onmouseout	user moves the mouse away from an HTML element
Keyboard Events
onkeydown	user presses a key
onkeyup		user releases a key
Object Events
onload		browser has finished loading the page
onunload	a page has unloaded
onresize	a document view is resized
onscroll	a document view is scrolled


Limitations of Client-Side JavaScript

[Was] Extremely difficult to explicitly draw graphics.
This has been dramatically improved in the latest versions
No access to the underlying file system or operating system
Unable to open and use arbitrary network connections
No support for multithreading
[Was] Not suitable for computationally intensive applications
This has been dramatically improved in the latest versions

伪多线程—call-back实现


JavaScript is case-sensitive
sum, SUM and Sum are 3 different identifiers
HTML is NOT case-sensitive
JavaScript ignores spaces, tabs, newlines
So it can be minified
Semicolon is optional


Literals
number, string, boolean


string.tolowerCase(); string.toupperCase()
string.indexOf(searchstring [, startindex])   //returns index value                          of char within string where searchString begins
string.charAt(index)       //returns the one char at position index
string.substring(indexA, indexB)    //returns characters of string
                                          between indexA and indexB
            Escape sequences are used to embed special characters in a string
                              	\b	backspace		\t	tab
                                	\f	form feed		\’	single quote
                        	\n	newline		\"	double quote
                        	\r	carriage return	\\	backslash


                          Variables should be declared, but not their type
                          		var i, sum;     //declaration
                          		var zero = 0;   //declaration and initialization
                          		var myName = "Ellis"
                           The type of value a variable can hold during execution may change.
                           Scope
                           Any variable outside a function is a global variable and can be referenced by any statement in the document
                           Variables declared in a function are local to the function
                          if var is omitted, the variable becomes global
                          In a multi-frame or multi-window set up of the browser, scripts can access global variables from any other document currently loaded
如果变量在函数内没有声明（没有使用 var 关键字），该变量为全局变量
lamp	JavaScript 变量均为对象。当您声明一个变量时，就创建了一个新的对象。

Every array has a length property
The length property is the largest integer property name in the array plus one
var myArray = [];
myArray.length                    //0
myArray[100000] = true;
myArray.length                     //100001
Arrays are sparse, in the above example only one index is allocated


There are many ways to iterate over an array
for loop; for (i=0; i < len; i++) {. . . }
forin loop; for (x in person) { . . . }
while loop; while (condition) {. . . }
There are many built-in methods for working with arrays, here are just a few:
concat(), joins two or more arrays
indexOf(), search the array for an element and return its position
pop(), remove the last element
push() add a new element at the end
reverse(), reverses the order of elements


null
在 JavaScript 中 null 表示 "什么都没有"。

null是一个只有一个值的特殊类型。表示一个空对象引用。

Note	：用 typeof 检测 null 返回是object。
你可以设置为 null 来清空对象:

undefined
在 JavaScript 中, undefined 是一个没有设置值的变量。

typeof 一个没有值的变量会返回 undefined。

实例
var person;      // 值为 undefined(空), 类型是undefined


Arrays and Objects are Semantically Identical

JavaScript does NOT support associative arrays,

There is nothing special about JavaScript arrays and the properties that cause this. JavaScript properties that begin with a digit cannot be referenced with dot notation; and must be accessed using bracket notation

JavaScript方法不能overload
