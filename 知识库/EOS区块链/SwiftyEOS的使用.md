# SwiftyEOS的使用



### 创建钱包和导入私钥

每新创建一个账户，就会在keyStore文件夹里生成一个新的keystore文件, 所以当转账的时候，会从使用currentAccunt的私钥进行签名，而currentAccount会去keystore文件夹里拿出第一个文件，如果这个文件夹只有一个keystore的话就没问题，但是一旦有了其他的keystore文件，就可能签名失败

所以调用currentAccount时，

```
public class var currentAccount: SELocalAccount? {
        if __account == nil {
            __account = existingAccount()
        }
        return __account
    }

```



如果直接创建钱包的话，会直接创建一对密钥对存进去

如果先单独生成密钥对，那么在导入钱包的过程中会创建钱包



### 创建账户

创建账户貌似只能系统管理员eosio来做，所以code这里传eosio

code是执行交易的主账户，在创建账户时主账户是系统管理员eosio，

action应该是发给在eosio这个账户中的智能合约里方法名

 一般的转账交易的话应该是bob此类的账户

args里面是action(方法)newaccount的参数，不同的action方法，args不同

 【在SwiftyEOS pushTrasaction方法中，data里面就只需要args后面的东西就行了，不是下面的完整的创建账户的json，code和action是以参数的形式传进去的，不包括在data中，这个方法自己会最后封装成下面这样完整的json】



```

{
  "code": "eosio",
  "action": "newaccount",
  "args": {
    "creator": "eosio",
    "name": "joya",
    "owner": {
      "threshold": 1,
      "keys": [
        {
          "key": "EOS8mkDUDottP33MaC1wNFfCPQVF2JCdR9usQWTCG53jL264Tmtpp",
          "weight": 1
        }
      ],
      "accounts": [],
      "waits": []
    },
    "active": {
      "threshold": 1,
      "keys": [
        {
          "key": "EOS8mkDUDottP33MaC1wNFfCPQVF2JCdR9usQWTCG53jL264Tmtpp",
          "weight": 1
        }
      ],
      "accounts": [],
      "waits": []
    }
  }
}
```

