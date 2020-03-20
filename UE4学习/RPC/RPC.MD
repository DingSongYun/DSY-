UE4中的网络同步
===============

# 同步基础

## 端(客户端， 服务器)的标识
* `Actor`的`Role` & `RemoteRole`
    * `ROLE_Authority` 服务器上`Actor`
    * `ROLE_SimulatedProxy` 客户端上的网络同步`Actor`
    * `ROLE_AutonomousProxy` 客户端上的自我操控型`Actor`, 主操控角色
### `RPC`基础
* `RPC`的3种情况
1. `Multicast` :  `RPC`在服务器调用，函数执行分发到客户端
2. `Server` : `RPC`在客户端调用，最终函数执行仅在服务器，必须在有`Net Owner`的Actor上才可使用
3. `Clinet` : `RPC`在服务器上调用，最终函数执行仅在其所有者客户端, 必须在有`Net Owner`的Actor上才可使用

* `Net Owner`
    `Player Controller`或者`Owner`是`Plyer Controller`的Actor




# 其他
* 判断当前是Server还是Client
    1. UNetDriver中`ServerConnection`如果是空的那么就是Client

# TODO:
1. 客户端World的创建和同步
2. 客户端Actor的创建和同步
3. 几种同步方式的差别