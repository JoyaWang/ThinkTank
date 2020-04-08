# YYModel

- ### JSON Object 和 Json Data

  - JSON Object

    > Dictionary 类型
    > Array 类型

  - JSON Data

    > Data 类型



- ### 其它 转到 模型

  - 字典 -> 模型

    > model.yy_modelSet(with:[:])

  - JSONObject -> 模型

    > model.yy_modelSet(withJSON:Any)

- ### 字典数组 转到 模型数组

  > NSArray.yy_modelArray(with: JLEmoticonPackage.self, json: array) as? [JLEmoticonPackage]

- ### 模型 转到 其它

  - 模型 -> 字典

    > model.yy_modelToJSONObject()

  - 模型 -> JSON data

    > model.yy_modelToJSONData()

- ### 用字典键值对给模型设置属性

  > ​	model.yy_modelSet(with:Dict)