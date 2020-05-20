---
title: 动态符号执行 | Microsoft IntelliTest 开发人员测试工具
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Dynamic symbolic execution
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: e5a3248d3f081bcab08c08110d305f0aa6235817
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79306991"
---
# <a name="input-generation-using-dynamic-symbolic-execution"></a>使用动态符号执行的输入生成

IntelliTest 通过分析程序中的分支条件为[参数化单元测试](test-generation.md#parameterized-unit-testing)生成输入。 测试输入的选择依据是它们是否可触发程序的新分支行为。 分析是一个增量过程。 这将优化正式测试输入参数 `I` 的谓词 `q: I -> {true, false}`。 `q` 表示 IntelliTest 已观察到的行为集。 最初，`q := false`，因为尚未观察到任何行为。

循环的步骤如下：

1. IntelliTest 确定输入 `i`，以使用[约束求解器](#constraint-solver)使 `q(i)=false`。 按构造，输入 `i` 将采用之前没有见过的执行路径。 最初，这意味着 `i` 可以是任何输入，因为尚未发现任何执行路径。

1. IntelliTest 使用所选输入 `i` 执行测试，并监视测试以及被测程序的执行情况。

1. 在执行期间，程序采用由该程序的所有条件分支决定的特定路径。 确定执行的所有条件集称为“路径条件”，在形式输入参数中写作谓词 `p: I -> {true, false}`。 IntelliTest 计算此谓词的表示形式。

1. IntelliTest 设置 `q := (q or p)`。 换言之，它会记录观察到由 `p` 表示的路径这一事实。

1. 转到步骤 1。

IntelliTest 的[约束求解器](#constraint-solver)可处理 .NET 程序中可能出现的所有类型的值：

* [整数](#integers-and-floats)和[浮点数](#integers-and-floats)
* [对象](#objects)
* [结构](#structs)
* [数组](#arrays-and-strings)和[字符串](#arrays-and-strings)

IntelliTest 筛出违反规定假设的输入。

除了即时输入（[参数化单元测试](test-generation.md#parameterized-unit-testing)的自变量），测试还可从 [PexChoose](static-helper-classes.md#pexchoose) 静态类进一步提取输入值。 作出的选择还将确定[参数化模拟](#parameterized-mocks)的行为。

## <a name="constraint-solver"></a>约束求解器

IntelliTest 使用约束求解器确定测试和受测程序的相关输入值。

IntelliTest 使用 [Z3](https://github.com/Z3Prover/z3/wiki) 约束求解器。

## <a name="dynamic-code-coverage"></a>动态代码覆盖率

运行时监视的一个副作用是 IntelliTest 会收集动态代码覆盖率数据。
这称为“动态”  ，因为 IntelliTest 只识别已执行的代码，所以它提供覆盖率的绝对值方式与其他覆盖率工具通常采用的方式不同。

例如，当 IntelliTest 报告动态覆盖率为 5/10 基本块时，意思是已覆盖 10 个块中的 5 个，其中到目前为止分析所访问的所有方法（而不是受测程序集中存在的所有方法）中的总块数为 10。
之后在分析中，随着发现更多的可访问方法，分子（本例中的 5）和分母 (10) 还可能增加。

## <a name="integers-and-floats"></a>整数和浮点数

IntelliTest 的[约束求解器](#constraint-solver)确定基元类型（如字节型  、整型  、浮点型  等）的测试输入值，以便为测试和受测程序触发不同的执行路径。

## <a name="objects"></a>对象

IntelliTest 可[创建现有 .NET 类的实例](#existing-classes)，也可使用 IntelliTest 自动[创建 mock 对象](#parameterized-mocks)，该对象根据使用率以不同的方式实现特定接口和行为。

<a name="existing-classes"></a>
## <a name="instantiate-existing-classes"></a>实例化现有类

**有什么问题？**

IntelliTest 运行测试和受测程序时，将监视执行的指令。 特别是，它会监视对字段的所有访问。 然后，它会使用[约束求解器](#constraint-solver)来确定新的测试输入（包括对象及其字段值），这样测试和受测程序便会采用其他感兴趣的行为方式。

这意味着 IntelliTest 必须创建某些类型的对象并设置其字段值。 如果类[可见](#visibility)并具有[可见](#visibility)默认构造函数，IntelliTest 可创建该类的实例。
如果类的所有字段都[可见](#visibility)，IntelliTest 可自动设置字段。

如果类型不可见或字段不[可见](#visibility)，则 IntelliTest 需要帮助才能创建对象，使对象处于感兴趣的状态以实现最大代码覆盖率。 IntelliTest 可使用反射以任意方式创建和初始化实例，但人们通常并不希望这样，因为这样可能会使对象在正常执行程序期间处于永不出现的状态。 IntelliTest 会转而依赖用户的提示。

## <a name="visibility"></a>可见性

.NET 具有一个精心设计的可见性模型：类型、方法、字段以及其他成员可为“私有”、“公共”、“内部”等    。

当 IntelliTest 生成测试时，它将尝试只在生成测试的上下文内执行对于 .NET 可见性规则合法的操作（例如调用构造函数、方法和设置字段）。

规则如下所示：

* **内部成员的可见性**
  * IntelliTest 假定生成的测试有权访问对封闭 [PexClass](attribute-glossary.md#pexclass) 可见的内部成员。
  .NET 具有 InternalsVisibleToAttribute  ，可将内部成员的可见性扩展到其他程序集。

* **[PexClass](attribute-glossary.md#pexclass) 的（在 C# 中保护的）私有和家庭成员的可见性**
  * IntelliTest 始终将生成的测试直接置于 [PexClass](attribute-glossary.md#pexclass) 或子类中。 因此，IntelliTest 假定它可使用（在 C# 中保护的  ）所有可见的家庭成员。
  * 如果将生成的测试直接置于 [PexClass](attribute-glossary.md#pexclass) 中（通常使用分部类执行），IntelliTest 假定它还可使用 [PexClass](attribute-glossary.md#pexclass) 的所有私有成员。

* **公共成员的可见性**
  * IntelliTest 假定它可使用在 [PexClass](attribute-glossary.md#pexclass) 的上下文中可见的所有导出成员。

## <a name="parameterized-mocks"></a>参数化模拟

如何测试具有接口类型的参数的方法？ 或者具有非密封类的参数的方法？ IntelliTest 不知道之后调用此方法时将使用哪种实现。 可能在测试时甚至没有真正的实现可用。

常规的方法是使用具有显式行为的 mock 对象  。

mock 对象会实现接口（或扩展非密封类）。 它不表示真正的实现，而只是一个允许使用 mock 对象执行测试的快捷方式。 它的行为手动定义为每个使用它的测试用例的一部分。 许多工具使定义 mock 对象及其预期行为变得简单，但仍必须手动定义此行为。

IntelliTest 可生成值，而不是 mock 对象中的硬编码值。 就像它启用[参数化单元测试](test-generation.md#parameterized-unit-testing)一样，IntelliTest 还启用参数化模拟。

参数化 mock 具有两个不同的执行模式：

*  选择：浏览代码时，参数化模拟是其他测试输入的源，IntelliTest 将尝试选择感兴趣的值
*  重播：执行之前生成的测试时，参数化模拟的行为类似于具有行为（换而言之，预定义的行为）的存根。

使用 [PexChoose](static-helper-classes.md#pexchoose) 获取参数化模拟的值。

## <a name="structs"></a>结构

IntelliTest 推理“结构”  值的方式类似于它处理[对象](#objects)的方式。

## <a name="arrays-and-strings"></a>数组和字符串

IntelliTest 运行测试和受测程序时，将监视执行的指令。 特别是，它将观察程序何时依赖于一个字符串或数组的长度（以及多维数组的下限和长度）。
它还将观察程序如何使用字符串或数组的不同元素。 然后使用[约束求解器](#constraint-solver)确定哪些长度和元素值可能会导致测试和受测程序的行为会以感兴趣的方式表现。

IntelliTest 尝试最大程度地减小触发感兴趣的程序行为所需的数组和字符串的大小。

<a name="additional-inputs"></a>
## <a name="obtain-additional-inputs"></a>获取其他输入

可使用 [PexChoose](static-helper-classes.md#pexchoose) 静态类获取测试的其他输入，并且可使用它实现[参数化模拟](#parameterized-mocks)。

## <a name="got-feedback"></a>有反馈？

在[开发人员社区](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)上发布想法和功能请求。

## <a name="further-reading"></a>其他阅读材料

* [它如何工作？](https://devblogs.microsoft.com/devops/smart-unit-tests-a-mental-model/)
