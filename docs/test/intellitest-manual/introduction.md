---
title: 概述 | Microsoft IntelliTest 开发人员测试工具
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Visual Studio IntelliTest developer testing tool
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: dfa81e7afe313a112e2355ddf5efadb70c555477
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591589"
---
# <a name="overview-of-microsoft-intellitest"></a>Microsoft IntelliTest 的概述

IntelliTest 使你能够尽早发现 bug，降低测试维护成本。 IntelliTest 使用一种自动化透明的测试方法，为 .NET 代码生成备用的测试套件。 测试套件生成可由指定的“正确性属性”  进行进一步引导。 IntelliTest 甚至会随受测代码的变化而自动完善测试套件。

**表征测试** 通过 IntelliTest 可确定传统单元测试套件方面的代码行为。
这类测试套件可用作回归套件，为处理重构旧代码或陌生代码相关的复杂问题奠定基础。

**引导式测试输入生成** IntelliTest 使用开放代码分析和约束求解方法，自动生成精确的测试输入值；通常无需任何用户的干预。 对于复杂对象类型，它会自动生成工厂。 可通过扩展和配置工厂来满足要求，以此来引导测试输入生成。 还可自动使用代码中指定为断言的正确性属性，进一步引导生成测试输入。

**IDE 集成** IntelliTest 已完全集成到 Visual Studio IDE 中。 测试套件生成过程中收集的所有信息（如自动生成的输入、代码中的输出、生成的测试用例及其通过或未通过状态）将显示在 Visual Studio IDE 中。 可轻松在修复代码和重新运行 IntelliTest 之间循环访问，无需离开 Visual Studio IDE。
这些测试可保存到解决方案中作为单元测试项目，之后 Visual Studio 测试资源管理器会自动检测到它们。

**补充现有测试方案** 使用 IntelliTest 补充任何可能已遵照执行的现有测试方案。

如果想要测试：

