# eos_luckpoint
基于EOS 1.0.10版本的EOS DAPP实战开发教程源码，包含前端的用户界面，和后端的智能合约代码。
开发者基于这套代码，可以开发出一个包含前后端的完整的DAPP结构出来。

源码说明：
-----------------------------------
实现了一个简单的用户界面，及简单的智能合约。
EOS tag: 1.0.10
Eosjs tag: 15.0.6


使用说明：
-----------------------------------

1、将git下来的www_luckpoint文件夹，放入eos目录下，与contracts、build、programs这些目录同级。
  将git下来的contracts目录下的luckpoint文件夹，放入contracts目录下。

2、控制台进入到www_luckpoint目录，安装依赖包：npm install --save

3、编译luckpoint合约，生成abi文件：
> cd ./contracts/luckpoint
>
> eosiocpp -o luckpoint.wast luckpoint.cpp
>
> eosiocpp -g luckpoint.abi luckpoint.cpp
>

4、启动eos节点：
> cd /你的eos所在父级目录/eos/build/programs/nodeos
>
> ./nodeos -e -p eosio --plugin eosio::wallet_api_plugin --plugin eosio::chain_api_plugin --plugin eosio::account_history_api_plugin --access-control-allow-origin='*'

5、另起一个控制台，用户初始化钱包、合约等：
  cd /你的eos所在父级目录/eos

  // 创建钱包、导入私钥、创建及部署合约
> cleos --wallet-url http://127.0.0.1:8888 wallet create -n luckpoint
>
> cleos --wallet-url http://127.0.0.1:8888 wallet unlock -n luckpoint
>
> cleos --wallet-url http://127.0.0.1:8888 wallet import 5JcziTgwUhQgKyvmvc4ygEPGonQPVrBYNTwezAg5UuJ7djyVDWQ 
>
> cleos --wallet-url http://127.0.0.1:8888 create account eosio luckpoint.co EOS6zzuh8wUHAmEftGNzHLRDCaxtVmTdBKWNCMDb9rF3DhQMB1XuQ EOS6zzuh8wUHAmEftGNzHLRDCaxtVmTdBKWNCMDb9rF3DhQMB1XuQ
>
> cleos --wallet-url http://127.0.0.1:8888 set contract luckpoint.co ./contracts/luckpoint -p luckpoint.co

  // 创建banker、player1、player2这三个账户
>
> cleos --wallet-url http://127.0.0.1:8888 create account eosio banker EOS6zzuh8wUHAmEftGNzHLRDCaxtVmTdBKWNCMDb9rF3DhQMB1XuQ EOS6zzuh8wUHAmEftGNzHLRDCaxtVmTdBKWNCMDb9rF3DhQMB1XuQ
>
> cleos --wallet-url http://127.0.0.1:8888 create account eosio player1 EOS6zzuh8wUHAmEftGNzHLRDCaxtVmTdBKWNCMDb9rF3DhQMB1XuQ EOS6zzuh8wUHAmEftGNzHLRDCaxtVmTdBKWNCMDb9rF3DhQMB1XuQ
>
> cleos --wallet-url http://127.0.0.1:8888 create account eosio player2 EOS6zzuh8wUHAmEftGNzHLRDCaxtVmTdBKWNCMDb9rF3DhQMB1XuQ EOS6zzuh8wUHAmEftGNzHLRDCaxtVmTdBKWNCMDb9rF3DhQMB1XuQ
>

6、再启动一个控制台，用于启动web服务：
> cd /你的eos所在父级目录/eos/www_luckpoint
>
> npm run start
>

7、用浏览器打开（建议用Chrome浏览器，便于调试）：http://localhost:8080/

8、开始游戏。


命令行执行合约接口及查询表数据：
-----------------------------------

// 创建一个新游戏
>
> cleos --wallet-url http://127.0.0.1:8888 push action luckpoint.co creategame '["banker"]' -p banker
>
>

// 玩家开牌命令（第一个参数为游戏id，需要与实际的游戏id对应）
>
> cleos --wallet-url http://127.0.0.1:8888 push action luckpoint.co opencard '[1,1]' -p player1
>
> cleos --wallet-url http://127.0.0.1:8888 push action luckpoint.co opencard '[1,2]' -p player2
>
>

// 查询表数据
>
> cleos --wallet-url http://127.0.0.1:8888 get table luckpoint.co luckpoint.co game
>
>

参考资料：
-----------------------------------

// eos安装文档
>
> https://github.com/EOSIO/eos/wiki/Local-Environment#getting-the-code
>

// eosjs官方教程
>
> https://github.com/EOSIO/eosjs
>

// eosjs api文档
>
> https://github.com/EOSIO/eosjs-api/blob/master/src/api/v1/chain.json
>

演示视频：
-----------------------------------
> http://v.youku.com/v_show/id_XMzYxMDU5OTk2NA==.html
>
