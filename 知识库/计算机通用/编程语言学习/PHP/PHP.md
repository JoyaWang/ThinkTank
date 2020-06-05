# 服务器端php搭建

- ### 登录

  - login.php

    ```php
    <?php
    class itcastUsers {
      private $db;
    
      // 用户登录
      function userLogin() {
        if (isset($_GET['username']) && isset($_GET['password'])){
          // 获取GET请求参数
          $accessType = '[GET]';
          $userName = $_GET['username'];
          $userPassword = $_GET['password'];
        } else if (isset($_POST['username']) && isset($_POST['password'])){
          // 获取POST请求参数
          $accessType = '[POST]';
          $userName = $_POST['username'];
          $userPassword = $_POST['password'];
    
        } else {
          echo('非法请求!');
          return false;
        }
    
        if ($userName == 'zhangsan' && $userPassword == '123') {
            // 将查询结果绑定到数据字典
            $result = array(
                          'userId' => 1,
                          'userName' => $userName,
                          'userImage' => $accessType
                            );
            // 将数据字典使用JSON编码
            echo json_encode($result);
        } else {
            // 将查询结果绑定到数据字典
            $result = array(
                          'userId' => -1,
                          'userName' => $userName,
                          'userImage' => $accessType
                            );
            // 将数据字典使用JSON编码
            echo json_encode($result);
        }
        
        return true;
      }
    }
    
    header('Content-Type:application/json;charset=utf-8');
    $itcast = new itcastUsers;
    $itcast->userLogin();
    ?>
    ```

  - login.html

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>post请求</title>
    </head>
    <body>
    <h1>GET请求</h1>
    <form action="login.php" method="get">
        <input type="text" name="username"><br>
        <input type="password" name="password"><br>
        <input type="submit">
    </form>
    
    <h1>POST请求</h1>
    <form action="login.php" method="post">
        <input type="text" name="username"><br>
        <input type="password" name="password"><br>
        <input type="submit">
    </form>
    </body>
    </html>
    ```

    

- ### 上传文件

  - upload.php

    ```php
    <?php
    
    // 打印出上传的文件的信息
    print_r($_FILES);
    
    
    // 创建一个空数组(字典?)来存储最终要返回的响应
    $response = array();
    
    // 获取服务器的根目录，拼接存储上传的文件的路径
    $target_path  = $_SERVER['DOCUMENT_ROOT']."/upload/files/";//接收文件目录
    
    // 在上传的路径上拼接文件名
    $target_path = $target_path . basename( $_FILES['userfile']['name']);
    
    
    // 将文件从暂存目录移动到接收文件目录
    // $_FILES是个字典
    // $_FILES['userfile']是上传的文件的信息数组
    // $_FILES['userfile']['tmp_name']是文件信息数组中文件的暂存路径(包括文件临时名称)
    if(move_uploaded_file($_FILES['userfile']['tmp_name'], $target_path)) {
    	// 如果上传成功，往响应字典中存储成功信息
        $response ['success'] = "The file ".  basename( $_FILES['userfile']['name']). " has been uploaded";
    }  else{
    	// 如果上传失败，存储失败信息
        $response ['error'] = "There was an error uploading the file, please try again!". $_FILES['userfile']['error'];
    }
    
    // 返回响应json格式
    echo json_encode($response);
    ?>
    ```

  - upload.html

    ```php+HTML
    <!DOCTYPE html>
    <html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    	<title>文件上传测试</title>
    </head>
    <body>
    <h1>文件上传</h1>
    <hr />
    		<form action="upload.php" method="post" enctype="multipart/form-data">
    			请选择要上传的文件: <input name="userfile" type="file">
    			<input type="submit" value="上传">
    		</form>
    </body>
    </html>
    ```

    

