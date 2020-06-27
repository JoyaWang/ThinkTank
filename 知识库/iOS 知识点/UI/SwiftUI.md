# SwiftUI

### UI搭建

当创建一个SwiftUI视图时，在它的 body 属性中描述它的内容、布局和行为。

然而，body 属性只返回一个单一的视图。

你可以在 stacks 中组合或者嵌套多个视图，它可以将视图水平、垂直或者从后到前组合在一起。



### 在SwiftUI中使用 UIKit 类视图

将 UIKit 创建的 view 嵌套到遵守 UIViewRepresentable协议的 SwiftUI view中。

> makeUIView(context:) 创建并返回一个UIKit View
>
> updateUIView(_:context:) 配置这个view，并且对变动做出响应

```swift
import SwiftUI
import MapKit

/// 地图视图
struct MapView: UIViewRepresentable {
    
    /// 数据模型
    var coordinate: CLLocationCoordinate2D

    // 创建并返回UIKit的view
    func makeUIView(context: Context) -> MKMapView {
        MKMapView(frame: .zero) // 创建并返回一个MKMapView空对象
    }
    // 配置 这个空对象，并且对变动做出响应
    func updateUIView(_ uiView: MKMapView, context: Context) {
        // 1. 创建 经纬度坐标
        let coordinate = CLLocationCoordinate2D(latitude: 34.011286, longitude: -116.166868)
        // 2. 创建 范围
        let span = MKCoordinateSpan(latitudeDelta: 2.0, longitudeDelta: 2.0)
        // 3. 创建 要显示的地图区域 (坐标+范围)
        let region = MKCoordinateRegion(center: coordinate, span: span)
        
        // 4. 给 地图设置显示区域
        uiView.setRegion(region, animated:true)
    }
    
}
```



### List 列表，表格 

> 相当于 UITableView

When you use SwiftUI’s `List` type, you can display a platform-specific list of views. The elements of the list can be static, like the child views of the stacks you’ve created so far, or dynamically generated. You can even mix static and dynamically generated views.

当你使用SwiftUI的 List 类型时，你可以显示一个因平台而异的视图列表。列表的元素可以是静态的，就像目前堆中你创建的那些子视图一样，也可以是动态生成的。你还可以混合静态视图和动态生成的视图。

### Make the List Dynamic

相比于一个个创建列表的元素，你可以直接将一个集合生成一个有多行视图的列表

你可以创建一个显示某个集合中元素的列表，通过传递你存有数据的集合和一个可以为此集合中每个元素创建相应视图的闭包

列表通过提供的闭包将集合中的每个元素转换成它的一个组成视图



Lists work with *identifiable* data. You can make your data identifiable in one of two ways: by passing along with your data a key path to a property that uniquely identifies each element, or by making your data type conform to the `Identifiable` protocol.

列表需要可唯一识别的数据。你可以通过以下两种方式使你的数据唯一话，在传递你的数据给List时，一起传递一个属性路径，这个属性可以准确唯一地识别每一个元素，或者使你的数据类型遵守Identifiable协议。

Identifiable 是List视图要求的，List的每个模型元素必须有其唯一的标识符 id

You can create a `List` of views from a collection of `Identifiable` elements. What approach do you use to adapt a collection of elements that don’t conform to the `Identifiable` protocol?

你可以从包含可被唯一标识的元素的集合，直接创建视图列表。如果元素不遵守Identifiable协议的情况下，在创建列表List时，通过与数据一起传递一个可唯一标识这个元素的属性路径作为第二个参数给 `List(_:id:)`



### 页面间跳转

Set Up Navigation Between List and Detail

NavigationView 和 NavigationLink

### 页面间传值

Pass Data into Child Views



### Ways to set the device for previewing your views

Change the simulator selected in the active scheme.

Specify one or more devices using the `previewDevice(_:)` method.

Connect your development device and click the Device Preview button.



### @State 状态

*State* is a value, or a set of values, that can change over time, and that affects a view’s behavior, content, or layout. You use a property with the `@State` attribute to add state to a view.

