# Solidity
使用**REMIX**进行智能合约开发，使用**Solidity**作为开发语言；

## 共享协议信息
    智能合约程序编译后生成字节码并在以太坊节点上部署，为了提高智能合约的可信度，Remix建议源程序在首行添加共享协议信息。
详细的共享协议在[SPDX官网](https://spdx.dev/)可以看到；Remix官方推荐使用以下共享协议：

```javaScript
// SPDX-License-Identifier: GPL-3.0
```

## 变量
**基础数据类型** 
* 布尔类型
    > 挖个坑，后面补一个关于位运算的笔记内容
* 整数类型
    >根据类型的长度和表示范围可以分为  
    >uint8~uint256  
    >int8~int256
* 枚举类型
    >枚举类型同C语言一致，枚举类型被返回的结果为uint  
    >允许显式转换，不允许隐式转换

    <img style="display: block; margin: 0 auto;" src="Images/EnumError.png" alt="" />
* 地址类型  
    >大小为20个字节，160位；  
    >地址类型变量有一系列属性与函数  
    >balance send  transfer call
      
**进阶数据类型**
* string类型
* struct类型

**Data Location**
    


