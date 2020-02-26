---
title: 警告和错误 | Microsoft IntelliTest 开发人员测试工具
ms.date: 05/02/2017
ms.topic: reference
helpviewer_keywords:
- IntelliTest, Warnings and errors
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: c3f5fe55a4e1afb1a9551d43d0d61ae9f76b81e4
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77275434"
---
# <a name="warnings-and-errors"></a>警告和错误

## <a name="warnings-and-errors-by-category"></a>警告和错误

* **边界**
  * [已超出 MaxBranches](#maxbranches-exceeded)
  * [已超出 MaxConstraintSolverTime](#maxconstraintsolvertime-exceeded)
  * [已超出 MaxConditions](#maxconditions-exceeded)
  * [已超出 MaxCalls](#maxcalls-exceeded)
  * [已超出 MaxStack](#maxstack-exceeded)
  * [已超出 MaxRuns](#maxruns-exceeded)
  * [已超出 MaxRunsWithoutNewTests](#maxrunswithoutnewtests-exceeded)

* **约束求解**
  * [无法具体化解决方案](#cannot-concretize-solution)

* **域或运行时**
  * [需要帮助来构造对象](#help-construct)
  * [需要帮助来查找类型](#help-types)
  * [猜测的可用类型](#usable-type-guessed)

* **执行**
  * [浏览期间的意外故障](#unexpected-exploration)
  * [TargetInvocationException](#targetinvocationexception)

* **检测**
  * [已调用未检测的方法](#uninstrumented-method-called)
  * [已调用外部方法](#external-method-called)
  * [已调用无法检测的方法](#uninstrumentable-method-called)
  * [可测试性问题](#testability-issue)
  * [限制](#limitation)

* **解释器**
  * [观察到调用不匹配](#observed-call-mismatch)
  * [存储在静态字段中的值](#value-static-field)

<a name="maxbranches-exceeded"></a>
## <a name="maxbranches-exceeded"></a>已超出 MaxBranches

IntelliTest 在[输入生成](input-generation.md)期间会限制其浏览的所有执行路径的长度。 当程序进入无限循环时，此功能可阻止 IntelliTest 变得无法响应。

执行和监视代码的每个条件和非条件分支均计入此限制，包括不依赖于[参数化单元测试](test-generation.md#parameterized-unit-testing)的输入的分支。

例如，以下代码按 0-100 使用分支：

```csharp
for (int i=0; i<100; i++) { }
```

可以编辑派生自 PexSettingsAttributeBase 的属性（例如 [PexClass](attribute-glossary.md#pexclass) 或 [PexMethod](attribute-glossary.md#pexmethod)）的 MaxBranches 选项   。 下面的示例可有效地移除此边界：

```csharp
[PexMethod(MaxBranches=int.MaxValue)]
public void MyTest(...) {
    // ....
}
```

还可通过设置 TestExcludePathBoundsExceeded 选项告知 IntelliTest 通常如何处理这些问题  。

在测试代码中，可使用 [PexSymbolicValue](static-helper-classes.md#pexsymbolicvalue) 来忽略循环条件生成的约束：

```csharp
for (int i=0;
    PexSymbolicValue.Ignore(i<100); // IntelliTest will 'forget' about this path condition
    i++)
{ }
```

<a name="maxconstraintsolvertime-exceeded"></a>
## <a name="maxconstraintsolvertime-exceeded"></a>已超出 MaxConstraintSolverTime

IntelliTest 使用[约束求解器](input-generation.md#constraint-solver)来计算新的测试输入。 约束求解是一个非常耗时的过程，所以 IntelliTest 允许配置边界，即 MaxConstraintSolverTime  。

对于许多应用程序，大幅度增加超时并不会有更好的覆盖率。 其原因在于，大部分超时都是由没有解决方案的约束系统引起的。 但是，IntelliTest 需要尝试所有可能的解决方法才能确定它不一致，这就会导致超时。

<a name="maxconditions-exceeded"></a>
## <a name="maxconditions-exceeded"></a>已超出 MaxConditions

IntelliTest 在[输入生成](input-generation.md)期间会限制其浏览的所有执行路径的长度。 当程序进入无限循环时，此功能可阻止 IntelliTest 变得无法响应。

每个依赖于[参数化单元测试](test-generation.md#parameterized-unit-testing)的输入的条件分支均计入此限制。

例如，以下代码中的每个路径均使用 n+1  个条件：

```csharp
[PexMethod]
void ParameterizedTest(int n) {
    // conditions are "0<n", "1<n", ..., "!(n<n)"
    for (int i=0; i<n; i++)
    { ... }

    // irrelevant for MaxConditions, since conditions do not depend on input
    for (int i=0; i<100; i++)
    { ... }
}
```

可以编辑派生自 PexSettingsAttributeBase 的属性（例如 [PexClass](attribute-glossary.md#pexclass) 或 [PexMethod](attribute-glossary.md#pexmethod)）的 MaxConditions 选项   。 例如：

```csharp
[PexMethod(MaxConditions=10000)]
void ParameterizedTest(int n) {
    // ...
}
```

还可通过设置 TestExcludePathBoundsExceeded 选项告知 IntelliTest 通常如何处理这些问题  。

可使用 [PexSymbolicValue](static-helper-classes.md#pexsymbolicvalue) 来忽略循环条件生成的约束：

```csharp
[PexMethod]
void ParameterizedTest(int n) {
    int nshadow = PexSymbolicValue.Ignore(n); // IntelliTest looses track of 'n'

    // irrevelant for MaxConditions, since nshadow is not related to input
    for (int i=0; i<nshadow; i++)
    {...}
}
```

<a name="maxcalls-exceeded"></a>
## <a name="maxcalls-exceeded"></a>已超出 MaxCalls

IntelliTest 在[输入生成](input-generation.md)期间会限制其浏览的所有执行路径的长度。 当程序进入无限循环时，此功能可阻止 IntelliTest 变得无法响应。

执行和监视代码的每个调用（直接、间接、虚拟或跳转）均计入此限制。

可编辑派生自 PexSettingsAttributeBase 的属性（例如 [PexClass](attribute-glossary.md#pexclass) 或 [PexMethod](attribute-glossary.md#pexmethod)）的 MaxCalls 选项   。 下面的示例可有效地移除此边界：

```csharp
[PexMethod(MaxCalls=int.MaxValue)]
public void MyTest(...) {
    // ....
}
```

还可通过设置 TestExcludePathBoundsExceeded 选项告知 IntelliTest 通常如何处理这些问题  。

<a name="maxstack-exceeded"></a>
## <a name="maxstack-exceeded"></a>已超出 MaxStack

IntelliTest 在[输入生成](input-generation.md)期间会限制其浏览的所有执行路径的调用堆栈大小。 发生堆栈溢出时，此功能可防止 IntelliTest 终止。

可编辑派生自 PexSettingsAttributeBase 的属性（例如 [PexClass](attribute-glossary.md#pexclass) 或 [PexMethod](attribute-glossary.md#pexmethod)）的 MaxStack 选项   。 下例可有效地移除此边界（不推荐）：

```csharp
[PexMethod(MaxStack=int.MaxValue)]
public void MyTest(...) {
    // ....
}
```

还可通过设置 TestExcludePathBoundsExceeded 选项告知 IntelliTest 通常如何处理这些问题  。

<a name="maxruns-exceeded"></a>
## <a name="maxruns-exceeded"></a>已超出 MaxRuns

IntelliTest 在[输入生成](input-generation.md)期间会限制其浏览的执行路径的数量。 程序具有循环或递归时，此功能可确保 IntelliTest 终止。

并不是每次 IntelliTest 使用特定输入运行参数化测试时，它都会发出新的测试用例。 请参阅 [TestEmissionFilter](exploration-bounds.md#testemissionfilter) 了解有关详细信息。

可编辑派生自 PexSettingsAttributeBase 的属性（例如 [PexClass](attribute-glossary.md#pexclass) 或 [PexMethod](attribute-glossary.md#pexmethod)）的 MaxRuns 选项   。 下例可有效地移除此边界（不推荐）：

```csharp
[PexMethod(MaxRuns=2000)]
public void MyTest(...) {
    // ....
}
```

<a name="maxrunswithoutnewtests-exceeded"></a>
## <a name="maxrunswithoutnewtests-exceeded"></a>已超出 MaxRunsWithoutNewTests

IntelliTest 在[输入生成](input-generation.md)期间会限制其浏览的执行路径的数量。 程序具有循环或递归时，此功能可确保 IntelliTest 终止。

并不是每次 IntelliTest 使用特定输入运行参数化测试时，它都会发出新的测试用例。 请参阅 [TestEmissionFilter](exploration-bounds.md#testemissionfilter) 了解有关详细信息。

IntelliTest 通常会在最初查找许多有趣的测试输入，但一段时间之后它就不会再发出任何其他测试。 此选项可控制 IntelliTest 在多长时间内不断尝试查找其他相关的测试输入。

可编辑派生自 PexSettingsAttributeBase 的属性（例如 [PexClass](attribute-glossary.md#pexclass) 或 [PexMethod](attribute-glossary.md#pexmethod)）的 MaxRunsWithoutNewTests 选项   。 下例可有效地移除此边界（不推荐）：

```csharp
[PexMethod(MaxRunsWithoutNewTests=2000)]
public void MyTest(...) {
    // ....
}
```

<a name="cannot-concretize-solution"></a>
## <a name="cannot-concretize-solution"></a>无法具体化解决方案

此错误通常由之前的错误导致。 IntelliTest 使用[约束求解器](input-generation.md#constraint-solver)来确定新的测试输入。 有时[约束求解器](input-generation.md#constraint-solver)建议的测试输入无效。 下列情况下测试输入无效：

* 某些约束未知
* 如果通过用户定义的方式创建值，会导致用户代码中出错
* 某些涉及的类型具有不受 IntelliTest 控制的初始化逻辑，例如 COM 类

<a name="help-construct"></a>
## <a name="need-help-to-construct-object"></a>需要帮助来构造对象

IntelliTest 会[生成测试输入](input-generation.md)，某些输入对象可能包含字段。
这时 IntelliTest 将尝试生成具有私有字段的类的实例，并假定此私有字段具有特定值时将发生有趣的程序行为。

但是，尽管使用反射可以实现这一点，IntelliTest 无法生成带有任意字段值的对象。
相反，在这些情况下，它依赖用户提示如何使用类的公共方法创建对象，并在其私有字段具有所需值时使用该对象。

如需了解如何帮助 IntelliTest 构造有趣对象，请参阅[实例化现有类](input-generation.md#existing-classes).

<a name="help-types"></a>
## <a name="need-help-to-find-types"></a>需要帮助来查找类型

IntelliTest 可针对任何 .NET 类型[生成测试输入](input-generation.md)。 这时 IntelliTest 将尝试创建一个派生自抽象类的实例或实现一个抽象接口，并且 IntelliTest 不知道满足约束的任何类型。

可通过指向一个或多个满足约束的类型来帮助 IntelliTest。 通常可使用以下属性之一提供帮助：

* **PexUseTypeAttribute**，指向特定类型。

  例如，如果 IntelliTest 报告“不知道可以分配给 System.Collections.IDictionary 的任何类型”，则可以将以下 PexUseTypeAttribute 附加到测试（或装置类），以提供帮助   ：

  ```csharp
  [PexMethod]
  [PexUseType(typeof(System.Collections.Hashtable))]
  public void MyTest(IDictionary[] dictionaries) { ... }
  ```

* **程序集级别属性**

  ```csharp
  [assembly: PexUseType(typeof(System.Collections.Hashtable))]
  ```

<a name="usable-type-guessed"></a>
## <a name="usable-type-guessed"></a>猜测的可用类型

IntelliTest 可针对任何 .NET 类型[生成测试输入](input-generation.md)。 当类型为抽象或接口时，IntelliTest 必须选择该类型的特定实现。 若要进行选择，需要知道存在哪些类型。

显示此警告，表示 IntelliTest 查找了一些引用程序集，并找到了一个实现类型，但不确定是否应使用该类型，或不确定其他位置是否有更合适的类型。 IntelliTest 只是选择了一个看似可行的类型。

为避免此警告，可接受 IntelliTest 选择的类型，或添加相应的 [PexUseType](attribute-glossary.md#pexusetype) 来帮助 IntelliTest 使用其他类型。

<a name="unexpected-exploration"></a>
## <a name="unexpected-failure-during-exploration"></a>浏览期间的意外故障

浏览测试时捕获到意外的异常。

请[将此报告为 bug](#report-bug)。

<a name="targetinvocationexception"></a>
## <a name="targetinvocationexception"></a>TargetInvocationException

用户代码中发生异常。 检查堆栈跟踪，并在代码中删除该 bug。

<a name="uninstrumented-method-called"></a>
## <a name="uninstrumented-method-called"></a>已调用未检测的方法

IntelliTest 会通过监视程序执行来[生成测试输入](input-generation.md)。 应正确检测相关代码，这一点很重要，这样 IntelliTest 才能监视其行为。

已检测代码调用其他未检测程序集中的方法时，会出现此警告。
如果希望 IntelliTest 浏览两者的交互，必须检测另一个程序集（或其中的部分内容）。

<a name="external-method-called"></a>
## <a name="external-method-called"></a>已调用外部方法

IntelliTest 会通过监视 .NET 应用程序的执行来[生成测试输入](input-generation.md)。
IntelliTest 无法针对非 .NET 语言编写的代码生成有意义的测试输入。

已检测代码调用 IntelliTest 无法分析的非托管本机方法时，会出现此警告。 如果希望 IntelliTest 浏览两者的交互，必须模拟非托管方法。

<a name="uninstrumentable-method-called"></a>
## <a name="uninstrumentable-method-called"></a>已调用无法检测的方法

IntelliTest 会通过监视 .NET 应用程序的执行来[生成测试输入](input-generation.md)。 但是出于技术原因，IntelliTest 无法监视某些方法。 例如，IntelliTest 无法监视静态构造函数。

已检测代码调用 IntelliTest 无法监视的方法时，会出现此警告。

<a name="testability-issue"></a>
## <a name="testability-issue"></a>可测试性问题

IntelliTest 会通过监视程序执行来[生成测试输入](input-generation.md)。 仅当程序确定，并且相关行为由测试输入控制时才能生成相关测试输入。

执行测试用例期间，如果调用方法的行为不确定或与环境进行交互，会出现此警告。 示例包括 System.Random 和 System.IO.File 的方法   。 如果希望 IntelliTest 创建有意义的测试输入，必须模拟 IntelliTest 标记为可测试性问题的方法。

<a name="limitation"></a>
## <a name="limitation"></a>限制

IntelliTest 会使用[约束求解器](input-generation.md#constraint-solver)来[生成测试输入](input-generation.md)。
但是有些操作不在[约束求解器](input-generation.md#constraint-solver)范围内。
目前包括：

* 大部分浮点操作（浮点数仅支持某些线性运算）
* 浮点数和整数之间的转换
* System.Decimal 类型上的所有操作 

执行的代码执行操作或调用 IntelliTest 无法解释的方法时，会出现此警告。

<a name="observed-call-mismatch"></a>
## <a name="observed-call-mismatch"></a>观察到调用不匹配

IntelliTest 会通过监视程序执行来[生成测试输入](input-generation.md)。 但是 IntelliTest 无法监视所有说明。 例如，它无法监视本机代码，并且无法监视未检测的代码。

IntelliTest 无法监视代码时，就无法生成与该代码相关的测试输入。
通常情况下，对方法的调用返回之前，IntelliTest 根本不知道它无法监视该方法。 但是，出现此警告的原因在于：

* IntelliTest 监视了某些代码，该代码启动了对未检测方法的调用
* 未检测的方法调用了已检测的方法
* IntelliTest 监视调用的已检测方法

IntelliTest 不知道未检测中间方法的作用，因此无法生成与嵌套的已检测调用相关的测试输入。

<a name="value-static-field"></a>
## <a name="value-stored-in-static-field"></a>存储在静态字段中的值

只有单元测试确定时，IntelliTest 才能系统地确定[相关测试输入](input-generation.md)，换而言之，它对相同测试输入的处理方式始终相同。 具体而言，这意味着测试应使系统处于能够重新执行该测试的状态。
理想情况下，单元测试不应更改任何全局状态，但应模拟与全局的所有交互。

此警告表示静态字段已更改；这可能会使测试行为不确定。

以下情况可以更改静态字段：

* 测试输入导致安装或清理代码撤消更改时
* 该字段只启动一次，并且之后该值不再更改时

<a name="report-bug"></a>

## <a name="got-feedback"></a>是否获得反馈？

在[开发人员社区](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)上发布想法和功能请求。
