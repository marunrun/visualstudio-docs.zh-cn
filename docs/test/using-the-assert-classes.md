---
title: MSTest Assert 类和方法
ms.date: 06/07/2018
ms.topic: reference
helpviewer_keywords:
- Assert classes
- Assert methods
- unit tests, Assert classes
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: c36916c79bd783ed2c6ce960b068e85478b9971d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592043"
---
# <a name="use-assert-classes-for-unit-testing"></a>使用 Assert 类进行单元测试

使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting> 命名空间的 Assert 类来验证特定功能。 单元测试方法执行应用程序代码中的方法代码，但只有包含 Assert 语句时，它才会报告代码行为的正确性。

## <a name="kinds-of-asserts"></a>Assert 的类型

<xref:Microsoft.VisualStudio.TestTools.UnitTesting> 命名空间提供数种类型的 Assert 类。

在测试方法中，可以调用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=fullName> 类的任何方法，如 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A?displayProperty=nameWithType>。 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> 类有许多方法可供选择，并且其中有很多方法具有若干重载。

### <a name="compare-strings-and-collections"></a>比较字符串和集合

使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CollectionAssert> 类比较对象的集合，并验证集合的状态。

使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert> 类来比较和检查字符串。 此类包含各种有用的方法，如 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Contains%2A?displayProperty=nameWithType>、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Matches%2A?displayProperty=nameWithType> 和 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.StartsWith%2A?displayProperty=nameWithType>。

### <a name="exceptions"></a>异常

测试失败时，将引发 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertFailedException> 异常。 如果测试超时，引发意外的异常，或者包含生成失败结果的 Assert 语句，则测试将失败  。

测试生成无结论的结果时，将引发 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertInconclusiveException>  。 通常，将 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Inconclusive%2A?displayProperty=nameWithType> 语句添加到仍在处理的测试中，以指示它是否尚未准备好运行。

> [!NOTE]
> 备用策略使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.IgnoreAttribute> 属性标记尚未准备好运行的测试。 但是，这样做的弊端是你无法轻松地对未执行的测试数量生成报表。

如果编写新的 Assert 异常类，让该类从基类 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.UnitTestAssertException> 继承使其可更轻松地将异常识别为断言失败，而不是从测试或生产代码引发的意外异常。

要验证期望由应用程序代码中的方法引发的异常确实已引发，请使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A?displayProperty=nameWithType> 方法。

## <a name="see-also"></a>请参阅

- [单元测试代码](../test/unit-test-your-code.md)
