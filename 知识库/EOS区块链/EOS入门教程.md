# EOS入门教程

## 目标

- How to quickly spin up a node 快速搭建一个节点
- Manage wallets and keys 管理钱包和秘钥
- Create Accounts 创建账户
- Write some contracts 编写一些合约
- Compilation and ABI 编译合约，创建合约的ABI
- Deploy contracts 部署合约



# 开发环境安装

## 安装 eosio

### 安装二进制文件

```shell
brew tap eosio/eosio
brew install eosio
```

### 创建合约文件夹

```shell
mkdir contracts
cd contracts
```

### 安装CDT

> EOSIO Contract Development Toolkit，用来编译合约，生成ABI，Application Binary Files (ABI)

> ABI
>
> 作用就是用 JSON 文件描述合约中定义的方法(函数)名 ，这样就可以用JSON格式文件调用合约中定义的方法了
>
> The Application Binary Interface (ABI) is a JSON-based description on how to convert user actions between their JSON and Binary representations. The ABI also describes how to convert the database state to/from JSON. Once you have described your contract via an ABI then developers and users will be able to interact with your contract seamlessly via JSON.

```shell
brew tap eosio/eosio.cdt
brew install eosio.cdt
```

```shell
brew remove eosio.cdt
```



## 创建开发钱包

1. 创建钱包 

   ```shell
   cleos wallet create --to-console
   
   钱包密码
   PW5JuurMyks6Y6X8N7EP3UPiZrnRRk8cSsuAqqKdKt42gtEmVvUV3
   ```

2. 打开钱包 cleos wallet open 

   ```shell
   cleos wallet open
   cleos wallet list
   ```

3. 解锁钱包 cleos wallet unlock

   ```text
   cleos wallet unlock
   cleos wallet list
   ```

4. 将密钥对导入钱包 

   ```text
   # 创建密钥对并导入到钱包
   cleos wallet create_key
   
   用cleos wallet create_key创建了一组(用来开发的)密钥对，公钥是EOS8mkDUDottP33MaC1wNFfCPQVF2JCdR9usQWTCG53jL264Tmtpp
   ```

5. 导入系统用户的秘钥

   > Every new EOSIO chain has a default "system" user called "eosio". This account is used to setup the chain by loading system contracts that dictate the governance and consensus of the EOSIO chain. Every new EOSIO chain comes with a development key, and this key is the same. Load this key to sign transactions on behalf of the system user (eosio)

   ```shell
   cleos wallet import
   ```

   You'll be prompted for a private key, enter the `eosio` development key provided below

   ```text
   5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
   ```

## 开启keosd和nodeos

1. 开启keosd 

   ```shell
   keosd &
   ```

2. 开启nodeos 

   > 配置节点信息
   >
   > ~/Library/Application\ Support/eosio/nodeos/config

   ```shell
   nodeos -e -p eosio \
   --plugin eosio::producer_plugin \
   --plugin eosio::producer_api_plugin \
   --plugin eosio::chain_api_plugin \
   --plugin eosio::http_plugin \
   --plugin eosio::history_plugin \
   --plugin eosio::history_api_plugin \
   --filter-on="*" \
   --access-control-allow-origin='*' \
   --contracts-console \
   --http-validate-host=false \
   --verbose-http-errors >> nodeos.log 2>&1 &
   ```

3. 检查Nodeos是否产生块

   ```shell
   tail -f nodeos.log
   ```

4. 检查钱包

   ```shell
   cleos wallet list
   ```

5. 检查RPC API 

   ```shell
   curl http://localhost:8888/v1/chain/get_info
   ```

## 创建账户

```
# 创建bob账户， 用钱包里存储的自己创建的密钥对中的公钥，作为bob的owner权限的钥匙孔，也作为active权限的钥匙孔，这样此公钥对应的私钥则可以打开这个账户进行操作。
cleos create account eosio bob EOS8mkDUDottP33MaC1wNFfCPQVF2JCdR9usQWTCG53jL264Tmtpp
cleos create account eosio alice EOS8mkDUDottP33MaC1wNFfCPQVF2JCdR9usQWTCG53jL264Tmtpp
```

查询账户信息

```
cleos get account alice
```



