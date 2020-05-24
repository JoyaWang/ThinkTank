# Socket通信

## Socket 是什么?

A软件(自己的App)和B软件(Terminal)之间通信

A使用一个Socket监听本机的一个特定端口，B使用一个Socket通过IP地址找到A所在的主机，再通过端口号找到A的Socket(连接头)，因为A在通过自己的Socket监听此端口，然后开始AB之间的通信即数据传输。

通过IP地址和端口号找到对应的应用，搭一个桥梁，进行数据传输，相当于一个管道

一根管子连接两个油箱，Socket相当于油箱口连接头

> 在Internet上的主机一般运行了多个服务软件，同时提供几种服务。每种服务都打开一个Socket，并绑定到一个端口上，不同的端口对应于不同的服务。Socket正如其英文原义那样，像一个多孔插座。一台主机犹如布满各种插座的房间，每个插座有一个编号，有的插座提供220伏交流电， 有的提供110伏交流电，有的则提供有线电视节目。 客户软件将插头插到不同编号的插座，就可以得到不同的服务。

## Socket的通信过程

- 创建Socket
- 连接到服务器
- 发送数据给服务器
- 从服务器接收数据
- 关闭连接



HTTP 协议

HTTP协议要求，请求结束后要关闭连接，节省服务器资源

### 短连接

> http/1.0 :  接收到服务器响应以后，立即断开连接，下次再要从服务器请求数据时，再进行三次握手，建立连接。但节省服务器资源

### 长连接

> http/1.1 :  接收到服务器响应后，不断开连接，下次从服务器请求数据时，直接发送请求，不需要进行三次握手。一直消耗服务器资源。【当服务器响应结束后，连接会等待非常短的时间，如果这个时间内没有新的请求，就断开连接】
>
> 比如打开百度的网页，要显示网页，一次性会发送很多个请求，获取文字、图片及视频等，这些请求会在一次长连接中完成。



### 请求

A软件向B软件发送数据就是请求

A向B发送的数据是一大串，HTTP协议要求把这一大串按照协议规则分割为请求头和请求体

- 请求头

  > 在请求头中配置一些信息，如请求方法GET还是POST、服务器主机(Host)地址或者域名信息等。
  >
  > User-Agent: 可以配置请求什么设备的网页
  >
  > Connection: keep-alive 或者 close 可以配置长连接或者短连接

- 请求体

  > 可以在请求体传输数据

### 响应

B软件向回应A软件的请求就是响应

B向A发送的数据是一大串，HTTP协议要求把这一大串按照协议规则分割为响应头和响应体

- 响应头

  > 响应头中有B的地址、状态码等信息
  >
  > server: GitHub.com
  >
  > status: 304

- 响应体

  > 响应体中才是传输的数据，比如一个html网页的字符串格式编码的二进制data，json 字符串格式编码的二进制data，plist 、xml等格式编码的二进制数据。AFN默认会把响应体序列化为 JSON 字符串，可以通过更改响应体序列化器为其他格式来接收其他编码格式的响应体，比如，如果响应体是 htmlString格式的，则需要把响应体序列化器更改为AFHTTPResponseSerializer, 才可以正确的解析出响应体的信息。



## 使用 GCDAsyncSocket 第三方库进行网络通信

代码见 `Mac服务器`

> Socket是纯C语言的
>
> GCDAsyncSocket是对Socket的封装的OC语言的一个第三方库
>
> 服务器端有两个Socket，一个负责监听(宿管大妈)，一个负责通信

1. 2. 初始化一个Socket对象作为服务器A一端的Socket(连接头)，用它绑定一个端口号，然后监听此端口号

   ```
   /// 创建服务器连接头Socket
   lazy var server:GCDAsyncSocket = GCDAsyncSocket(delegate: self, delegateQueue: .main)
   server.accept(onPort: UInt16(portNumber.intValue)) // 绑定并监听一个端口号
   ```

   ```swift
    /// 绑定并监听一个端口号
          /// - Parameter sender: 监听按钮
          @IBAction func listeningPort(_ sender: Any) {
              // 使用 socket 绑定并监听端口
               do {
                   try server.accept(onPort: UInt16(portNumber.intValue))
               }
               catch {
                   print("监听端口\(portNumber.intValue)出错:\(error)")
               }
           
               // Socket连接之后就开始读取数据
               readData()
          }
       
       func readData() {
           timer = Timer.scheduledTimer(timeInterval: 1.0, target: self, selector: #selector(readingData), userInfo: nil, repeats: true)
           // 将定时器添加到当前运行循环中
           RunLoop.current.add(timer!, forMode: .common)
       }
       
       /// 从所有客户端Socket中读取数据
       @objc func readingData() {
           for newSocket in clientSocketsArray {
               newSocket.readData(withTimeout: -1, tag: 0) // 调用此方法才会调用 didRead data代理方法
           }
       }
   ```

3. 如果有新来的客户端，比如B的Socket访问我们正在监听的端口号，就会调用下面代理方法

   ```
   func socket(_ sock: GCDAsyncSocket, didAcceptNewSocket newSocket: GCDAsyncSocket)
   ```

   通过此代理方法获取到访问我们监听的端口号的B软件的Socket(连接头)并持有，以便后面进行通信，否则会被释放

   ```swift
   /// 当接收到新 socket 通信时
       /// - Parameters:
       ///   - sock: 当前 socket【服务器】
       ///   - newSocket: 新来的客户端 socket
       func socket(_ sock: GCDAsyncSocket, didAcceptNewSocket newSocket: GCDAsyncSocket) {
           print("newSocket: \(newSocket)")
           
           print("ip地址: \(newSocket.connectedHost ?? "")")
           print("端口号:\(newSocket.connectedPort)")
           print("连接时间: \(Date())")
           print("断开时间:\("")")
           
           // 保存正在访问的客户端的Socket
           clientSocketsArray.append(newSocket)
   
           // 当第一次连接时，读取一次数据
           newSocket.readData(withTimeout: -1, tag: 0)
       }
   ```

   

4. 服务器A接收客户端B消息

   调用客户端B的Socket的 `readData(withTimeout:-1, tag:0)` 就会读取客户端发来的数据，通过代理方法 `socket(_ sock: GCDAsyncSocket, didRead data: Data, withTag tag: Int)`来接收数据

   ```swift
    /// 通过代理接收数据【客户端Socket的readData被调用时会被调用】
       /// - Parameters:
       ///   - sock: 客户端的Socket
       ///   - data: 客户端发送过来的数据
       ///   - tag: <#tag description#>
       func socket(_ sock: GCDAsyncSocket, didRead data: Data, withTag tag: Int) {
           let message = String.init(data: data, encoding: .utf8)
           print("客户端发来的贺电: \(message ?? "")")
           sock.write(message?.data(using: .utf8), withTimeout: -1, tag: 0)
       }
   ```

   

5. 服务器A向客户端B发送消息

   当服务器的Socket创建连接之后，也就是绑定并监听端口之后，初始化一个定时器，一直调用保存下来的，连接上我们监听的端口的所有Socket的readData，然后在代理方法中接收数据。

   由A给B发送消息，则找到B的Socket，调用它的readData方法