State 是会随时间变化的一个值，或者多个值，并且这种变化会影响一个视图的行为，内容或者布局。用@State修饰符标记一个属性，将它作为视图的一个State

### binding 绑定

To give the user control over the list’s filter, you need to add a control that can alter the value of `showFavoritesOnly`. You do this by passing a binding to a toggle control.

A *binding* acts as a reference to a mutable state. When a user taps the toggle from off to on, and off again, the control uses the binding to update the view’s state accordingly.

It’s a value and a way to change that value.

A binding controls the storage for a value, so you can pass data around to different views that need to read or write it.

Add a `Toggle` view as the first child of the `List` view, passing a binding to `showFavoritesOnly`.

You use the `$` prefix to access a binding to a state variable, or one of its properties.

如果要让用户可以对列表进行过滤，你需要添加一种可以改变`showFavoritesOnly`的控制，你可以通过 绑定 一个控制开关来实现。

当用户点击开关时，开关会通过绑定功能相应更新视图的状态。它是一个值，也是一种改变这个值的方式。

绑定控制着一个值的存储，所以你可以通过 绑定 向需要读写这个值的不同的视图传递数据。

添加一个开关与`showFavoritesOnly`绑定，来控制它的值变化

你可以使用`$`前缀获取状态变量的绑定，或者它的某个属性

```swift
// 1. 静态行 - 开关
                Toggle(isOn: self.$showFavoritesOnly) {
                    Text("Favorites only")
                }
```



### ForEach

> `ForEach` operates on collections the same way as the list, which means you can use it anywhere you can use a child view, such as in stacks, lists, groups, and more. When the elements of your data are simple value types — like the strings you’re using here — you can use `\.self` as key path to the identifier.
>
> ForEach 像列表一样可以用在集合上，这意味着你可以在任何有子视图的地方使用它，比如在stacks, lists, groups等。当你的数据元素是简单的值类型时，比如字符串，你可以使用 `\.self`作为标识符的路径。

```swift
struct LandmarkList_Previews: PreviewProvider {
    static var previews: some View {
        ForEach(["iPhone SE", "iPhone XS Max"], id: \.self) { deviceName in
            LandmarkList()
                .previewDevice(PreviewDevice(rawValue: deviceName))
                .previewDisplayName(deviceName)
        }
    }
}
```

To combine static and dynamic views in a list, or to combine two or more different groups of dynamic views, use the `ForEach` type instead of passing your collection of data to `List`.

要在list中混合静态和动态视图时，或者混合两个及以上的不同组的动态视图时，使用ForEach类型来实现，不需要将数据集合传递给List

```swift
// 地标列表 (静态行 + 动态行)
            List{                
                // 1. 静态行 - 开关
                Toggle(isOn: self.$showFavoritesOnly) {
                    Text("Favorites only")
                }
                
                // 2. 动态列表 (行的数据可动态设置)
                ForEach(landmarkData) { landmark in
                    // 只有在全部显示状态下，或者只显示收藏时，此地标属于被收藏时显示
                    if !self.showFavoritesOnly || landmark.isFavorite {
                        
                        // 这里相当于map函数，为地标数组中的每个元素创建了一个地标视图并返回
                        NavigationLink(destination: LandmarkDetail(landmark: landmark)) {
                            // 地标行视图 (外包一层导航链接，可跳到目的地视图)
                            LandmarkRow(landmark: landmark)
                        }
                    }
                }
            }
```



### observable object 可观察对象

To prepare for the user to control which particular landmarks are favorites, you’ll first store the landmark data in an *observable object.*

An observable object is a custom object for your data that can be bound to a view from storage in SwiftUI’s environment. SwiftUI watches for any changes to observable objects that could affect a view, and displays the correct version of the view after a change.

Declare a new model type that conforms to the `ObservableObject` protocol from the Combine framework.

SwiftUI subscribes to your observable object, and updates any views that need refreshing when the data changes.

An observable object needs to publish any changes to its data, so that its subscribers can pick up the change.

Add the `@Published` attribute to each property in the model.

为了可以使用户能对地标进行收藏，你需要先将地标的数据存储在一个可观察对象中。