# 智能合约开发

## 合约开发

> 开发一个合约就是创建一个类，并在类里面创建相应的方法(函数)
>
> Token合约，也就是Token类(eosio.token)已经定义好了，发行不同的Token，也就是创建不同的Token合约对象。

### 创建合约文件

> 也就是创建一个C++文件，里面声明要创建的类名称和方法

```shell
cd /Users/joyawang/EOS_Dir/contracts
mkdir hello
cd hello
touch hello.cpp
```

### 合约代码

```c++
#include <eosio/eosio.hpp>

using namespace eosio;

class [[eosio::contract]] hello : public contract {
  public:
      using contract::contract;

      [[eosio::action]]
      void hi( name user ) {
         print( "Hello, ", user);
      }
};
```

### 编译合约

> 将C++类文件编译成eos可以执行的二进制文件?

```shell
eosio-cpp hello.cpp -o hello.wasm
```

### 部署合约

> 创建一个用来部署某个合约的eos账户，相当于分配了一块内存？

```shell
cleos create account eosio hello EOS8mkDUDottP33MaC1wNFfCPQVF2JCdR9usQWTCG53jL264Tmtpp -p eosio@active
```

> 将合约部署在这个eos账户下, 即在这块内存中，创建并存放一个此类的实例对象？

```shell
cleos set contract hello /Users/joyawang/EOS_Dir/contracts/hello -p hello@active
```

### 执行合约

> 调用这个账户的这个类的实例对象的方法？

```
cleos push action hello hi '["bob"]' -p bob@active
```

如果合约内容更新后，需要重新编译

```shell
eosio-cpp -abigen -o hello.wasm hello.cpp
```

然后，更新合约

```shell
cleos set contract hello /Users/joyawang/EOS_Dir/contracts/hello -p hello@active
```



## 通证(Token)的部署、发行和转账

### 获取通证合约源码

> 获取存放通证合约(类)的源码

```shell
cd /Users/joyawang/EOS_Dir/contracts

git clone https://github.com/EOSIO/eosio.contracts --branch v1.7.0 --single-branch

cd /Users/joyawang/EOS_Dir/contracts/eosio.contracts/contracts/eosio.token
```



### 创建要部署合约的账户

> 创建eosio.token账户，即一块内存来存放合约的实例对象？

```shell
cleos create account eosio eosio.token EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
```



### 编译通证合约

> 编译通证类

```shell
eosio-cpp -I include -o eosio.token.wasm src/eosio.token.cpp --abigen
```



### 部署通证(Token)合约

> 创建一个Token类，存到这个账户的内存中？

```shell
cleos set contract eosio.token /Users/joyawang/EOS_Dir/contracts/eosio.contracts/contracts/eosio.token --abi eosio.token.abi -p eosio.token@active
```



### 创建新通证(Token)

> 向那个账户(内存)存放的Token实例对象发送create消息，即调用create方法
>
> create方法需要两个参数 issuer、maximum_supply

```shell
cleos push action eosio.token create '{"issuer":"alice", "maximum_supply":"1000000000.0000 JLT"}' -p eosio.token@active
```



### 发布通证(Token)

> 向那个账户(内存)存放的Token实例对象发送issue消息，即调用issue方法
>
> issue方法需要三个参数 name、quantity、memo

```shell
cleos push action eosio.token issue '[ "alice", "100.0000 JLT", "memo" ]' -p alice@active

cleos push action eosio.token issue '["alice", "100.0000 JLT", "memo"]' -p alice@active -d -j
```



### 通证(Token)转账

> 向那个账户(内存)存放的Token实例对象发送transfer消息，即调用transfer方法
>
> transfer方法需要四个参数 from、to、quantity、memo

```
# 从alice向bob转账
cleos push action eosio.token transfer '[ "alice", "bob", "25.0000 JLT", "m" ]' -p alice@active
```



### 查询账户余额

```shell
cleos get currency balance eosio.token bob JLT
```



## 数据存储

### 创建新文件夹

```shell
cd /Users/joyawang/EOS_Dir/contracts
mkdir addressbook
cd addressbook
```

### 创建并打开新文件

```shell
touch addressbook.cpp
```
