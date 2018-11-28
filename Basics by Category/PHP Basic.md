##PHP 1.What is PHP?
* PHP == ‘PHP: Hypertext Preprocessor’ (recursive backronym)
* Open-source, server-side scripting language
* Used to generate dynamic web-pages（today generate data）
* PHP scripts reside between reserved PHP tags
  This allows the programmer to embed PHP scripts within HTML pages

## Comment：java注释和#

## Variable

### Scope: Static, Global and locally-scoped variables
* Global variables can be used anywhere (declared outside a function)
* Local variables restricted to a function or class
* Variable declared “static” do not disappear when a function is completed
* Superglobals: predefined variables available in all ‘scopes（predefined global）

  _全局变量可以被脚本中的任何部分访问，但要在一个函数中访问一个全局变量，需要使用 global 关键字。_
### define rule:
* PHP variables must begin with a “$” sign
* The variable name must be followed by a letter or underscore
* Case-sensitive ($Foo != $foo != $fOo)
* Variables take the type of the current value

_当一个函数完成时，它的所有变量通常都会被删除。然而，有时候您希望某个局部变量不要被删除。要做到这一点，请在您第一次声明变量时使用 static 关键字：_


### Superglobal examples:
* Form variables ($_POST, $_GET)
* Server variables ($_SERVER, $HTTP_SERVER_VARS removed)
* State variables ($_COOKIE, $_SESSION)
* Environment variables ($_ENV, $HTTP_ENV_VARS deprecated)

## Constant

常量是全局的
常量在定义后，默认是全局变量，可以在整个运行的脚本的任何地方使用
Constant names use all uppercase letters

define ( string $name , mixed $value [, bool $case_insensitive = false ] )
该函数有三个参数:

name：必选参数，常量名称，即标志符。
value：必选参数，常量的值。
case_insensitive ：可选参数，如果设置为 TRUE，该常量则大小写不敏感。默认是大小写敏感的




## PHP echo 和 print 语句


echo - 可以输出一个或多个字符串
print - 只允许输出一个字符串，返回值总为 1

## Data Type:
String（字符串）, Integer（整型）, Float（浮点型）, Boolean（布尔型）, Array（数组）, Object（对象）, NULL（空值），Resourece。

在 PHP 中，对象必须声明。

echo "5x5=$foo";	// Outputs 5x5=25echo ‘5x5=$foo‘;	// Outputs 5x5=$foo
<?php
$heading="\"Computer Science\"";
Print $heading;
?>
输出“computer science”




PHP NULL 值
NULL 值表示变量没有值。NULL 是数据类型为 NULL 的值

在 PHP 中创建数组
在 PHP 中，array() 函数用于创建数组：

array();
在 PHP 中，有三种类型的数组：

数值数组 - 带有数字 ID 键的数组
关联数组 - 带有指定的键的数组，每个键关联一个值
多维数组 - 包含一个或多个数组的数组

PHP 数值数组
这里有两种创建数值数组的方法：

自动分配 ID 键（ID 键总是从 0 开始）：
```PHP
$cars=array("Volvo","BMW","Toyota");
人工分配 ID 键：

$cars[0]="Volvo";
$cars[1]="BMW";
$cars[2]="Toyota";
```
下面的实例创建一个名为 $cars 的数值数组，并给数组分配三个元素,然后打印一段包含数组值的文本：

PHP - 数组排序函数
在本章中，我们将一一介绍下列 PHP 数组排序函数：

sort() - 对数组进行升序排列
rsort() - 对数组进行降序排列
asort() - 根据关联数组的值，对数组进行升序排列
ksort() - 根据关联数组的键，对数组进行升序排列
arsort() - 根据关联数组的值，对数组进行降序排列
krsort() - 根据关联数组的键，对数组进行降序排列


遍历关联数组
遍历并打印关联数组中的所有值，您可以使用 foreach 循环，如下所示

