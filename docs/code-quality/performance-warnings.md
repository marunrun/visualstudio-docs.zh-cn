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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 30acc1f38ea0d27a3a8245f586b3c41765330c50
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283393"
---
# <a name="performance-warnings"></a>性能警告
性能警告支持高性能库和应用程序。

## <a name="in-this-section"></a>本节内容

| 规则 | 说明 |
| - | - |
| [CA1800:避免进行不必要的强制转换](../code-quality/ca1800.md) | 重复强制转换会降低性能，特别是在精简的迭代语句中执行强制转换时。 |
| [CA1801:检查未使用的参数](../code-quality/ca1801.md) | 方法签名包含一个没有在方法体中使用的参数。 |
| [CA1802:在合适的位置使用文本](../code-quality/ca1802.md) | 字段在中声明为静态和只读（在中为 Shared 和 ReadOnly [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ），并使用编译时可的值进行初始化。 由于分配给目标字段的值是在编译时可的，因此将声明更改为 const （in in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ）字段，以便在编译时（而不是在运行时）计算值。 |
| [CA1804:移除未使用的局部变量](../code-quality/ca1804.md) | 未使用的局部变量和不必要的赋值会增加程序集的大小并降低性能。 |
| [CA1806:不要忽略方法结果](../code-quality/ca1806.md) | 创建新的对象，但从未使用过，或者创建并返回一个新字符串的方法未被使用，或者组件对象模型（COM）或 P/Invoke 方法返回从不使用的 HRESULT 或错误代码。 |
| [CA1809:避免过多的局部变量](../code-quality/ca1809.md) | 优化性能的常见方法是将值存储于处理器寄存器，而不是内存中，这称为“注册值”。  若要提高所有的局部变量都能注册的机会，应将局部变量的数目限制在 64 个以内。 |
| [CA1810:以内联方式初始化引用类型的静态字段](../code-quality/ca1810.md) | 当一个类型声明显式静态构造函数时，实时 (JIT) 编译器会向该类型的每个静态方法和实例构造函数中添加一项检查，以确保之前已调用该静态构造函数。 静态构造函数检查会降低性能。 |
| [CA1811:避免使用未调用的私有代码](../code-quality/ca1811.md) | 私有或内部（程序集级别）成员在程序集中没有调用方，它不是由公共语言运行时调用的，并且不是由委托调用的。 |
| [CA1812:避免未实例化的内部类](../code-quality/ca1812.md) | 程序集级别类型的实例不是由程序集中的代码创建的。 |
| [CA1813:避免使用非密封特性](../code-quality/ca1813.md) | .NET 提供了用于检索自定义特性的方法。 默认情况下，这些方法搜索特性继承层次结构。 通过密封特性，将无需搜索继承层次结构，且能够提高性能。 |
| [CA1814:与多维数组相比，首选使用交错数组](../code-quality/ca1814.md) | 交错数组是元素为数组的数组。 构成元素的数组可以是不同的大小，这可能会导致某些数据集的空间浪费更少。 |
| [CA1815:重写值类型上的 Equals 和相等运算符](../code-quality/ca1815.md) | 对于值类型，Equals 的继承的实现使用反射库，并比较所有字段的内容。 反射需要消耗大量计算资源，可能没有必要比较每一个字段是否相等。 如果希望用户对实例进行比较或排序，或者希望用户将实例用作哈希表键，则值类型应实现 Equals。 |
| [CA1816:正确调用 GC.SuppressFinalize](../code-quality/ca1816.md) | 作为 Dispose 实现的方法不调用 GC。Gc.suppressfinalize，或者不是 Dispose 的实现的方法会调用 GC。Gc.suppressfinalize 或方法调用 GC。Gc.suppressfinalize 并传递除此外的其他内容（Me in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ）。 |
| [CA1819:属性不应返回数组](../code-quality/ca1819.md) | 即使属性是只读的，由属性返回的数组仍不受写保护。 若要使数组不会被更改，属性必须返回数组的副本。 通常，用户不能理解调用这种属性的负面性能影响。 |
| [CA1820:使用字符串长度测试是否有空字符串](../code-quality/ca1820.md) | 使用 String.Length 属性或 String.IsNullOrEmpty 方法比较字符串要比使用 Equals 的速度快得多。 |
| [CA1821:移除空终结器](../code-quality/ca1821.md) | 应尽可能避免终结器，因为跟踪对象生存期会产生额外的性能系统开销。 空的终结器会产生额外的开销，而不会带来任何好处。 |
| [CA1822:将成员标记为 static](../code-quality/ca1822.md) | 可以将不访问实例数据或不调用实例方法的成员标记为 static（在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中为 Shared）。 在将这些方法标记为 static 之后，编译器将向这些成员发出非虚拟调用站点。 这会使性能敏感的代码的性能得到显著提高。 |
| [CA1823:避免未使用的私有字段](../code-quality/ca1823.md) | 检测到程序集内有似乎未访问过的私有字段。 |
| [CA1824:用 NeutralResourcesLanguageAttribute 标记程序集](../code-quality/ca1824.md) | NeutralResourcesLanguage 特性通知 ResourceManager 用于显示程序集的非特定区域性资源的语言。 这将改进所加载的第一个资源的查找性能，并缩小工作集。 |
| [CA1825:避免数组分配长度为零](../code-quality/ca1825.md) | 初始化长度为零的数组将导致不必要的内存分配。 相反，请通过调用来使用静态分配的空数组实例 <xref:System.Array.Empty%2A?displayProperty=nameWithType> 。 内存分配在此方法的所有调用之间共享。 |
| [CA1826:使用属性，而不是 Linq Enumerable 方法](../code-quality/ca1826.md) | <xref:System.Linq.Enumerable>LINQ 方法用于支持等效且更有效的属性的类型。 |
| [CA1827:如果可以使用 Any，请勿使用 Count/LongCount](../code-quality/ca1827.md) | <xref:System.Linq.Enumerable.Count%2A><xref:System.Linq.Enumerable.LongCount%2A>使用方法，其中 <xref:System.Linq.Enumerable.Any%2A> 方法会更有效。 |
| [CA1828:如果可以使用 AnyAsync，请勿使用 CountAsync/LongCountAsync](../code-quality/ca1828.md) | <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.CountAsync%2A><xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.LongCountAsync%2A>使用方法，其中 <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.AnyAsync%2A> 方法会更有效。 |
| [CA1829:使用 Length/Count 属性，而不是 Enumerable.Count 方法](../code-quality/ca1829.md) | <xref:System.Linq.Enumerable.Count%2A>LINQ 方法用于支持等效的、更有效的或属性的类型 `Length` `Count` 。 |
| [CA1831：适当时，使用 AsSpan 而不是字符串的基于范围的索引器](../code-quality/ca1831.md) | 对字符串使用范围索引器并将值隐式赋值给 ReadOnlySpan &lt; char &gt; 类型时， <xref:System.String.Substring%2A?#System_String_Substring_System_Int32_System_Int32_> 将使用方法而不是 <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> ，这将生成请求的字符串部分的副本。 |
| [CA1832：使用 AsSpan 或 AsMemory，而不是基于范围的索引器来获取数组的 ReadOnlySpan 或 ReadOnlyMemory 部分](../code-quality/ca1832.md) | 在数组上使用范围索引器并将值隐式赋值给 <xref:System.ReadOnlySpan%601> 或类型时 <xref:System.ReadOnlyMemory%601> ， <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> 将使用方法而不是 <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> ，这将生成数组的请求部分的副本。 |
| [CA1833：使用 AsSpan 或 AsMemory，而不是基于范围的索引器来获取数组的跨距或 Memory 部分](../code-quality/ca1833.md) | 在数组上使用范围索引器并将值隐式赋值给 <xref:System.Span%601> 或类型时 <xref:System.Memory%601> ， <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> 将使用方法而不是 <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> ，这将生成数组的请求部分的副本。 |
| [CA1835：首选 "ReadAsync" 和 "WriteAsync" 的基于 Memory' 的重载](../code-quality/ca1835.md) | "Stream" 有一个 "ReadAsync" 重载，该重载采用 "Memory &lt; byte &gt; " 作为第一个参数，而 "WriteAsync" 重载采用 "ReadOnlyMemory &lt; Byte &gt; " 作为第一个参数。 更愿意调用基于内存的重载，这些重载更有效。 |
