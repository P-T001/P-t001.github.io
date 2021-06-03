# Php api

---

测试时：

```
ini_set('display_errors', 'On'); //显示报错开启
ini_set('memory_limit','200M');  //内存空间设置200M
error_reporting(E_ALL);          //显示所有报错
```

定义变量为路径

```
define('ROOT_URL', dirname(dirname('http://' . $_SERVER['HTTP_HOST'] . $_SERVER['PHP_SELF']))); 
//定义ROOT_URL为http://主机名/php文件相对路径  如：http://xx.com/px/index.php
```

设置只能自己连

```
// key不对或者没有key参数则返回404错误页面
if (!isset($_REQUEST["key"]) || "00GV32RuPFNCdFRbapKaeTVy" !== $_REQUEST["key"]) {
header("status: 404 Not Found");
exit('');
}
```

数据库连接

```
//读取数据库文件进行连接
$webroot = $_SERVER['DOCUMENT_ROOT']; //获取当前文件路径
$db = require $webroot . '/../app/database.php'; //读取数据库文件
$conn = @new mysqli($db['hostname'], $db['username'], $db['password'], $db['database'], $db['hostport']);  //连接数据库

//判断是否连接成功，不成功退出
if (!$conn) {
            die("{\"status\":\"failed\",\"count\":0}");
        }
$conn->query("set names 'utf8';");  //设置数据库编码格式
$select_db = $conn->select_db($db['database']); //设置查询
//如果查询不存在则报错
if (!$select_db) {
            die("could not connect to the db:\n");
        }
//设置当前时间为添加，如果有参数则用参数的时间
$addDate = date('Y-m-d') . ' 00:00:00';
if (isset($_REQUEST["addDate"])) {
    $addDate = str_replace("/", "-", $_REQUEST["addDate"]);
}
//输入参数sql，去请求查询
if (isset($_REQUEST["sql"])) {
    $sql = base64_decode($_REQUEST["sql"]);
}
$ID = array();
if ($result = $conn->query($sql, MYSQLI_USE_RESULT)) {
    while ($row = $result->fetch_assoc()) {
          try {
               array_push($ID, $row);
          } catch (Exception $e) {
          }
    }
    $response['status'] = "success";
} else {
    $response['status'] = "failed";
}
$response['website'] = $_SERVER['SERVER_NAME']; //定义主机名（域名或IP）为响应中website
$response['data'] = $ID;
$response['count'] = sizeof($ID);
```