可观察对象是一个你数据的自定义对象，在SwiftUI的环境中，可以从内存中绑定到一个视图上。SwiftUi监听可观察对象的任何可以影响一个视图的变动，并且在变动之后相应地更新视图。

声明一个新的模型类型，使其遵守Combine框架中的可观察对象协议

SwiftUI视图会订阅可观察数据对象，当可观察数据对象发生变化时，SwiftUI视图也会随之变化

可观察对象会把自己的数据中标记为@Published的所有变动发布给它的订阅者, 所以把发生变动后会影响SwiftUI视图的属性(数据)用@Published标记

```swift
import SwiftUI
import Combine



/// 可观察数据对象
/*
 SwiftUI视图会订阅可观察数据对象，当可观察数据对象发生变化时，SwiftUI视图也会随之变化
 */
final class UserData: ObservableObject {
    
    /*
     可观察对象会把自己的数据中标记为@Published的所有变动发布给它的订阅者, 所以把发生变动后会影响SwiftUI视图的属性(数据)用@Published标记
     */
    
    /// 是否只显示收藏地标标记 - 会影响视图变化的数据1
    @Published var showFavoritesOnly = false
    
    /// 地标数据数组 - 会影响视图变化的数据2
    @Published var landmarks = landmarkData
}

```



### @EnvironmentObject 环境对象

> 环境对象，某个对象本身的变化会导致视图和其子视图变化，也就是导致此视图整体环境变化，就叫做这个视图的环境对象
>
> 包含数据源以及一些会导致视图变化的变量
>
> 创建视图时，需要传递环境对象进去

```swift
/// 主视图 列表视图
struct LandmarkList: View {
    
    
    /// 可观察对象，此视图的数据模型，包含数据源以及一些会导致视图变化的变量
    @EnvironmentObject var userData: UserData
    
    
    var body: some View {
        
        // 可导航(跳转)视图
        NavigationView {
            
            // 地标列表 (静态行 + 动态行)
            List{
                // 1. 静态行 - 开关
                Toggle(isOn: $userData.showFavoritesOnly) {
                    Text("Favorites only")
                }
                
                // 2. 动态列表 (行的数据可动态设置)
                ForEach(landmarkData) { landmark in
                    // 只有在全部显示状态下，或者只显示收藏时，此地标属于被收藏时显示
                    if !self.userData.showFavoritesOnly || landmark.isFavorite {
                        
                        // 这里相当于map函数，为地标数组中的每个元素创建了一个地标视图并返回
                        NavigationLink(destination: LandmarkDetail(landmark: landmark)) {
                            // 地标行视图 (外包一层导航链接，可跳到目的地视图)
                            LandmarkRow(landmark: landmark)
                        }
                    }
                }
            }
            
            // 本页面的导航栏标题
            .navigationBarTitle(Text("Landmarks"))
        }
    }
}
```

Which of the following passes data downward in the view hierarchy?

在视图层次结构中，向下传递数据的是`environmentObject(_:)` 修饰符

You apply this modifier so that views further down in the view hierarchy can read data objects passed down through the environment.

使用`environmentObject(_:)` 修饰符，可以使视图层次结构中下面的视图读取在环境中传递下来的数据对象

```swift
// 创建视图时，需要传递环境对象进去
// 主视图入口
        let contentView = LandmarkList()
                            .environmentObject(UserData()) // 传递一个可观察数据对象进去，即就是这个视图的数据模型

        // Use a UIHostingController as window root view controller.
        if let windowScene = scene as? UIWindowScene {
            let window = UIWindow(windowScene: windowScene)
            window.rootViewController = UIHostingController(rootView: contentView)
            self.window = window
            window.makeKeyAndVisible()
        }
```



### Group 组

`Group` is a container for grouping view content. Xcode renders the group’s child views as separate previews in the canvas.

A view’s children inherit the view’s contextual settings, such as preview configurations.

Group是用来组合视图内容的容器。Xcode在画布中将组中的子视图渲染成单独的预览。视图的子视图集成它的一些环境设置，比如预览配置。

只能在画布中使用?