```php
<?php
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");

foreach($age as $key=>$value)
{
    echo "Key=" . $x . ", Value=" . $x_value;
    echo "<br>";
}
?>

// //foreach 循环
// foreach 循环用于遍历数组。
//
// 语法
// foreach ($array as $value)
// {
//     要执行代码;
// }
// 每进行一次循环，当前数组元素的值就会被赋值给 $value 变量（数组指针会逐一地移动），在进行下一次循环时，您将看到数组中的下一个值

HP 超级全局变量列表:

$GLOBALS
$_SERVER
$_REQUEST
$_POST
$_GET
$_FILES
$_ENV
$_COOKIE
$_SESSION

PHP $_REQUEST
PHP $_REQUEST 用于收集HTML表单提交的数据

PHP $_GET
PHP $_GET 同样被广泛应用于收集表单数据，在HTML form标签的指定该属性："method="get"。

$_GET 也可以收集URL中发送的数据

PHP $_POST
PHP $_POST 被广泛应用于收集表单数据，在HTML form标签的指定该属性："method="post"
Post method sends all contents of a form with basically hidden headers (not easily visible to users)
Get method sends all form input in the URL requested using name=value pairs separated by ampersands (&)
E.g., process.php?name=trevor&number=345


PHP中的$_ENV是一个包含服务器端环境变量的数组。它是PHP中一个超级全局变量，我们可以在PHP 程序的任何地方直接访问它。
$_ENV只是被动的接受服务器端的环境变量并把它们转换为数组元素，

PHP 魔术变量
_LINE_ , _METHOD_, _CLASS_, _DIR_


Functions MUST be defined before they can be called
function names are not case sensitive




Include “footer.php” by placing within the HTML the line
<?php include 'footer.php';  ?>


## Cookies
setcookie() 函数向客户端发送一个 HTTP cookie。

cookie 是由服务器发送到浏览器的变量。cookie 通常是服务器嵌入到用户计算机中的小文本文件。每当同一台计算机通过浏览器请求页面时，就会发送这个 cookie。

cookie 的名称自动指定为相同名称的变量。例如，如果被发送的 cookie 名为 "user"，则会自动创建一个名为 $user 的变量，包含 cookie 的值。

## Session:
Whenever you want to create a website that allows you to store and display information about a user, determine which user-groups a person belongs to, or utilize permissions on your website, PHP Sessions are vital to each of these features.

PHP has a set of functions that can achieve the same results of Cookies without storing information on the user's computer. PHP Sessions store the information on the web server in a location that you chose in special files. These files are connected to the user's web browser via the server and a special ID called a "Session ID". This is virtually invisible to the user.

```PHP
<?php
        session_start();
        if(isset($_POST["submit"])) {
                $_SESSION["fname"] = $_POST["fname"];
                $_SESSION["lname"] = $_POST["lname"];
        }
        if(isset($_POST["logout"])) {
                session_destroy();
                unset($_SESSION);
        }
?>
<?php if(!(isset($_SESSION["fname"],$_SESSION["lname"]))): ?>
<h1>Login</h1>
<form method="POST">
<p><label for="username">First Name:</label>
        <input type="text" name="fname" />
</p> <p>
        <label for="lname">Last Name:</label>
        <input type="text" name="lname" />
</p> <p><input type="submit" name="submit" value="Submit"></p>
</form>
<?php   else:  ?>
<h1>Welcome, <?php echo ucwords($_SESSION["fname"] . " " . $_SESSION["lname"]);
?>
<form method="POST">
        <input type="submit" name="logout" value="logout">
</form>
<?php endif; ?>
```


## connect Database
```PHP
<html><body>
<?php
  // setup a query
  $link = mysql_connect($host, $user, $password);
  mysql_select_db($database);
  $query = “SELECT * FROM $table WHERE id = ‘$id’;”;
  $result = mysql_query($query);
  echo “<table>”;
  While ($row = mysql_fetch_array($result)) {
    echo “<tr>”;
      foreach ($row as $key => $value) {
         echo “<td>$value</td>”;
      }
      echo “</tr>”;
   }
  echo “</table>”;
  mysql_close($link);
  ?>
  </body></html>   
