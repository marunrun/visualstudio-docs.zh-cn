---
title: 静态帮助程序类 | Microsoft IntelliTest 开发人员测试工具
ms.date: 05/02/2017
ms.topic: reference
helpviewer_keywords:
- IntelliTest, Static helper classes
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 5010761213cf79756cf8da3d2fffe60dd0b61efd
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79306985"
---
# <a name="static-helper-classes"></a>静态帮助程序类

IntelliTest 提供了一套静态帮助程序类，可供创作[参数化单元测试](test-generation.md#parameterized-unit-testing)时使用：

* [PexAssume](#pexassume)：用于定义对输入的假设，并且对筛选不需要的输入非常有用
* [PexAssert](#pexassert)：一个简单的断言类，可在测试框架未提供断言类时使用
* [PexChoose](#pexchoose)：IntelliTest 管理的一系列其他测试输入
* [PexObserve](#pexobserve)：记录具体值，并在生成的代码中对其进行验证（可选）

使用某些类可以与 IntelliTest 推理引擎进行低级别交互：

* [PexSymbolicValue](#pexsymbolicvalue)：检查或修改对变量的符号约束的实用程序

<a name="pexassume"></a>
## <a name="pexassume"></a>PexAssume

表示假设的静态类，例如[参数化单元测试](test-generation.md#parameterized-unit-testing)中的[前置条件](test-generation.md#precondition)。 此类的方法可用于筛除不需要的测试输入。

如果假设的条件不适用于某些测试输入，则会引发 PexAssumeFailedException  。 这将导致在无提示的情况下忽略该测试。

**示例**

以下参数化测试不会考虑 j = 0  ：

```csharp
public void TestSomething(int i, int j) {
     PexAssume.AreNotEqual(j, 0);
     int k = i/j;
     ...
}
```

**备注**

上述代码几乎等效于：

```csharp
     if (j==0)
          return;
```

只是 PexAssume 失败时会导致无测试用例  。 使用 if 语句时，IntelliTest 会生成一个单独的测试用例，使其包含 if 语句的 then 分支    。

PexAssume  还包含专用的嵌套类，用于对字符串、数组和集合进行假设。

<a name="pexassert"></a>
## <a name="pexassert"></a>PexAssert

表示断言的静态类，例如[参数化单元测试](test-generation.md#parameterized-unit-testing)中的[后置条件](test-generation.md#postcondition)。

如果断言的条件不适用于某些测试输入，则会引发 PexAssertFailedException，这将导致测试失败  。

**示例**

以下断言中整数的绝对值为正：

```csharp
public void TestSomething(int i) {
     int j = Maths.Abs(i);
     PexAssert.IsTrue(j >= 0);
     ...
}
```

<a name="pexchoose"></a>
## <a name="pexchoose"></a>PexChoose

向测试提供辅助输入值的静态类，可用于实现[参数化模拟](input-generation.md#parameterized-mocks)。

PexChoose 类不可用于确定针对特定输入值的测试通过或失败  。 PexChoose 只提供输入值，也称为“选择”   。 仍由用户负责限制输入值，并写入定义测试何时通过或失败的断言。

**操作模式**

PexChoose 类可在两种模式下运行  ：

* IntelliTest 在[输入生成](input-generation.md)期间对测试和经测试代码执行符号分析时，选择器会返回任意值，并且 IntelliTest 会跟踪每个值在测试和经测试代码中的使用方式。 IntelliTest 会生成相关值，以触发测试和经测试代码中的不同执行路径。

* 针对特定测试用例生成的代码会通过某种方式设置选择提供程序，在重新执行此类测试用例时进行特定选择，以触发特定的执行路径。

**用法**

* 简单调用 PexChoose.Value 生成新值  ：

```csharp
public int Foo() {
    return PexChoose.Value<int>("foo");
}
```

<a name="pexobserve"></a>
## <a name="pexobserve"></a>PexObserve

记录已命名值的静态类。

IntelliTest 浏览代码时，会通过 PexObserve 记录使用其格式化字符串表现形式的计算值  。 该值与唯一名称相关联。

```csharp
PexObserve.Value<string>("result", result);
```

**示例**

```csharp
// product code
public static class MathEx {
     public static int Square(int value) { return value * value; }
}

// fixture
[TestClass]
public partial class MathExTests {
     [PexMethod]
     public int SquareTest(int a) {
        int result = MathEx.Square(a);
        // storing result
        return result;
     }
}
```

<a name="pexsymbolicvalue"></a>
## <a name="pexsymbolicvalue"></a>PexSymbolicValue

一个静态类，用于忽略对参数的约束，并打印与值关联的符号信息。

**用法**

通常情况下，IntelliTest 会在执行期间尝试涵盖代码的所有执行路径。 但是，它无法浏览所有可能的用例，尤其是在计算假设和断言条件时。

**示例**

此示例演示了如何实现 PexAssume.Arrays.ElementsAreNotNull 方法  。
在该方法中会忽略对数组值长度的约束，以避免 IntelliTest 尝试生成其他大小的数组。 只在此处忽略该约束。 如果经测试代码对不同数组长度的处理方式不同，IntelliTest 无法根据对经测试代码的约束生成不同大小的数组。

```csharp
public static void AreElementsNotNull<T>(T[] value)
    where T : class
{
    PexAssume.NotNull(value);
    // the followings prevents the exploration of all array lengths
    int len = PexSymbolicValue.Ignore<int>(value.Length);

    // building up a boolean value as follows prevents exploration
    // of all combinations of non-null (instead, there are just two cases)
    bool anyNull = false;
    for (int i = 0; i < len; ++i)
        anyNull |= value[i] == null;

    // was any element null?
    if (anyNull)
        PexAssume.Fail("some element of array is a null reference");
}
```

## <a name="got-feedback"></a>有反馈？

在[开发人员社区](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)上发布想法和功能请求。
