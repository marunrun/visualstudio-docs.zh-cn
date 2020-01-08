---
title: 测试生成 | Microsoft IntelliTest 开发人员测试工具
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Test generation
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: c251a1539b42da2b4e92c2996457075f3c3be135
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591549"
---
# <a name="test-generation"></a>测试生成

在传统单元测试中，测试包含多项内容：

* [方法调用的序列](test-generation.md#test-generators)
* 调用方法时使用的参数，即[测试输入](input-generation.md)
* 通过声明一组[断言](#assumptions-and-assertions)来验证测试应用程序的预期行为

下面是一个示例测试结构：

```csharp
[Test]
void MyTest() {
    // data
    ArrayList a = new ArrayList();

    // method sequence
    a.Add(5);

    // assertions
    Assert.IsTrue(a.Count==1);
    Assert.AreEqual(a[0], 5);
}
```

IntelliTest 通常可以自动确定更常规[参数化单元测试](#parameterized-unit-testing)的相关参数值，提供方法调用和断言序列。

<a name="test-generators"></a>
## <a name="test-generators"></a>测试生成器

IntelliTest 生成测试用例的方法如下：选择正在测试并即将执行的实现方法的序列，然后生成方法的输入，并检查派生数据的断言。

[参数化单元测试](#parameterized-unit-testing)在其主体中直接声明方法调用的序列。

IntelliTest 需要构造对象时，将根据需要在序列中自动添加对构造函数和工厂方法的调用。

<a name="parameterized-unit-testing"></a>
## <a name="parameterized-unit-testing"></a>参数化单元测试

参数化单元测试 (PUT) 是采用参数的测试  。 传统单元测试通常是封闭的方法，PUT 与之不同，可采用任何参数集。 是不是很简单？ 是的 - IntelliTest 将从此尝试[生成（最小）输入集](input-generation.md)，[完全涵盖](input-generation.md#dynamic-code-coverage)可从测试访问的代码。

PUT 使用 [PexMethod](attribute-glossary.md#pexmethod) 自定义属性定义，其方式与 MSTest（或 NUnit、xUnit）类似。 PUT 实例方法按逻辑分组成使用 [PexClass](attribute-glossary.md#pexclass) 标记的类。 下面的示例展示了 MyPexTest 类中存储的简单 PUT  ：

```csharp
[PexMethod]
void ReplaceFirstChar(string target, char c) {

    string result = StringHelper.ReplaceFirstChar(target, c);

    Assert.AreEqual(result[0], c);
}
```

其中 **ReplaceFirstChar** 是替换字符串第一个字符的方法：

```csharp
class StringHelper {
    static string ReplaceFirstChar(string target, char c) {
        if (target == null) throw new ArgumentNullException();
        if (target.Length == 0) throw new ArgumentOutOfRangeException();
        return c + target.Substring(1);
    }
}
```

在此测试中，IntelliTest 可以自动为 PUT [生成输入](input-generation.md)，且该输入包含测试代码的许多执行路径。 每个包含不同执行路径的输入将被“序列化”为单元测试：

```csharp
[TestMethod, ExpectedException(typeof(ArgumentNullException))]
void ReplaceFirstChar0() {
    this.ReplaceFirstChar(null, 0);
}
...
[TestMethod]
void ReplaceFirstChar10() {
    this.ReplaceFirstChar("a", 'c');
}
```

<a name="generic-parameterized"></a>
## <a name="generic-parameterized-unit-testing"></a>泛型参数化单元测试

参数化单元测试可以是泛型方法。 在这种情况下，用户必须使用 [PexGenericArguments](attribute-glossary.md#pexgenericarguments) 指定用于实例化该方法的类型。

```csharp
[PexClass]
public partial class ListTest {
    [PexMethod]
    [PexGenericArguments(typeof(int))]
    [PexGenericArguments(typeof(object))]
    public void AddItem<T>(List<T> list, T value)
    { ... }
}
```

<a name="allowing-exceptions"></a>
## <a name="allowing-exceptions"></a>允许异常

IntelliTest 提供大量验证属性，帮助将异常分类为预期异常和意外异常。

预期异常生成带有“ExpectedException(typeof(xxx))”等注释的负面测试用例，而意外异常生成失败测试用例   。

```csharp
[PexMethod, PexAllowedException(typeof(ArgumentNullException))]
void SomeTest() {...}
```

验证程序包括：

* [PexAllowedException](attribute-glossary.md#pexallowedexception)：允许任何位置出现特定异常类型
* [PexAllowedExceptionFromAssembly](attribute-glossary.md#pexallowedexceptionfromassembly)：允许指定程序集中出现特定异常类型
* [PexAllowedExceptionFromType](attribute-glossary.md#pexallowedexceptionfromtype)：允许指定类型中出现特定异常类型
* [PexAllowedExceptionFromTypeUnderTest](attribute-glossary.md#pexallowedexceptionfromtypeundertest)：允许正在测试的类型中出现特定异常类型

<a name="internal-types"></a>
## <a name="testing-internal-types"></a>测试内部类型

只要 IntelliTest 能找到内部类型，就可以对其进行“测试”。 若要使 IntelliTest 找到类型，可通过 Visual Studio IntelliTest 向导将以下属性添加到产品或测试项目：

```csharp
[assembly: InternalsVisibleTo("Microsoft.Pex, PublicKey=002400000480000094000000060200000024000052534131000400000100010007d1fa57c4aed9f0a32e84aa0faefd0de9e8fd6aec8f87fb03766c834c99921eb23be79ad9d5dcc1dd9ad236132102900b723cf980957fc4e177108fc607774f29e8320e92ea05ece4e821c0a5efe8f1645c4c0c93c1ab99285d622caa652c1dfad63d745d6f2de5f17e5eaf0fc4963d261c8a12436518206dc093344d5ad293")]
```

<a name="assumptions-and-assertions"></a>
## <a name="assumptions-and-assertions"></a>假设和断言

用户可以使用假设和断言来表示有关测试的[前置条件](#precondition)（假设）和[后置条件](#postcondition)（断言）。 IntelliTest 生成一组参数值和“浏览”代码时，可能会违反测试的假设。 在这种情况下，它将不会生成该路径的测试，而会以无提示方式忽略该路径。

断言是常规单元测试框架中的常见概念，因此 IntelliTest 已“了解”每个受支持测试框架提供的内置 Assert 类  。 但是大部分框架不会提供 Assume 类  。 在这种情况下，IntelliTest 会提供 [PexAssume](static-helper-classes.md#pexassume) 类。 如果不想使用现有的测试框架，IntelliTest 还有 [PexAssert](static-helper-classes.md#pexassert) 类。

```csharp
[PexMethod]
public void Test1(object o) {
    // precondition: o should not be null
    PexAssume.IsNotNull(o);

    ...
}
```

具体而言，非空假设可以编码为自定义属性：

```csharp
[PexMethod]
public void Test2([PexAssumeNotNull] object o)
// precondition: o should not be null
{
   ...
}
```

<a name="precondition"></a>
## <a name="precondition"></a>前置条件

方法的前置条件表示在该条件下方法会成功。

通常情况下，通过检查参数和对象声明，并在违反时引发 ArgumentException 或 InvalidOperationException 来强制执行前置条件   。

在 IntelliTest 中，[参数化单元测试](#parameterized-unit-testing)的前置条件使用 [PexAssume](static-helper-classes.md#pexassume) 表示。

<a name="postcondition"></a>
## <a name="postcondition"></a>后置条件

方法的后置条件表示前置条件最初有效时，执行方法期间和之后应保持的条件。

通常情况下，通过调用 Assert 方法来强制执行后置条件  。

使用 IntelliTest 时，[参数化单元测试](#parameterized-unit-testing)的后置条件使用 [PexAssert](static-helper-classes.md#pexassert) 表示。

<a name="test-failures"></a>
## <a name="test-failures"></a>测试失败
生成的测试用例在什么情况下失败？

1. 如果测试用例未在[配置的路径边界](exploration-bounds.md)内终止，则被视为失败，除非设置了 [TestExcludePathBoundsExceeded](exploration-bounds.md#testexcludepathboundsexceeded) 选项

1. 如果测试引发 PexAssumeFailedException，则测试成功  。 但是，它通常会被筛除，除非 [TestEmissionFilter](exploration-bounds.md#testemissionfilter) 被设置为“全部” 

1. 如果测试违反[断言](#assumptions-and-assertions)例如，引发单元测试框架的断言冲突异常时，测试失败

如果上述情况未导致失败，则当且仅当未引发任何异常时，测试成功。 断言冲突的处理方式与异常相同。

<a name="setup-teardown"></a>
## <a name="setup-and-tear-down"></a>设置和清理

作为与测试框架集成的一部分，IntelliTest 支持检测和运行设置和清理方法。

**示例**

```csharp
using Microsoft.Pex.Framework;
using NUnit.Framework;

namespace MyTests
{
    [PexClass]
    [TestFixture]
    public partial class MyTestClass
    {
        [SetUp]
        public void Init()
        {
            // monitored
        }

        [PexMethod]
        public void MyTest(int i)
        {
        }

        [TearDown]
        public void Dispose()
        {
            // monitored
        }
    }
}
```

<a name="further-reading"></a>
## <a name="further-reading"></a>其他阅读材料

* [代码绑定测试](https://devblogs.microsoft.com/devops/smart-unit-tests-test-to-code-binding-test-case-management/)
* [One test to rule them all](https://devblogs.microsoft.com/devops/intellitest-one-test-to-rule-them-all/)（一个测试掌控所有情况）

## <a name="got-feedback"></a>是否获得反馈？

在[开发人员社区](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)上发布想法和功能请求。