* 针对基元数据或基元数据数组的算法：
  * 编写[参数化单元测试](test-generation.md#parameterized-unit-testing)
* 针对复杂数据（如编译器）的算法：
  * 让 IntelliTest 首先生成数据的抽象表示形式，然后将其添加到算法中
  * 让 IntelliTest 使用[自定义对象创建](input-generation.md#objects)和数据不变量生成实例，然后调用算法
* 数据容器：
  * 编写[参数化单元测试](test-generation.md#parameterized-unit-testing)
  * 让 IntelliTest 使用[自定义对象创建](input-generation.md#objects)和数据不变量生成实例，然后调用容器的方法，之后重新检查不变量
  * 编写根据参数值调用不同实现方法的[参数化单元测试](test-generation.md#parameterized-unit-testing)
* 现有代码基础：
  * 使用 Visual Studio 的 IntelliTest 向导，通过生成一组[参数化单元测试 (PUT)](test-generation.md#parameterized-unit-testing) 入门

## <a name="the-hello-world-of-intellitest"></a>IntelliTest 的 Hello World

IntelliTest 查找与测试程序相关的输入，这意味着可使用它生成众所周知的“Hello World!”  字符串。 此处假设已创建了一个基于 C# MSTest 的测试项目并添加了对 Microsoft.Pex.Framework  的引用。 如果使用不同的测试框架，请创建一个 C# 类库并参阅有关如何设置项目的测试框架文档。

以下示例针对名为 value  的参数创建两个约束，以便 IntelliTest 生成所需的字符串：

```csharp
using System;
using Microsoft.Pex.Framework;
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public partial class HelloWorldTest {
    [PexMethod]
    public void HelloWorld([PexAssumeNotNull]string value) {
        if (value.StartsWith("Hello")
            && value.EndsWith("World!")
            && value.Contains(" "))
            throw new Exception("found it!");
    }
}
```

编译并执行后，IntelliTest 会生成一组如下所示的测试：

1. ""
2. "\0\0\0\0\0"
3. "Hello"
4. "\0\0\0\0\0\0"
5. "Hello\0"
6. "Hello\0\0"
7. "Hello\0World!"
8. "Hello World!"

> [!NOTE]
> 对于生成问题，请尝试将Microsoft.VisualStudio.TestPlatform.TestFramework 和 Microsoft.VisualStudio.TestPlatform.TestFramework.Extensions 引用替换为 Microsoft.VisualStudio.QualityTools.UnitTestFramework。

阅读[使用 IntelliTest 生成单元测试](../../test/generate-unit-tests-for-your-code-with-intellitest.md)，了解生成的测试的保存位置。 生成的测试代码应包含如下所示的测试：

```csharp
[TestMethod]
[PexGeneratedBy(typeof(global::HelloWorldTest))]
[PexRaisedException(typeof(Exception))]
public void HelloWorldThrowsException167()
{
    this.HelloWorld("Hello World!");
}
```

就这么简单！

## <a name="limitations"></a>限制

本部分介绍 IntelliTest 的限制：

* [不确定性](#nondeterminism)
* [并发](#concurrency)
* [本机 .NET 代码](#native-code)
* [平台](#platform)
* [语言](#language)
* [符号推理](#symbolic-reasoning)
* [堆栈跟踪](#incorrect-stack-traces)

### <a name="nondeterminism"></a>不确定性

IntelliTest 假定分析的程序是确定的。 否则 IntelliTest 将循环，直到它达到浏览边界。

如果程序依赖于 IntelliTest 无法控制的输入，IntelliTest 将其视为非确定。

IntelliTest 控制提供给[参数化单元测试](test-generation.md#parameterized-unit-testing)的输入和从 [PexChoose](static-helper-classes.md#pexchoose) 获得的输入。
从这种意义上来说，对非托管代码或未检测代码的调用结果也会被视为已检测程序的“输入”，但 IntelliTest 无法控制它们。 如果程序的控制流依赖于来自这些外部源的特定值，IntelliTest 将无法将程序“引向”之前未覆盖的区域。

此外，如果来自外部源的值在重新运行程序时更改，该程序将被视为非确定。 在这种情况下，IntelliTest 会失去对程序执行的控制，且其搜索效率会变得低下。

出现这种情况时，有时并不明显。 请开考虑以下示例：

* GetHashCode()  方法的结果由非托管代码提供，不可预测。
* System.Random  类使用当前系统时间提供真正随机的值。
* System.DateTime  类提供当前时间，该时间不受 IntelliTest 控制。

### <a name="concurrency"></a>并发

IntelliTest 不处理多线程的程序。

### <a name="native-code"></a>本机代码

IntelliTest 不了解本机代码，如通过 P/Invoke  调用的 x86 指令。 它并不知道如何将此种调用转换为可传递到[约束求解器](input-generation.md#constraint-solver)的约束。
即使对于 .NET 代码，它也只可分析它检测的代码。 IntelliTest 无法检测 mscorlib  的某些部分，包括反射库。 无法检测 DynamicMethod  。

建议的解决方法是当此类方法位于动态程序集的类型中时采用测试模式。 但是，即使某些方法未检测，IntelliTest 也会尝试尽可能多地覆盖已检测的代码。

### <a name="platform"></a>Platform

仅 32 位的 X86 NETframework 支持 IntelliTest。

### <a name="language"></a>语言

原则上，IntelliTest 可分析以任何 .NET 语言编写的任意 .NET 程序。 但在 Visual Studio 中，它仅支持 C#。

### <a name="symbolic-reasoning"></a>符号推理

IntelliTest 使用自动[约束求解器](input-generation.md#constraint-solver)确定哪些值与测试和受测代程序相关。 但是，约束求解器的能力始终有限。

### <a name="incorrect-stack-traces"></a>不正确的堆栈跟踪

因为 IntelliTest 在每个已检测方法中捕获并“重新引发”异常，堆栈跟踪中的行号将不正确。 这是“重新引发”指令设计的局限性。

## <a name="further-reading"></a>其他阅读材料

* [介绍性的博客文章](https://devblogs.microsoft.com/devops/introducing-smart-unit-tests/)。
* [使用 IntelliTest 为代码生成单元测试](../../test/generate-unit-tests-for-your-code-with-intellitest.md)
