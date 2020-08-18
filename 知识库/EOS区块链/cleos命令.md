# cleos命令



cleos wallet create --to-console 创建钱包

cleos wallet open 打开钱包
cleos wallet list 查看所有钱包列表

cleos wallet unlock 解锁钱包

cleos wallet create_key 创建一组密钥对，并导入到钱包，将公钥显示在界面上

cleos wallet private_keys 显示钱包里面存储的所有密钥对

cleos create account 创建账户（用某个密钥对的公钥创建账户）

```shell
创建了bob账户，它的两个钥匙孔owner和active都是公钥EOS8m...，也就意味着只有EOS8m...对应的私钥才能对这个账户进行操作。
cleos create account {创建者账户名} {新的账户名} 公钥1 公钥2

cleos create account eosio bob EOS8mkDUDottP33MaC1wNFfCPQVF2JCdR9usQWTCG53jL264Tmtpp
cleos create account eosio alice EOS8mkDUDottP33MaC1wNFfCPQVF2JCdR9usQWTCG53jL264Tmtpp
```

