# FMDB SQLite

> 详见 JL微博、数据存储-FMDB

- ### SQLite 概念简介

  > - 表
  >
  >   一张表 table 用来存储一类对象，表的 column / 字段 / 属性 就是对象的属性
  >
  >   > Person 表就存储 Person 类的所有对象
  >   >
  >   > Teacher 表就存储所有 Teacher 类的对象
  >
  > - db
  >
  >   一个数据库 database，可存很多不同的表，即可以存储不同类的对象
  >
  >   > Person 表和 Teacher 表 都存在 froshims.db 数据库中

- ### FMDB 和 CoreData 异同

  > 存储数据，也就是要把一个个 OC 对象，比如 Student 对象，存储到数据库中
  >
  > 那么需要在数据库中创建一个存储这个对象类型的表，在 FMDB 中，通过语句创建，而在 CoreData 中，通过视图界面创建 Entity，每个 Entity 对应一张表，Entity 的 attributes 对应对象的属性。
  >
  > 创建了一个 Entity，如 Teacher以后，默认创建了这样一个 OC 类，虽然看不见，但你可以直接使用 Teacher 这个类创建对象，也可以在 Entity 的 Codegen 里面更改，将 Entity 的属性以 Extension 的形式添加给你自己后面手动创建的 Teacher 类。
  >
  > CoreData 不能执行 SQL 语句，取而代之，操作的是对象，FMDB SQLite 可以直接 SQL 语句

