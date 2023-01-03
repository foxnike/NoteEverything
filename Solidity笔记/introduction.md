# solidty笔记
在阅读本篇笔记前，笔者强烈推荐通过阅读[官方文档](https://docs.soliditylang.org/)进行Solidity学习，本篇笔记由于笔者水平可能存在错误，欢迎勘正；
## 变量
solidty是一种**静态类型语言**：使用变量前需要声明其数据类型；

solidty支持的数据类型主要分为以下两类：

**值类型变量**：bool 整型 浮点型 address

**引用类型**：数组 string struct mapping

根据变量声明位置，变量可分为：

**状态变量**：声明在合约内部和合约方法外，作用域为其声明的合约内部

**局部变量**：声明在方法内部的变量，作用域为方法内部

**全局变量**：声明在方法外，作用域为全局变量空间

[变量笔记](%E5%B0%8F%E8%8A%82/%E5%8F%98%E9%87%8F.md)

## 函数
其基本定义格式如下:

```solidity
function requestList(uint256 arg1, uint256 arg2) public view returns (uint256, SimpleCar[] memory)
```

本小节内容：函数访问控制、pure与view、payable、特殊函数:

[函数笔记](%E5%B0%8F%E8%8A%82/%E5%87%BD%E6%95%B0.md)

## Library与继承
## 日志
## 异常处理