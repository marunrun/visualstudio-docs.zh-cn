---
title: 浏览边界 | Microsoft IntelliTest 开发人员测试工具
ms.date: 05/02/2017
ms.topic: reference
helpviewer_keywords:
- IntelliTest, Exploration bounds
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: jillre
ms.openlocfilehash: 03f23aacbe95615b565dfcee54d2b620c0ae1cd9
ms.sourcegitcommit: 00ba14d9c20224319a5e93dfc1e0d48d643a5fcd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "77091829"
---
# <a name="exploration-bounds"></a>浏览边界

PexSettingsAttributeBase  是设置边界即特性的抽象基类。 请参阅[设置瀑布图](settings-waterfall.md)，大致了解 IntelliTest 中的设置。

使用该设置的命名属性及其派生特性可修改设置：

```csharp
[PexClass(MaxRuns = 10)]
public partial class FooTest {...}
```

* **约束求解边界**
  * [MaxConstraintSolverTime](#maxconstraintsolvertime) - [约束求解器](input-generation.md#constraint-solver)必须发现将导致后跟一个新的其他执行路径的输入所需的秒数。
  * [MaxConstraintSolverMemory](#maxconstraintsolvermemory) - [约束求解器](input-generation.md#constraint-solver)可能用于发现输入的大小 (MB)。
* **浏览路径边界**
  * [MaxBranches](#maxbranches) - 可能沿单个执行路径使用的最大分支数。
  * [MaxCalls](#maxcalls) - 可能在单个执行路径期间执行的最大调用数。
  * [MaxStack](#maxstack) - 单个执行路径期间任何时候的堆栈最大大小，以活动调用的帧数来衡量。
  * [MaxConditions](#maxconditions) - 可能在单个执行路径期间检查的最大输入条件数。
* **浏览边界**
  * [MaxRuns](#maxruns) - 浏览期间将尝试运行的最大次数。
  * [MaxRunsWithoutNewTests](#maxrunswithoutnewtests) - 不发出新测试情况下连续运行的最大数目。
  * [MaxRunsWithUniquePaths](#maxrunswithuniquepaths) - 浏览期间，将尝试使用唯一执行路径运行的最大次数。
  * [MaxExceptions](#maxexceptions) - 在所有发现的执行路径组合中可能找到的最大异常数。
* **测试套件代码生成设置**
  * [TestExcludePathBoundsExceeded](#testexcludepathboundsexceeded) - 为 true 时，将忽略超过任何路径边界的执行路径（[MaxCalls](#maxcalls)、[MaxBranches](#maxbranches)、[MaxStack](#maxstack)、[MaxConditions](#maxconditions)）。
  * [TestEmissionFilter](#testemissionfilter) - 指示 IntelliTest 应在哪些情况下发出测试。
  * [TestEmissionBranchHits](#testemissionbranchhits) - 控制 IntelliTest 发出的测试数量。

<a name="maxconstraintsolvertime"></a>
## <a name="maxconstraintsolvertime"></a>MaxConstraintSolverTime

[约束求解器](input-generation.md#constraint-solver)必须计算将导致使用一个新的其他执行路径的输入所需的秒数。 这是 PexSettingsAttributeBase  及其派生类型的一个选项。

IntelliTest 浏览程序的执行路径越深，IntelliTest 从程序的控制流和数据流生成的约束系统就会变得越复杂。 根据时间限制，可通过设置此值，让 IntelliTest 花费更多或更少的时间来发现新的执行路径。

通常情况下，超时的原因是 IntelliTest 尝试为不含解决方案的约束系统查找解决方案，但它并没有意识到没有解决方案这个事实。 由于这是最常见的超时情况，增加边界可能毫无意义。

<a name="maxconstraintsolvermemory"></a>
## <a name="maxconstraintsolvermemory"></a>MaxConstraintSolverMemory

[约束求解器](input-generation.md#constraint-solver)必须计算将导致使用一个新的其他执行路径的输入的大小 (MB)。 这是 PexSettingsAttributeBase  * 及其派生类型的一个选项。

IntelliTest 浏览程序的执行路径越深，IntelliTest 从程序的控制流和数据流生成的约束系统就会变得越复杂。 根据计算机的可用内存，可通过设置此值，让 IntelliTest 处理更复杂的约束系统。

通常情况下，超时的原因是 IntelliTest 尝试为不含解决方案的约束系统查找解决方案，但它并没有意识到没有解决方案这个事实。 由于这是内存不足情况最常见的原因，增加边界可能毫无意义。

<a name="maxbranches"></a>
## <a name="maxbranches"></a>MaxBranches

可能沿单个执行路径使用的最大分支数。

此浏览边界背后的动机是限制[输入生成](input-generation.md)期间 IntelliTest 浏览的任何执行路径的长度。 具体而言，如果程序进入无限循环，此功能可阻止 IntelliTest 变得无法响应。

执行和监视代码的每个条件和非条件分支均计入此限制，包括不依赖于参数化测试的输入的分支。

例如，以下代码按 0-100 使用分支：

```csharp
for (int i=0; i<100; i++) { }
```

<a name="maxcalls"></a>
## <a name="maxcalls"></a>MaxCalls

可能在单个执行路径期间执行的最大调用数。

此浏览边界背后的动机是限制[输入生成](input-generation.md)期间 IntelliTest 浏览的任何执行路径的长度。 具体而言，如果程序以递归方式调用某方法无限次，则会导致堆栈溢出并且 IntelliTest 无法恢复，此功能可防止 IntelliTest 变得无法响应。

执行和监视代码的每个调用（直接、间接、虚拟、跳转）均计入此限制。

<a name="maxstack"></a>
## <a name="maxstack"></a>MaxStack

单个执行路径期间任何时候的堆栈最大大小，以活动调用的帧数来衡量。

此浏览边界背后的动机是限制[输入生成](input-generation.md)期间 IntelliTest 浏览的任何执行路径的堆栈大小。 具体而言，它会阻止 IntelliTest 使用所有可用的堆栈空间，否则会导致堆栈溢出并且 IntelliTest 无法恢复。

<a name="maxconditions"></a>
## <a name="maxconditions"></a>MaxConditions

可能在单个执行路径期间检查的输入的最大条件数。

此浏览边界背后的动机是限制[输入生成](input-generation.md)期间 IntelliTest 浏览的任何执行路径的复杂性。 每个依赖于参数化测试的输入的条件分支均计入此限制。

例如，以下代码中的每个路径使用 n+1 个条件：

```csharp
[PexMethod]
void ParameterizedTest(int n)
{
     for (int i=0; i<n; i++) { // conditions are "0<n", "1<n", ..., "!(n<n)"
          ...
     }
     for (int i=0; i<100; i++) { // irrelevant for MaxConditions, since conditions do not depend on input
          ...
     }
}
```

<a name="maxruns"></a>
## <a name="maxruns"></a>MaxRuns

浏览测试期间 IntelliTest 将尝试运行的最大次数。

此浏览边界背后的动机是包含循环或递归的任何代码可能具有无限数目的执行路径，因此需要在[输入生成](input-generation.md)期间限制 IntelliTest。

MaxRuns  和 MaxRunsWithUniquePaths  这两个设置的关系如下所示：

* IntelliTest 将使用不同的测试输入调用参数化测试方法最多 MaxRuns  次。
* 如果执行代码是确定的，IntelliTest 每次将使用不同的执行路径。 但在某些情况下，执行代码可能会使用不同的输入沿用之前使用过的执行路径。
* IntelliTest 计算找到的唯一执行路径数；此数目受 MaxRunsWithUniquePaths  选项限制。

<a name="maxrunswithoutnewtests"></a>
## <a name="maxrunswithoutnewtests"></a>MaxRunsWithoutNewTests

在不发出新测试的情况下连续运行的最大数目。

虽然 IntelliTest 通常可在短时间内找到许多有趣的测试输入，但一段时间后，它将找不到其他新的测试输入，并且不再发出单元测试。 此配置选项对在不发出新测试的情况下 IntelliTest 可能执行的连续尝试次数进行了限制。 达到限制即停止浏览。

<a name="maxrunswithuniquepaths"></a>
## <a name="maxrunswithuniquepaths"></a>MaxRunsWithUniquePaths

浏览期间，IntelliTest 将考虑使用的唯一路径最大数。

此浏览边界背后的动机是包含循环或递归的任何代码可能具有无限数目的执行路径，因此必须在[输入生成](input-generation.md)期间限制 IntelliTest。

MaxRuns  和 MaxRunsWithUniquePaths  这两个设置的关系如下所示：

* IntelliTest 将使用不同的测试输入调用参数化测试方法最多 MaxRuns  次。
* 如果执行代码是确定的，IntelliTest 每次将使用不同的执行路径。 但在某些情况下，执行代码可能会使用不同的输入沿用之前使用过的执行路径。
* IntelliTest 计算找到的唯一执行路径数；此数目受 MaxRunsWithUniquePaths  选项限制。

<a name="maxexceptions"></a>
## <a name="maxexceptions"></a>MaxExceptions

停止浏览前可能遇到的最大异常数。

此浏览边界背后的动机是停止浏览包含多个 bug 的代码。 如果 IntelliTest 在代码中找到太多错误，则停止浏览。

<a name="testexcludepathboundsexceeded"></a>
## <a name="testexcludepathboundsexceeded"></a>TestExcludePathBoundsExceeded

将忽略超过配置的路径边界 [MaxCalls](#maxcalls)、[MaxBranches](#maxbranches)、[MaxStack](#maxstack) 和 [MaxConditions](#maxconditions) 的执行路径。

此浏览边界背后的动机是处理（大多数情况下）非终止测试。 IntelliTest 达到浏览边界（如[MaxCalls](#maxcalls)、[MaxBranches](#maxbranches)、[MaxStack](#maxstack) 或 [MaxConditions](#maxconditions)）时，它会假定测试不是非终止进程，且之后不会导致堆栈溢出。 这种测试用例可能会给其他测试框架带来问题，但此特性会提供一种方法来阻止 IntelliTest 为可能的非终止进程发出测试用例或发出导致堆栈溢出的测试用例。

<a name="testemissionfilter"></a>
## <a name="testemissionfilter"></a>TestEmissionFilter

指示 IntelliTest 应发出的测试类型。 可能的值为：

* 全部  - 对所有内容（包括假设冲突）发出测试。
* FailuresAndIncreasedBranchHits  （默认）- 对所有唯一故障发出测试，且每当测试用例按 [TestEmissionBranchHits](#testemissionbranchhits) 的控制，增加覆盖率时发出测试。
* FailuresAndUniquePaths  - 对 IntelliTest 找到的所有故障以及导致唯一执行路径的每个测试输入发出测试。
* 故障  - 仅对故障发出测试。

<a name="testemissionbranchhits"></a>
## <a name="testemissionbranchhits"></a>TestEmissionBranchHits

根据当前 [TestEmissionFilter](#testemissionfilter) 设置，当 IntelliTest 涵盖之前程序中未涵盖的分支时发出新的测试用例。

TestEmissionBranchHits  设置确定 IntelliTest 是否应考虑完全涵盖某个分支，是测试涵盖一次，即 (**TestEmissionBranchHits = 1**)，还是两次，即 (**TestEmissionBranchHits = 2**)，依次类推。

TestEmissionBranchHits = 1  将产生非常小的测试套件，套件将涵盖 IntelliTest 可访问的所有分支。 具体而言，此测试套件还将涵盖它访问的所有基本块和语句。

此选项的默认值是 TestEmissionBranchHits = 2  ，这将生成更具表达意义的测试套件，也更适合检测将来的回归错误。

## <a name="got-feedback"></a>是否获得反馈？

在[开发人员社区](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)上发布想法和功能请求。