- ### 简介

  > - 什么是FMDB？
  >
  >   > 一个iOS中SQLite API的封装库
  >   >
  >   > 1.是对libsqlite3库的封装，使用起来简洁、高效，没有原来的一大堆晦涩难懂、影响开发效率的C语句，更加面向对象
  >   >
  >   > 2.非常的轻量化、灵活
  >   >
  >   > 3.对于多线程的并发操作进行了处理，是线程安全的（重要特性之一）
  >   >
  >   > 4.因为它是OC语言封装的，只能在ios开发的时候使用，所以在实现跨平台操作的时候存在局限性
  >
  > - [iOS FMDB数据库详解教程](https://www.jianshu.com/p/7ac1c6eb63ed)
  >
  > - [FMDB Github地址](https://github.com/ccgus/fmdb)
  >
  > - 大写只是为了区分代码命令和用户信息
  >
  > - iOS 中 `?` 代表预编译指令的占位符

- ### 安装和导入

  > - 安装
  >
  >   > cd到项目目录
  >   >
  >   > pod init
  >   >
  >   > vim Podfile并添加pod 'FMDB'
  >   >
  >   > pod install
  >
  > - 导入libsqlite3框架
  >
  > - import <FMDatabase>



------

## 使用方法

- ### 创建数据库

  > 创建 froshims.db 数据库
  >
  > 终端 sqlite3 froshims.db
  >
  > 数据库文件默认存储位置为当前用户的家目录

  ```objc
  // MARK: 创建数据库
  /// 创建数据库
  - (void) createDatabase {
      // 1. 获取数据库文件的路径
      _docPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
      NSLog(@"%@", _docPath);
      // 设置数据库名称
      NSString *filename = [_docPath stringByAppendingPathComponent:@"student.sqlite"];
      // 2. 创建数据库
      _db = [FMDatabase databaseWithPath:filename];
      if ([_db open]) {
          NSLog(@"打开数据库成功");
      } else {
          NSLog(@"打开数据库失败");
      }
  }
  ```

  

- ### 创建数据表

  > 创建一个名为 registrants，3 个 column (列)，分别为 id，name，dorm 的数据表
  >
  > 终端 CREATE TABLE 'registrants' ('id' integer, 'name' varchar(255), 'dorm' varchar(255));

  ```objc
  // MARK: 创建表
  /// 创建表
  - (void) createTable {
      BOOL result = [_db executeUpdate:@"CREATE TABLE IF NOT EXISTS t_student (id integer PRIMARY KEY AUTOINCREMENT, name text NOT NULL, age integer NOT NULL, sex text NOT NULL);"];
      if (result) {
        NSLog(@"创建表成功");
      } else {
        NSLog(@"创建表失败");
      }
  }
  ```

  

- ### 【增】新增数据

  > 向 registrants 表添加一条数据， id, name, dorm column 中的值分别填1, 'Brian', 'Pennypacker'
  >
  > 终端 INSERT INTO registrants (id, name, dorm) VALUES(1, 'Brian', 'Pennypacker');

  ```objc
  // MARK: - 增
  // 插入数据
  - (void) addStudent {
      
      // 插入数据
      NSString *name = [NSString stringWithFormat:@"王子涵%@", @(mark_student)];
      int age = mark_student;
      NSString *sex = @"男";
      mark_student ++;
      // 1. executaUpdate: ?为占位符 (后面参数必须是OC对象，; 代表语句结束)
      BOOL result = [_db executeUpdate:@"INSERT INTO t_student (name, age, sex) VALUES (?,?,?)", name, @(age), sex];
      //2.executeUpdateWithForamat：不确定的参数用%@，%d等来占位 （参数为原始数据类型，执行语句不区分大小写）
      //    BOOL result = [_db executeUpdateWithFormat:@"insert into t_student (name,age, sex) values (%@,%i,%@)",name,age,sex];
      //3.参数是数组的使用方式
      //    BOOL result = [_db executeUpdate:@"INSERT INTO t_student(name,age,sex) VALUES  (?,?,?);" withArgumentsInArray:@[name,@(age),sex]];
      
      if (result) {
          NSLog(@"插入成功");
      } else {
          NSLog(@"插入失败");
      }
  }
  ```

- ### 【删】删除数据

  > 删除 id 为 1 的那一行数据
  >
  > 终端 DELETE FROM registrants WHERE id = 1;

  ```objc
  // 删除数据
  - (void)deleteStudent {
      // 1. 占位符用? (后面参数必须是OC对象)，需要将int包装成OC对象)
      int idNum = 11;
  //    BOOL result = [_db executeUpdate:@"delete from t_student where id = ?", @(idNum)];
      // 占位符用%@，%d等
      BOOL result = [_db executeUpdateWithFormat:@"delete from t_student where name = %@", @"王子涵0"];
      if (result) {
          NSLog(@"删除成功");
      } else {
          NSLog(@"删除失败");
      }
  }
  // 删除表
  - (void) deleteTable {
      // 如果表格存在 则销毁
      BOOL result = [_db executeUpdate:@"drop table if exists t_student"];
      if (result) {
        NSLog(@"删除表成功");
      } else {
        NSLog(@"删除表失败");
      }
  }
  ```

- ### 【改】修改 / 更新 数据

  > 更新 registrants 表，将 id 为 1 的那一行的 dorm 改为 Canaday
  >
  > 终端 UPDATE registrants SET dorm = 'Canaday' WHERE id = 1;

  ```objc
  // MARK: - 改
  // 修改数据
  - (void) modifyStudent {
      // 修改学生名字
      NSString *newname = @"李浩宇";
      NSString *oldname = @"王子涵2";
      BOOL result = [_db executeUpdateWithFormat:@"update t_student set name = %@ where name = %@", newname, oldname];
      if (result) {
          NSLog(@"修改成功");
      } else {
          NSLog(@"修改失败");
      }
  }
  
  ```


- ### 【查】读取数据

  - 读取所有数据

    > 选择显示 registrants 这个表中的所有数据
    >
    > 终端 SELECT * FROM registrants;

  - 按条件读取数据

    - 选择显示 registrants 这个表中 dorm 是 China 的所有数据

      > SELECT * FROM registrants WHERE dorm = 'China';

    - 选择显示 registrants 这个表中 dorm 为 Africa 的所有数据的 name

      > SELECT name FROM registrants WHERE dorm = 'Africa';

    ```objc
    // MARK: - 查
    // 查询
    - (void) search {
        // 查询整个表
    //    FMResultSet *resultSet = [_db executeQuery:@"select * from t_student"];
        // 根据条件查询
        FMResultSet *resultSet = [_db executeQuery:@"select * from t_student where id < ?", @(4)];
        // 遍历结果集合，打印出每一个符合条件的结果
        while ([resultSet next]) {
            int idNum = [resultSet intForColumn:@"id"];
            NSString *name = [resultSet objectForColumn:@"name"];
            int age = [resultSet intForColumn:@"age"];
            NSString *sex = [resultSet objectForColumn:@"sex"];
            NSLog(@"学号:%@ 姓名:%@ 年龄:%@ 性别:%@", @(idNum), name, @(age), sex);
        }
    }
    ```
