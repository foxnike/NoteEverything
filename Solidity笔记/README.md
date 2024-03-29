# solidty笔记
在阅读本篇笔记前，笔者强烈推荐通过阅读[官方文档](https://docs.soliditylang.org/)进行Solidity学习，本篇笔记由于笔者水平可能存在错误，欢迎勘正；

Solidity的发展变化非常快，请在阅读时请参考最新的文档以获取Solidity的新特性；
## 变量
本小节内容：
数据类型、数据作用域等

[变量笔记](%E5%B0%8F%E8%8A%82/%E5%8F%98%E9%87%8F.md)

## 函数
其基本定义格式如下:

```Solidity
function requestList(uint256 arg1, uint256 arg2) public view Modifer returns (uint256, SimpleCar[] memory)
```

本小节内容：函数访问控制、pure与view、payable、特殊函数、函数重载

[函数笔记](%E5%B0%8F%E8%8A%82/%E5%87%BD%E6%95%B0.md)

## 修饰器
函数修饰器**Modifier**以声明的方式改变函数的行为：例如在函数执行前检查条件；

本小节内容：

修饰器参数问题、修饰器重写问题、修饰器代码执行顺序等；

[修饰器笔记](%E5%B0%8F%E8%8A%82/%E4%BF%AE%E9%A5%B0%E5%99%A8.md)

## 多合约协作
* 合约类型：
    * 接口合约
    * 抽象合约
    * 库合约
* 合约导入
* 合约继承

[多合约协作笔记](%E5%B0%8F%E8%8A%82/%E5%A4%9A%E5%90%88%E7%BA%A6%E5%8D%8F%E4%BD%9C.md)

## 事件系统
Solidity的事件系统是在EVM的日志系统之上的一个抽象，外部应用程序可通过Ethereum客户端订阅与监听事件；

本小节内容：

日志的声明、调用、存储方式、`indexd`关键字与用途等；

[事件系统笔记](%E5%B0%8F%E8%8A%82/%E4%BA%8B%E4%BB%B6%E7%B3%BB%E7%BB%9F.md)

## 异常处理

本小节内容：

Solidity的恢复机制、异常类型、引发异常的方式等；

[异常处理笔记](%E5%B0%8F%E8%8A%82/%E5%BC%82%E5%B8%B8%E5%A4%84%E7%90%86.md)
