# 创建账户的rpc使用的json

创建账户貌似只能系统管理员eosio来做，所以code这里传eosio,并且交易签名也用的是管理员eosio的私钥。

但是，创建的账户"joya"到时候谁可以进入，是由创建"joya"账户时的owner和active的公钥决定的，owner公钥对应的私钥进入"Joya"账户后拥有完全权限，而active则不具备。

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

