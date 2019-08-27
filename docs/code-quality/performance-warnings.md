---
title: 性能警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.performancerules
helpviewer_keywords:
- warnings, performance
- performance warnings
- performance, warnings
- managed code analysis warnings, performance warnings
ms.assetid: e014ac3a-02e6-46d9-942c-3491dd63782f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7dd2945ec12ac398f2887d20d3d0cb6156f4ed3c
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66745211"
---
# <a name="performance-warnings"></a>性能警告
性能警告支持高性能库和应用程序。

## <a name="in-this-section"></a>本节内容

| 规则 | 描述 |
| - | - |
| [CA1800： 避免进行不必要的强制转换](../code-quality/ca1800-do-not-cast-unnecessarily.md) | 重复强制转换会降低性能，特别是在精简的迭代语句中执行强制转换时。 |
| [CA1801:检查未使用的参数](../code-quality/ca1801-review-unused-parameters.md) | 方法签名包含一个没有在方法体中使用的参数。 |
| [CA1802:在适用处使用文本](../code-quality/ca1802-use-literals-where-appropriate.md) | 字段声明为静态和只读的 (Shared 和 ReadOnly 中的[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)])，并使用在编译时计算的值初始化。 因为分配给目标字段的值可在编译时，将声明更改为一个常量 (中的常量[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) 字段，以便在编译时而不是在运行时计算的值。 |
| [CA1804:删除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md) | 未使用的局部变量和不必要的赋值会增加程序集的大小并降低性能。 |
| [CA1806:不要忽略方法结果](../code-quality/ca1806-do-not-ignore-method-results.md) | 创建但从未使用过，新对象或调用的方法创建并返回一个新的字符串和永远不会使用新的字符串，或组件对象模型 (COM) 或 P/Invoke 方法返回一个从未使用过的 HRESULT 或错误代码。 |
| [CA1809:避免过多的局部变量](../code-quality/ca1809-avoid-excessive-locals.md) | 优化性能的常见方法是将值存储于处理器寄存器，而不是内存中，这称为“注册值”。  若要增加所有本地变量都是以内的机会，限制为 64 的本地变量的数目。 |
| [CA1810:引用类型的静态字段以内联方式初始化](../code-quality/ca1810-initialize-reference-type-static-fields-inline.md) | 当一个类型声明显式静态构造函数时，实时 (JIT) 编译器会向该类型的每个静态方法和实例构造函数中添加一项检查，以确保之前已调用该静态构造函数。 静态构造函数检查会降低性能。 |
| [CA1811:避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md) | 私有或内部 （程序集级别） 成员在程序集中没有调用方、 由公共语言运行时，不调用它和它不由委托调用。 |
| [CA1812:避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md) | 程序集级别类型的实例不是由程序集中的代码创建的。 |
| [CA1813:避免使用未密封的特性](../code-quality/ca1813-avoid-unsealed-attributes.md) | .NET 提供了用于检索自定义特性的方法。 默认情况下，这些方法搜索特性继承层次结构。 通过密封特性，将无需搜索继承层次结构，且能够提高性能。 |
| [CA1814： 与通过多维首选使用交错的数组](../code-quality/ca1814-prefer-jagged-arrays-over-multidimensional.md) | 交错数组是元素为数组的数组。 构成元素的数组可以是不同的大小，可能会导致某些数据集的较低浪费空间。 |
| [CA1815:替代值类型上的 Equals 和相等运算符](../code-quality/ca1815-override-equals-and-operator-equals-on-value-types.md) | 对于值类型，Equals 的继承的实现使用反射库，并比较所有字段的内容。 反射需要消耗大量计算资源，可能没有必要比较每一个字段是否相等。 如果希望用户对实例进行比较或排序，或者希望用户将实例用作哈希表键，则值类型应实现 Equals。 |
| [CA1816:调用 GC。SuppressFinalize 正确](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md) | 实现 Dispose 方法不会调用 GC。SuppressFinalize 或不是实现 Dispose 方法调用 GC。SuppressFinalize 或方法调用 GC。SuppressFinalize，并将传递其他名称 (我在[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)])。 |
| [CA1819:属性不应返回数组](../code-quality/ca1819-properties-should-not-return-arrays.md) | 属性返回的数组不写保护状态，即使该属性是只读的。 若要使数组不会被更改，属性必须返回数组的副本。 通常，用户不能理解调用这种属性的负面性能影响。 |
| [CA1820:测试有空字符串，使用字符串长度](../code-quality/ca1820-test-for-empty-strings-using-string-length.md) | 使用 String.Length 属性或 String.IsNullOrEmpty 方法比较字符串要比使用 Equals 的速度快得多。 |
| [CA1821：移除空终结器](../code-quality/ca1821-remove-empty-finalizers.md) | 应尽可能避免终结器，因为跟踪对象生存期会产生额外的性能系统开销。 空终结器会产生增系统开销，而无需任何权益。 |
| [CA1822:将成员标记为静态](../code-quality/ca1822-mark-members-as-static.md) | 可以将不访问实例数据或不调用实例方法的成员标记为 static（在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中为 Shared）。 在将这些方法标记为 static 之后，编译器将向这些成员发出非虚拟调用站点。 这会使性能敏感的代码的性能得到显著提高。 |
| [CA1823:避免未使用的私有字段](../code-quality/ca1823-avoid-unused-private-fields.md) | 检测到程序集内有似乎未访问过的私有字段。 |
| [CA1824:用 NeutralResourcesLanguageAttribute 标记程序集](../code-quality/ca1824-mark-assemblies-with-neutralresourceslanguageattribute.md) | NeutralResourcesLanguage 特性通知 ResourceManager 用于显示程序集的非特定区域性资源的语言。 这将改进所加载的第一个资源的查找性能，并缩小工作集。 |
