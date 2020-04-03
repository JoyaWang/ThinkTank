# CoreData

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

- ### CoreData 简介

  > 存储数据，也就是要把一个个 OC 对象，比如 Student 对象，存储到数据库中
  >
  > 那么需要在数据库中创建一个存储这个对象类型的表，在 FMDB 中，通过语句创建，而在 CoreData 中，通过视图界面创建 Entity，每个 Entity 对应一张表，Entity 的 attributes 对应对象的属性。
  >
  > 创建了一个 Entity，如 Teacher以后，默认创建了这样一个 OC 类，虽然看不见，但你可以直接使用 Teacher 这个类创建对象，也可以在 Entity 的 Codegen 里面更改，将 Entity 的属性以 Extension 的形式添加给你自己后面手动创建的 Teacher 类。
  >
  > CoreData 不能执行 SQL 语句，取而代之，操作的是对象，FMDB SQLite 可以直接 SQL 语句



Core Data iOS5之后才出现的一个框架

- 如果创建项目时选择 Use Core Data
  - add some code to AppDelegate
  - Create a .xcdatamodeld file 【Data Model】就像 数据库的 Storyboard
- Entities (which are like a class)
- Attributes (which is like a var)
- Relationships (a var that points to other Entities)



### 创建数据库和数据表

- 【创建数据库】

  > 在创建项目的时候选择使用 CoreData，就会在 App Delegate 中创建 Container，也就是数据库，也可以自己参照这个代码创建

- 【创建数据表】打开 .xcdatamodeld 文件

  - 增加 Entity

    > - 创建 Entity，也就是创建要在数据库中存储的 类，比如 Tweet
    >
    >   > 比如 Tweet、TweetUser
    >
    > - 为 Entity，添加 attributes，也就是为 类 添加 属性/字段
    >
    >   > 比如，为 Tweet Entity 添加如下属性
    >   >
    >   > - created Date类型
    >   > - identifier String 类型
    >   > - text String类型
    >
    > - 创建 relationShip
    >
    > - 在此 Entity 的 Codegen 的地方选择要自动生成和此 Entity 对应的 OC 类，比如 Tweet，或者生成那个类的 Extension
    >
    >   > 如果选择了自动生成对应的 Tweet 类，则无法再手动创建 Tweet 类并方便的添加方法，所以建议自动生成 Tweet 的 Extension，Tweet 类自己手动创建
    >   >
    >   > 不管这两个选择哪一个，最后在创建对象的时候 Tweet 对象就自动拥有了 entity 中设置的属性

### 数据操作

- 获取 NSPersistentContainer 和 viewContext

  ```swift
  let persistentContainer = (UIApplication.shared.delegate as! AppDelegate).persistentContainer
  let context:NSManagedObjectContext = persistentContainer.viewContext
  ```

- 数据库操作

  - 增

    ```swift
    // 最基本的存储一条数据到 Coredata 的方式
    
    // 1. 获取 viewContext
    let context = persistentContainer.viewContext
    // 2. 创建 Entity
    // 必须先创建 Tweet 类，继承自 NSManagedObject，可在 Entity 那里用 Codegen 生成
    // 通过实体描述，描述出实体对象【连接Coredata的 Tweet Entity 和 Swift 的 Tweet 类？】
    let tweet:Tweet = NSEntityDescription.insertNewObject(forEntityName: "Tweet", into: context)
    tweet.text = "我的第一条推文" // 设置对象属性
    // 3. 保存Entity到数据库【上面的更改只在内存中，除非保存起来】
    try? context.save()
    ```

    ```swift
    // **** 方便的存储一条数据到 Coredata 的方式
    
    
    // 1. 获取 viewContext
    let context = persistentContainer.viewContext
    // 2. 创建 Entity，并设置属性
    let tweet = Tweet(context: context)
    tweet.text = "我的第一条推文"
    tweet.date = Date()
    // 3. 保存 Entity 到数据库
    try? context.save()
    ```

    

  - 删

    ```swift
    // 1. 获取 viewContext
    let context = persistentContainer.viewContext
    // 2. 删除
    context.delete(tweet)
    ```

  - 改

  - 查

    ```swift
    // 1. 创建 request 【获取哪类对象】
    let request:NSFetchRequest<Tweet> = Tweet.fetchRequest()
    
    // 2.设置 request 的条件【可省略?】
      // 2.1 设置查询条件
      let searchString = "foo"
      let predicate = NSPredicate(format: "text contains[c] %@", searchString)
      // 2.2 设置结果排序方式
      let sortDescriptor = NSSortDescriptor(
          key:"screenName", ascending: true, // 根据 screenName，升序
          selector: #selector(NSString.localizedStandardCompare(_:)) // can skip this
      )
    // 2.3 将条件设置给 request
    request.predicate = predicate
    request.sortDescriptors = [sortDescriptor]
    
    // 3. 获取结果
    let thetweets = try? context.fetch(request)
    ```

    



