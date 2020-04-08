## KVC 构造函数

即`字典转模型`

KVC 字典转模型

> Key - Value - Coding
>
> 字典转模型，用字典给对象属性赋值
>
> setValueForKey
>
> setValuesForKeys(_keyedValues: dict)
>
> dictionaryWithValuesForKeys

KVC是利用OC的运行时

使用KVC创建构造函数注意点：

> - 用KVC字典转模型方式创建构造函数时，必须直接或间接继承自NSObject，否则没有setValueForKey等KVC方法
>
> - 想要用 KVC 赋值的属性，必须在前面**使用`@objc`显式标记**(Swift4.0以后)，否则无法成功【或在类名前用@objcMembers标记】
>
> - 定义模型属性时
>
>   - 如果是对象，通常都是可选的 ( Optional )
>     - 在需要的时候才创建，不需要就不创建，节省内存空间
>     - 避免写构造函数，可以简化代码
>
>   - 如果是基本数据类型，不能设置成可选的，而且要设置初始值，否则 KVC 会崩溃
>
>     > 如Int 是一个基本数据类型的结构体，OC 中没有相应的类，只有基本数据类型int，而基本数据类型没有可选一说，一旦设置成可选，KVC就找不到这个key了
>
> - 如果需要使用 KVC 设置数值，属性(或方法)不能是私有 private 的，否则KVC会崩溃【可以使用**@objc** **private**】
>
>   > 在OC中，可以在私有扩展中"藏"属性，但是在运行时依然可以获取到
>   >
>   > 而Swift中，一旦将属性设置为 private ，运行时无法获取到此key，所以 KVC 无法使用
>
> - 如果子类没有重写父类的 KVC 方法`init(dict:)` ，调用的时候，会直接调用父类的方法，setValues时，会给子类的属性一并赋值
>
> - 如果字典中的key比对象的属性多，调用setValueforUndefinedKey并且函数体中不写任何实现，来保证在设置undefinedKey时不崩溃。

```swift
// KVC的基本实现
// 因为KVC是OC的东西，所以类必须是NSObject的子类才能使用KVC
class Teacher:NSObject {
    @objc var name:String? // 可空、可选属性【因为在Swift中是结构体，对应OC是NSString对象】
    @objc var age:Int = 0 // Int 是一个基本数据类型的结构体，OC 中没有相应的类，只有基本数据类型int，而基本数据类型没有可选一说，一旦设置成可选，KVC就找不到这个key了
    
    init(dict:[String:Any]) {
        // 在调用self的KVC方法之前，必须保证本类和父类都已初始化
        //【先将父类初始化，本类因为只有一个可选属性，可初始化为空，所以相当于本类自动初始化了】
        super.init()
        setValuesForKeys(dict)
    }
  // 重写父类的方法
    override func setValue(_ value: Any?, forUndefinedKey key: String) {
        // 没有调用 super，将父类的代码完全覆盖，保证碰见undefined key的时候不会崩溃
    }
}
```

