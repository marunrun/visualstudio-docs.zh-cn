---
title: 代码质量规则概述
ms.date: 08/27/2020
ms.topic: reference
f1_keywords:
- CA1000
- CA1001
- CA1002
- CA1003
- CA1005
- CA1008
- CA1010
- CA1012
- CS1014
- CA1016
- CA1017
- CA1018
- CA1019
- CA1021
- CA1024
- CA1027
- CA1028
- CA1029
- CA1030
- CA1031
- CA1032
- CA1033
- CA1034
- CA1036
- CA1040
- CA1041
- CA1043
- CA1044
- CA1045
- CA1046
- CA1047
- CA1050
- CA1051
- CA1052
- CA1053
- CA1054
- CA1055
- CA1056
- CA1058
- CA1060
- CA1061
- CA1062
- CA1063
- CA1064
- CA1065
- CA1066
- CA1067
- CA1068
- CA1069
- CA1070
- CA1200
- CA1303
- CA1304
- CA1305
- CA1307
- CA1308
- CA1309
- CA1310
- CA1401
- CA1417
- CA1501
- CA1502
- CA1505
- CA1506
- CA1507
- CA1508
- CA1509
- CA1700
- CA1707
- CA1708
- CA1710
- CA1711
- CA1712
- CA1713
- CA1714
- CA1715
- CA1716
- CA1717
- CA1720
- CA1721
- CA1724
- CA1725
- CA1801
- CA1802
- CA1805
- CA1806
- CA1810
- CA1812
- CA1813
- CA1814
- CA1815
- CA1816
- CA1819
- CA1820
- CA1821
- CA1822
- CA1823
- CA1824
- CA1825
- CA1826
- CA1827
- CA1828
- CA1829
- CA1830
- CA1831
- CA1832
- CA1833
- CA1834
- CA1835
- CA1836
- CA1837
- CA1838
- CA2000
- CA2002
- CA2007
- CA2008
- CA2009
- CA2011
- CA2012
- CA2013
- CA2014
- CA2015
- CA2016
- CA2100
- CA2101
- CA2109
- CA2119
- CA2153
- CA2200
- CA2201
- CA2207
- CA2208
- CA2211
- CA2213
- CA2214
- CA2215
- CA2216
- CA2217
- CA2219
- CA2225
- CA2226
- CA2227
- CA2229
- CA2231
- CA2234
- CA2235
- CA2237
- CA2241
- CA2242
- CA2243
- CA2245
- CA2246
- CA2247
- CA2248
- CA2249
- CA2300
- CA2301
- CA2302
- CA2305
- CA2310
- CA2311
- CA2312
- CA2315
- CA2321
- CA2322
- CA2326
- CA2327
- CA2328
- CA2329
- CA2330
- CA2350
- CA2351
- CA2352
- CA2353
- CA2354
- CA2355
- CA2356
- CA2361
- CA2362
- CA3001
- CA3002
- CA3003
- CA3004
- CA3005
- CA3006
- CA3007
- CA3008
- CA3009
- CA3010
- CA3011
- CA3012
- CA3061
- CA3075
- CA3076
- CA3077
- CA5347
- CA5350
- CA5351
- CA5359
- CA5360
- CA5361
- CA5362
- CA5363
- CA5364
- CA5365
- CA5366
- CA5367
- CA5368
- CA5369
- CA5370
- CA5371
- CA5372
- CA5373
- CA5374
- CA5375
- CA5376
- CA5377
- CA5378
- CA5379
- CA5380
- CA5381
- CA5382
- CA5383
- CA5384
- CA5385
- CA5386
- CA5387
- CA5388
- CA5389
- CA5390
- CA5391
- CA5392
- CA5393
- CA5394
- CA5395
- CA5397
- CA5398
- CA5399
- CA5400
- CA5401
- CA5402
- CA5403
- IL3000
- IL3001
ms.assetid: 5cb221f6-dc59-4abf-9bfa-adbd6f907f96
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 8e4b728fab6eb47501bb0d1bb752d22c0c29a8b4
ms.sourcegitcommit: 5caad925ca0b5d136416144a279e984836d8f28c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2020
ms.locfileid: "89509440"
---
# <a name="code-analysis-warnings-for-managed-code-by-checkid"></a>托管代码的代码分析警告（按 CheckId）

下表列出了托管代码的代码分析警告，按警告的 CheckId 标识符排列。

| CheckId | 警告 | 说明 |
|---------| - | - |
| CA1000 | [CA1000:不要在泛型类型中声明静态成员](../code-quality/ca1000.md) | 调用泛型类型的静态成员时，必须指定该类型的类型参数。 当调用不支持推理的泛型实例成员时，必须指定该成员的类型参数。 在上述两种情况下，用于指定类型自变量的语法不同，但很容易混淆。 |
| CA1001 | [CA1001:具有可释放字段的类型应该是可释放的](../code-quality/ca1001.md) | 一个类声明并实现 System.IDisposable 类型的实例字段，但该类不实现 IDisposable。 声明 IDisposable 字段的类间接拥有非托管资源，并且应该实现 IDisposable 接口。 |
| CA1002 | [CA1002:不要公开泛型列表](../code-quality/ca1002.md) | \<(T>) # A1) 的< (是为性能而不是继承而设计的泛型集合。 因此，List 不包含任何虚拟成员。 应改为公开针对继承设计的泛型集合。 |
| CA1003 | [CA1003:使用泛型事件处理程序实例](../code-quality/ca1003.md) |某个类型包含的委托返回 void，该委托的签名包含两个参数（第一个参数是对象，第二个参数是可以分配给 EventArgs 的类型），而且包含程序集针对的是 Microsoft .NET Framework 2.0。 |
| CA1005 | [CA1005:避免泛型类型的参数过多](../code-quality/ca1005.md) | 泛型类型包含的类型参数越多，越难以知道并记住每个类型参数各代表什么。 通常，使用一个类型参数（与在列表中一样 \<T> ），并且在具有两个类型参数的某些情况下，与在字典中一样 \<TKey, TValue> 。 但是，如果存在两个以上的类型参数，则大多数用户都会感到过于困难。 |
| CA1008 | [CA1008:枚举应具有零值](../code-quality/ca1008.md) | 像其他值类型一样，未初始化枚举的默认值为零。 无标志特性的枚举应通过使用零值来定义成员，这样默认值即为该枚举的有效值。 如果应用了 FlagsAttribute 特性的枚举定义值为零成员，则该成员的名称应为“None”，以指示枚举中尚未设置值。 |
| CA1010 | [CA1010:集合应实现泛型接口](../code-quality/ca1010.md) | 若要扩大集合的用途，应实现某个泛型集合接口。 然后，可以使用该集合来填充泛型集合类型。 |
| CA1012 | [CA1012:抽象类型不应具有构造函数](../code-quality/ca1012.md) | 抽象类型的构造函数只能由派生类型调用。 由于公共构造函数用于创建类型的实例，但无法为抽象类型创建实例，因此具有公共构造函数的抽象类在设计上是错误的。 |
| CA1014 | [CA1014:用 CLSCompliantAttribute 标记程序集](../code-quality/ca1014.md) | 公共语言规范 (CLS) 定义了程序集在跨编程语言使用时必须符合的命名限制、数据类型和规则。 好的设计要求所有程序集用 <xref:System.CLSCompliantAttribute> 显式指示 CLS 合规性。 如果程序集没有此特性，则该程序集即不合规。 |
| CA1016 | [CA1016:用 AssemblyVersionAttribute 标记程序集](../code-quality/ca1016.md) | .NET 使用版本号来唯一标识程序集，并绑定到强名称程序集中的类型。 版本号与版本和发行者策略一起使用。 默认情况下，仅使用用于生成应用程序的程序集版本运行应用程序。 |
| CA1017 | [CA1017:用 ComVisibleAttribute 标记程序集](../code-quality/ca1017.md) |ComVisibleAttribute 决定 COM 客户端如何访问托管代码。 合理的设计指出程序集将显式指示 COM 可见性。 可以设置整个程序集的 COM 可见性，然后重写各个类型和类型成员的 COM 可见性。 如果此特性不存在，则程序集的内容对 COM 客户端可见。 |
| CA1018 | [CA1018:用 AttributeUsageAttribute 标记特性](../code-quality/ca1018.md) | 当定义自定义特性时，用 AttributeUsageAttribute 标记该特性，以指示源代码中可以应用自定义特性的位置。 特性的含义和预定用法将决定它在代码中的有效位置。 |
| CA1019 | [CA1019:定义特性参数的访问器](../code-quality/ca1019.md) | 特性可以定义强制自变量，在对目标应用该特性时必须指定这些自变量。 这些实参也称为位置实参，因为它们将作为位置形参提供给特性构造函数。 对于每一个强制变量，特性还必须提供一个相应的只读属性，以便可以在执行时检索该变量的值。 特性还可以定义可选实参，可选实参也称为命名实参。 这些变量按名称提供给特性构造函数，并且必须具有相应的读/写属性。 |
| CA1021 | [CA1021:避免使用 out 参数](../code-quality/ca1021.md) | 通过引用（使用 out 或 ref）传递类型要求具有使用指针的经验，了解值类型和引用类型的不同之处，以及能处理具有多个返回值的方法。 另外，out 和 ref 参数之间的差异没有得到广泛了解。 |
| CA1024 | [CA1024:在适用处使用属性](../code-quality/ca1024.md) | 公共或受保护方法的名称以“Get”开头，没有采用任何参数或返回的值不是数组。 该方法可能很适于成为属性。 |
| CA1027 |[CA1027:用 FlagsAttribute 标记枚举](../code-quality/ca1027.md) | 枚举是一种值类型，它定义一组相关的已命名常数。 如果可以按照有意义的方式组合一个枚举的已命名常数，则对该枚举应用 FlagsAttribute。 |
| CA1028 | [CA1028:枚举存储应为 Int32](../code-quality/ca1028.md) | 枚举是一种值类型，它定义一组相关的已命名常数。 默认情况下，System.Int32 数据类型用于存储常量值。 尽管您可以更改此基础类型，然而对于大多数情况，既不需要，也不建议您这样做。 |
| CA1030 | [CA1030:在适用处使用事件](../code-quality/ca1030.md) |该规则检测名称通常用于事件的方法。 如果为响应明确定义的状态更改而调用一个方法，则应由事件处理程序调用该方法。 调用该方法的对象应引发事件而不是直接调用该方法。 |
| CA1031 | [CA1031:不要捕捉一般异常类型](../code-quality/ca1031.md) | 不应捕捉一般异常。 捕捉更具体的异常，或者在执行 catch 块中的最后一条语句时重新引发一般异常。 |
| CA1032 |[CA1032:实现标准异常构造函数](../code-quality/ca1032.md) | 如果不能提供完整的构造函数集，要正确处理异常将变得比较困难。 |
| CA1033 | [CA1033:接口方法应可由子类型调用](../code-quality/ca1033.md) | 未密封的外部可见类型提供了显式实现公共接口的方法，但没有提供具有相同名称的其他外部可见方法。 |
| CA1034 | [CA1034:嵌套类型不应是可见的](../code-quality/ca1034.md) | 嵌套类型是在另一个类型的范围中声明的类型。 嵌套类型用于封装包含类型的私有实现详细信息。 如果用于此用途，则嵌套类型不应是外部可见的。 |
| CA1036 | [CA1036:重写可比较类型中的方法](../code-quality/ca1036.md) |公共或受保护类型实现 System.IComparable 接口。 它不重写 Object.Equals，也不重载表示相等、不等、小于或大于的语言特定运算符。 |
| CA1040 |[CA1040:避免使用空接口](../code-quality/ca1040.md) | 接口定义提供某个行为或使用协定的成员。 接口所描述的功能可以被任何类型采用，而不管该类型出现在继承层次结构中的哪个位置。 类型通过实现接口的成员来实现接口。 空接口无法定义任何成员；因此，它无法定义可以实现的协定。 |
| CA1041 | [CA1041:提供 ObsoleteAttribute 消息](../code-quality/ca1041.md) | 用未指定其 ObsoleteAttribute.Message 属性的 System.ObsoleteAttribute 特性来标记类型或成员。 当编译用 ObsoleteAttribute 标记的类型或成员时，将显示该特性的 Message 属性。 这将为用户提供有关已过时的类型或成员的信息。 |
| CA1043 | [CA1043:将整型或字符串参数用于索引器](../code-quality/ca1043.md) | 索引器（即索引属性）应将整型或字符串类型用于索引。 这些类型一般用于为数据结构编制索引，并且提高库的可用性。 应仅限于在设计时无法指定特定整型或字符串类型的情况下使用 Object 类型。 |
| CA1044 | [CA1044:属性不应是只写的](../code-quality/ca1044.md) | 虽然可以接受且经常需要使用只读属性，但设计准则禁止使用只写属性。 这是因为允许用户设置值但又禁止该用户查看这个值不能提供任何安全性。 而且，如果没有读访问，将无法查看共享对象的状态，使其用处受到限制。 |
| CA1045 |[CA1045:不要通过引用来传递类型](../code-quality/ca1045.md) | 通过引用（使用 out 或 ref）传递类型要求具有以下能力：使用指针的经验，了解值类型和引用类型的不同之处，以及能处理具有多个返回值的方法。 为一般受众设计的库架构师不应指望用户使用 `out` 或 `ref` 参数。 |
| CA1046 | [CA1046:不要对引用类型重载相等运算符](../code-quality/ca1046.md) | 对于引用类型，相等运算符的默认实现几乎始终是正确的。 默认情况下，仅当两个引用指向同一对象时，它们才相等。 |
| CA1047 |[CA1047:不要在密封类型中声明受保护的成员](../code-quality/ca1047.md) | 类型声明受保护的成员，使继承类型可以访问或重写该成员。 按照定义，不能继承密封类型，这表示不能调用密封类型上的受保护方法。 |
| CA1050 | [CA1050:在命名空间中声明类型](../code-quality/ca1050.md) | 应在命名空间内声明类型以避免名称冲突，并作为一种在对象层次结构中组织相关类型的方式。 |
| CA1051 | [CA1051:不要声明可见实例字段](../code-quality/ca1051.md) | 字段的主要用途应是作为实现的详细信息。 字段应为 private 或 internal，并应通过使用属性公开这些字段。 |
| CA1052 | [CA1052:应密封静态容器类型](../code-quality/ca1052.md) | 公共或受保护类型仅包含静态成员，而且没有用 sealed（C# 参考）(NotInheritable) 修饰符声明该类型。 应使用 sealed 修饰符标记不希望被继承的类型，以免将其用作基类型。 |
| CA1053 |[CA1053:静态容器类型不应具有构造函数](../code-quality/ca1053.md) | 公共或嵌套公共类型只声明了静态成员，但具有公共或受保护的默认构造函数。 由于调用静态成员不需要类型的示例，因此没必要使用构造函数。 为安全起见，字符串重载应使用字符串自变量调用统一资源标识符 (URI) 重载。 |
| CA1054 | [CA1054:URI 参数不应为字符串](../code-quality/ca1054.md) | 如果某方法采用 URI 的字符串表示形式，则应提供采用 URI 类的实例的相应重载，该重载以安全的方式提供这些服务。 |
| CA1055 | [CA1055:URI 返回值不应是字符串](../code-quality/ca1055.md) | 此规则假定该方法返回 URI。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 System.Uri 类以一种安全的方式提供这些服务。 |
| CA1056 | [CA1056:URI 属性不应是字符串](../code-quality/ca1056.md) | 此规则假定属性表示统一资源标识符 (URI)。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 System.Uri 类以一种安全的方式提供这些服务。 |
| CA1058 | [CA1058:类型不应扩展某些基类型](../code-quality/ca1058.md) | 外部可见的类型扩展某些基类型。 请使用某个备选项。 |
| CA1060 | [CA1060：将 P/Invoke 移动到 NativeMethods 类](../code-quality/ca1060.md) | 平台调用方法（例如标以 System.Runtime.InteropServices.DllImportAttribute 特性的那些方法，或在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中使用 Declare 关键字定义的方法）可以访问非托管代码。 这些方法应属于 NativeMethods、SafeNativeMethods 或 UnsafeNativeMethods 类。 |
| CA1061 |[CA1061:不要隐藏基类方法](../code-quality/ca1061.md) | 如果派生方法的参数签名只是在类型方面有所不同，而且与基方法的参数签名中的对应类型相比，这些类型的派生方式更弱，则基类型中的方法由派生类型中的同名方法隐藏。 |
| CA1062 | [CA1062:验证公共方法的参数](../code-quality/ca1062.md) | 对于传递给外部可见方法的所有引用自变量，都应检查其是否为 null。 |
| CA1063 | [CA1063:正确实现 IDisposable](../code-quality/ca1063.md) | 所有的 IDisposable 类型都应当正确实现 Dispose 模式。 |
| CA1064 | [CA1064:异常应该是公共的](../code-quality/ca1064.md) | 内部异常仅在其自己的内部范围内可见。 当异常超出内部范围后，只能使用基异常来捕获该异常。 如果内部异常继承自 <xref:System.Exception> 、或， <xref:System.SystemException> <xref:System.ApplicationException> 外部代码将不会有足够的信息来了解如何处理该异常。 |
| CA1065 | [CA1065:不要在意外的位置引发异常](../code-quality/ca1065.md) | 不应引发异常的方法引发了异常。 |
| CA1066 | [CA1066：重写 Equals 时实现 IEquatable](../code-quality/ca1066.md) | 值类型重写 <xref:System.Object.Equals%2A> 方法，但不实现 <xref:System.IEquatable%601> 。 |
| CA1067 | [CA1067：实现 IEquatable 时重写 Equals](../code-quality/ca1067.md) | 类型实现 <xref:System.IEquatable%601> ，但不重写 <xref:System.Object.Equals%2A> 方法。 |
| CA1068 | [CA1068:CancellationToken 参数必须最后出现](../code-quality/ca1068.md) | 方法具有一个不是最后一个参数的 CancellationToken 参数。 |
| CA1069 | [CA1069:枚举不得具有重复值](../code-quality/ca1069.md) | 枚举具有多个显式分配相同常数值的成员。 |
| CA1070 | [CA1070:不要将事件字段声明为“虚拟”](../code-quality/ca1070.md) | [类似字段的事件](/dotnet/csharp/language-reference/language-specification/classes#field-like-events)被声明为 virtual。 |
| CA1200 | [CA1200:不要使用带前缀的 cref 标记](../code-quality/ca1200.md) | XML 文档标记中的 [cref](/dotnet/csharp/programming-guide/xmldoc/cref-attribute) 特性表示 "代码引用"。 它指定标记的内部文本是一个代码元素，例如类型、方法或属性。 避免使用 `cref` 带有前缀的标记，因为这会阻止编译器验证引用。 它还可防止 Visual Studio 集成开发环境 (IDE) 在重构期间查找和更新这些符号引用。 |
| CA1303 | [CA1303:请不要将文本作为本地化参数传递](../code-quality/ca1303.md) | 外部可见方法将字符串文本作为参数传递给 .NET 构造函数或方法，并且该字符串应可本地化。 |
| CA1304 | [CA1304:指定 CultureInfo](../code-quality/ca1304.md) | 某方法或构造函数调用的成员有一个接受 System.Globalization.CultureInfo 参数的重载，但该方法或构造函数没有调用接受 CultureInfo 参数的重载。 如果未提供 CultureInfo 或 System.IFormatProvider 对象，则重载成员提供的默认值可能不会在所有区域设置中产生您想要的效果。 |
| CA1305 | [CA1305:指定 IFormatProvider](../code-quality/ca1305.md) | 某方法或构造函数调用的一个或多个成员有接受 System.IFormatProvider 参数的重载，但该方法或构造函数没有调用接受 IFormatProvider 参数的重载。 如果未提供 System.Globalization.CultureInfo 或 IFormatProvider 对象，则重载成员提供的默认值可能不会在所有区域设置中产生您想要的效果。 |
| CA1307 | [CA1307:为了清晰起见，请指定 StringComparison](../code-quality/ca1307.md) | 字符串比较运算使用不设置 StringComparison 参数的方法重载。 |
| CA1308 |[CA1308:将字符串规范化为大写](../code-quality/ca1308.md) | 字符串应正常化为大写字母。 少量字符转换为小写字母后不能再转换回来。 |
| CA1309 | [CA1309:使用按顺序的 StringComparison](../code-quality/ca1309.md) | 非语义的字符串比较运算不会将 StringComparison 参数设置为 Ordinal 或 OrdinalIgnoreCase。 因此，通过将参数显式设置为 StringComparison.Ordinal 或 StringComparison.OrdinalIgnoreCase，通常可以提高代码的速度、正确性和可靠性。 |
| CA1310 | [CA1310：为了确保正确，请指定 StringComparison](../code-quality/ca1310.md) | 在默认情况下，字符串比较操作使用未设置 StringComparison 参数并使用特定于区域性的字符串比较的方法重载。 |
| CA1401 | [CA1401： P/Invoke 应不可见](../code-quality/ca1401.md) | 公共类型中的公共或受保护方法具有 System.Runtime.InteropServices.DllImportAttribute 特性（还在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中由 Declare 关键字实现）。 这些方法不能公开。 |
| CA1417 | [CA1417：不 `OutAttribute` 在 P/invoke 的字符串参数上使用](../code-quality/ca1417.md) | 如果字符串是暂存的字符串，则通过值传递的字符串参数与 `OutAttribute` 运行时的不稳定性。 |
| CA1501 | [CA1501:避免过度继承](../code-quality/ca1501.md) | 类型在继承层次结构中的深度超过四级。 深度嵌套的类型层次结构可能很难遵循、理解和维护。 |
| CA1502 | [CA1502:避免过度复杂](../code-quality/ca1502.md) | 此规则通过方法来测量线性独立的路径的数量，该数量是由条件分支的数量和复杂度决定的。 |
| CA1505 | [CA1505:避免使用无法维护的代码](../code-quality/ca1505.md) | 类型或方法具有较低的可维护性索引值。 如果可维护性指数较低，则表示类型或方法可能难以维护，最好重新进行设计。 |
| CA1506 | [CA1506:避免过度类耦合度](../code-quality/ca1506.md) | 此规则通过计算类型或方法包含的唯一类型引用的个数来衡量类耦合。 |
| CA1507 | [CA1507：使用 nameof 代替字符串](../code-quality/ca1507.md) | 字符串文本用作参数，可在其中 `nameof` 使用表达式。 |
| CA1508 | [CA1508：避免死条件代码](../code-quality/ca1508.md) | 方法具有始终计算为 `true` 或 `false` 在运行时的条件代码。 这会导致条件的分支中的代码停滞 `false` 。 |
| CA1509 | [CA1509：代码度量配置文件中的条目无效](../code-quality/ca1509.md) | 代码度量规则（如 [CA1501](ca1501.md)、 [CA1502](ca1502.md)、 [CA1505](ca1505.md) 和 [CA1506](ca1506.md)）提供了名为的配置文件， `CodeMetricsConfig.txt` 该文件具有无效条目。 |
| CA1700 | [CA1700:不要命名“Reserved”枚举值](../code-quality/ca1700.md) | 此规则假定当前不使用名称中包含“reserved”的枚举成员，而是将其作为一个占位符，以在将来的版本中重命名或移除它。 重命名或移除成员是一项重大更改。 |
| CA1707 | [CA1707:标识符不应包含下划线](../code-quality/ca1707.md) | 按照约定，标识符名称不包含下划线 (_) 字符。 该规则将检查命名空间、类型、成员和参数。 |
| CA1708 | [CA1708:标识符应以大小写之外的差别进行区分](../code-quality/ca1708.md) | 不能仅通过大小写区分命名空间、类型、成员和参数的标识符，因为针对公共语言运行时的语言不需要区分大小写。 |
| CA1710 | [CA1710:标识符应具有正确的后缀](../code-quality/ca1710.md) |按照约定，扩展某些基类型或实现某些接口的类型的名称，或者由这些类型派生的类型的名称应具有与相应基类型或接口关联的后缀。 |
| CA1711 | [CA1711:标识符应采用正确的后缀](../code-quality/ca1711.md) | 按照约定，只有扩展某些基类型或实现某些接口的类型的名称或者从这些类型派生的类型的名称，应该以特定的保留后缀结尾。 其他类型名称不应使用这些保留的后缀。 |
| CA1712 | [CA1712:不要将类型名用作枚举值的前缀](../code-quality/ca1712.md) | 枚举成员的名称不能使用类型名称作为前缀，因为类型信息将由开发工具提供。 |
| CA1713 | [CA1713:事件不应具有 before 或 after 前缀](../code-quality/ca1713.md) | 事件的名称以“Before”或“After”开头。 若要命名按特定顺序引发的相关事件，请使用现在时或过去时指示一系列操作中的相对位置。 |
| CA1714 | [CA1714:Flags 枚举应采用复数形式的名称](../code-quality/ca1714.md) | 公共枚举具有 System.FlagsAttribute 特性并且其名称不是以“s”结尾。 用 FlagsAttribute 标记的类型具有复数形式的名称，因为该特性指明可以指定多个值。 |
| CA1715 | [CA1715:标识符应具有正确的前缀](../code-quality/ca1715.md) | 外部可见的接口的名称不以大写的“I”开头。 外部可见的类型或方法上的泛型类型参数的名称不以大写的“T”开头。 |
| CA1716 | [CA1716:标识符不应与关键字冲突](../code-quality/ca1716.md) | 某个命名空间名称或类型名称与编程语言中的保留关键字相同。 命名空间和类型的标识符不应与针对公共语言运行时的语言所定义的关键字冲突。 |
| CA1717 | [CA1717:只有 FlagsAttribute 枚举应采用复数形式的名称](../code-quality/ca1717.md) | 命名约定规定，复数形式的枚举名称表示可以同时指定多个枚举值。 |
| CA1720 |[CA1720:标识符不应包含类型名称](../code-quality/ca1720.md) | 外部可见成员中的某个参数的名称包含一个数据类型名称，或者外部可见成员的名称包含一个语言特定的数据类型名称。 |
| CA1721 | [CA1721:属性名不应与 get 方法冲突](../code-quality/ca1721.md) |公共或受保护成员的名称以“Get”开头，且其余部分与公共或受保护属性的名称匹配。 “Get”方法和属性的名称应能够明确区分其功能上的差异。 |
| CA1724 | [CA1724:类型名不应与命名空间冲突](../code-quality/ca1724.md) | 类型名不应与 .NET 命名空间的名称相匹配。 与该规则冲突将使库的可用性下降。 |
| CA1725 | [CA1725:参数名应与基方法中的声明保持一致](../code-quality/ca1725.md) | 以一致的方式命名重写层次结构中的参数可以提高方法重写的可用性。 如果派生方法中的参数名与基声明中的名称不同，可能会导致无法区分出该方法是基方法的重写还是该方法的新重载。 |
| CA1801 | [CA1801:检查未使用的参数](../code-quality/ca1801.md) | 方法签名包含一个没有在方法体中使用的参数。 |
| CA1802 |[CA1802:在合适的位置使用文本](../code-quality/ca1802.md) |某个字段被声明为 static 和 read-only（在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中为 Shared 和 ReadOnly），并使用可在编译时计算的值初始化。 由于分配给目标字段的值是在编译时可的，因此将声明更改为) 字段中的 const (Const， [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 以便在编译时而不是在运行时计算该值。 |
| CA1805 | [CA1805：避免进行不必要的初始化](../code-quality/ca1805.md) | 在运行构造函数之前，.NET 运行时将引用类型的所有字段初始化为其默认值。 在大多数情况下，显式将字段初始化为其默认值是冗余的，这会增加维护成本，并可能会降低性能 (例如，通过增加) 的程序集大小。 |
| CA1806 | [CA1806:不要忽略方法结果](../code-quality/ca1806.md) | 创建一个新对象，但从不使用该对象；或者调用会创建并返回一个新字符串的方法，但从不使用这个新字符串；或者 COM 或 P/Invoke 方法返回一个从不使用的 HRESULT 或错误代码。 |
| CA1810 | [CA1810:以内联方式初始化引用类型的静态字段](../code-quality/ca1810.md) | 当一个类型声明显式静态构造函数时，实时 (JIT) 编译器会向该类型的每个静态方法和实例构造函数中添加一项检查，以确保之前已调用该静态构造函数。 静态构造函数检查会降低性能。 |
| CA1812 | [CA1812:避免未实例化的内部类](../code-quality/ca1812.md) | 程序集级别类型的实例不是由程序集中的代码创建的。 |
| CA1813 | [CA1813:避免使用非密封特性](../code-quality/ca1813.md) | .NET 提供了用于检索自定义特性的方法。 默认情况下，这些方法搜索特性继承层次结构。 通过密封特性，将无需搜索继承层次结构，且能够提高性能。 |
| CA1814 | [CA1814:与多维数组相比，首选使用交错数组](../code-quality/ca1814.md) | 交错数组是元素为数组的数组。 构成元素的数组可以是不同的大小，以减少某些数据集的浪费空间。 |
| CA1815 | [CA1815:重写值类型上的 Equals 和相等运算符](../code-quality/ca1815.md) | 对于值类型，Equals 的继承的实现使用反射库，并比较所有字段的内容。 反射需要消耗大量计算资源，可能没有必要比较每一个字段是否相等。 如果希望用户对实例进行比较或排序，或者希望用户将实例用作哈希表键，则值类型应实现 Equals。 |
| CA1816 | [CA1816:正确调用 GC.SuppressFinalize](../code-quality/ca1816.md) | 作为 Dispose 的实现的某个方法未调用 GC.SuppressFinalize；或者不是 Dispose 的实现的某个方法调用了 GC.SuppressFinalize；或者某个方法调用了 GC.SuppressFinalize 并传递 this（在 Visual Basic 中是 Me）以外的某个值。 |
| CA1819 | [CA1819:属性不应返回数组](../code-quality/ca1819.md) | 即使属性是只读的，该属性返回的数组也不是写保护的。 若要使数组不会被更改，属性必须返回数组的副本。 通常，用户不能理解调用这种属性的负面性能影响。 |
| CA1820 | [CA1820:使用字符串长度测试是否有空字符串](../code-quality/ca1820.md) | 使用 String.Length 属性或 String.IsNullOrEmpty 方法比较字符串要比使用 Equals 的速度快得多。 |
| CA1821 | [CA1821:移除空终结器](../code-quality/ca1821.md) | 应尽可能避免终结器，因为跟踪对象生存期会产生额外的性能系统开销。 空的终结器只会徒增系统开销，没有一点好处。 |
| CA1822 |[CA1822:将成员标记为 static](../code-quality/ca1822.md) | 可以将不访问实例数据或不调用实例方法的成员标记为 static（在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中为 Shared）。 在将这些方法标记为 static 之后，编译器将向这些成员发出非虚拟调用站点。 这会使性能敏感的代码的性能得到显著提高。 |
| CA1823 | [CA1823:避免未使用的私有字段](../code-quality/ca1823.md) | 检测到程序集内有似乎未访问过的私有字段。 |
| CA1824 |[CA1824:用 NeutralResourcesLanguageAttribute 标记程序集](../code-quality/ca1824.md) | NeutralResourcesLanguage 属性通知资源管理器，该语言用于显示程序集的非特定区域性的资源。 这将改进所加载的第一个资源的查找性能，并缩小工作集。 |
| CA1825 |[CA1825:避免数组分配长度为零](../code-quality/ca1825.md) | 初始化长度为零的数组将导致不必要的内存分配。 相反，请通过调用来使用静态分配的空数组实例 <xref:System.Array.Empty%2A?displayProperty=nameWithType> 。 内存分配在此方法的所有调用之间共享。 |
| CA1826 |[CA1826:使用属性，而不是 Linq Enumerable 方法](../code-quality/ca1826.md) | <xref:System.Linq.Enumerable> LINQ 方法用于支持等效且更有效的属性的类型。 |
| CA1827 |[CA1827:如果可以使用 Any，请勿使用 Count/LongCount](../code-quality/ca1827.md) | <xref:System.Linq.Enumerable.Count%2A><xref:System.Linq.Enumerable.LongCount%2A>使用方法，其中 <xref:System.Linq.Enumerable.Any%2A> 方法会更有效。 |
| CA1828 |[CA1828:如果可以使用 AnyAsync，请勿使用 CountAsync/LongCountAsync](../code-quality/ca1828.md) | <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.CountAsync%2A><xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.LongCountAsync%2A>使用方法，其中 <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.AnyAsync%2A> 方法会更有效。 |
| CA1829 |[CA1829:使用 Length/Count 属性，而不是 Enumerable.Count 方法](../code-quality/ca1829.md) | <xref:System.Linq.Enumerable.Count%2A> LINQ 方法用于支持等效的、更有效的或属性的类型 `Length` `Count` 。 |
| CA1830 |[CA1830:在 StringBuilder 上优先使用强类型“追加和插入”方法重载](../code-quality/ca1830.md) | <xref:System.Text.StringBuilder.Append%2A> 和 <xref:System.Text.StringBuilder.Insert%2A> 提供多种类型的重载 <xref:System.String> 。  如果可能，更倾向于使用 ToString ( # A1 和基于字符串的重载中的强类型重载。 |
| CA1831 |[CA1831:在合适的情况下，为字符串使用 AsSpan 而不是基于范围的索引器](../code-quality/ca1831.md) | 对字符串使用范围索引器并将值隐式赋值给 ReadOnlySpan &lt; char 类型时 &gt; ， <xref:System.String.Substring%2A?#System_String_Substring_System_Int32_System_Int32_> 将使用方法而不是 <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> ，这将生成请求的字符串部分的副本。 |
| CA1832 |[CA1832:使用 AsSpan 或 AsMemory 而不是基于范围的索引器来获取数组的 ReadOnlySpan 或 ReadOnlyMemory 部分](../code-quality/ca1832.md) | 在数组上使用范围索引器并将值隐式赋值给 <xref:System.ReadOnlySpan%601> 或类型时 <xref:System.ReadOnlyMemory%601> ， <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> 将使用方法而不是 <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> ，这将生成数组的请求部分的副本。 |
| CA1833 |[CA1833:使用 AsSpan 或 AsMemory 而不是基于范围的索引器来获取数组的 Span 或 Memory 部分](../code-quality/ca1833.md) | 在数组上使用范围索引器并将值隐式赋值给 <xref:System.Span%601> 或类型时 <xref:System.Memory%601> ， <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> 将使用方法而不是 <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> ，这将生成数组的请求部分的副本。 |
| CA1834 |[CA1834:对单字符字符串使用 StringBuilder.Append(char)](../code-quality/ca1834.md) | <xref:System.Text.StringBuilder> 具有一个 `Append` 采用 `char` 作为参数的重载。 `char`出于性能原因，更倾向于调用重载。 |
| CA1835 |[CA1835：首选 "ReadAsync" 和 "WriteAsync" 的基于 Memory' 的重载](../code-quality/ca1835.md) | "Stream" 有一个 "ReadAsync" 重载，该重载采用 "Memory &lt; byte &gt; " 作为第一个参数，而 "WriteAsync" 重载采用 "ReadOnlyMemory &lt; Byte &gt; " 作为第一个参数。 更愿意调用基于内存的重载，这些重载更有效。 |
| CA1836 |[CA1836：优先 `IsEmpty` `Count` 使用（如果可用）](../code-quality/ca1836.md) | 首选 `IsEmpty` 比、或更有效的属性， `Count` `Length` <xref:System.Linq.Enumerable.Count%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> <xref:System.Linq.Enumerable.LongCount%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> 以确定对象是否包含任何项。 |
| CA1837 | [CA1837：使用 `Environment.ProcessId` 而不是 `Process.GetCurrentProcess().Id`](../code-quality/ca1837.md) | `Environment.ProcessId` 比更简单、更快 `Process.GetCurrentProcess().Id` 。 |
| CA1838 | [CA1838：避免 `StringBuilder` P/invoke 参数](../code-quality/ca1838.md) | "StringBuilder" 的封送处理始终创建本机缓冲区副本，从而导致一个封送处理操作有多个分配。 |
| CA2000 | [CA2000:丢失范围之前释放对象](../code-quality/ca2000.md) | 由于可能发生异常事件，导致对象的终结器无法运行，因此，应显式释放对象，以避免对该对象的所有引用超出范围。 |
| CA2002 |[CA2002:不要锁定具有弱标识的对象](../code-quality/ca2002.md) |当可以跨应用程序域边界直接进行访问对象时，则认为该对象具有弱标识。 对于尝试获取对具有弱标识的对象的锁的线程，该线程可能会被其他应用程序域中持有对同一对象的锁的另一线程所阻止。 |
| CA2007 | [CA2007：不直接等待任务](ca2007.md) | 异步方法会[awaits](/dotnet/csharp/language-reference/keywords/await)直接等待 <xref:System.Threading.Tasks.Task> 。 当异步方法直接等待时 <xref:System.Threading.Tasks.Task> ，延续将在创建任务的同一线程中发生。 此行为在性能方面可能会很大，并且可能会在 UI 线程上导致死锁。 请考虑调用 <xref:System.Threading.Tasks.Task.ConfigureAwait(System.Boolean)?displayProperty=nameWithType> 以通知你的继续符。 |
| CA2008 | [CA2008：不要在未传递 TaskScheduler 的情况下创建任务](ca2008.md) | 任务创建或继续操作使用未指定参数的方法重载 <xref:System.Threading.Tasks.TaskScheduler> 。 |
| CA2009 | [CA2009：请勿对 ImmutableCollection 值调用 ToImmutableCollection](ca2009.md) | `ToImmutable` 不必要地对命名空间中的不可变集合调用方法 <xref:System.Collections.Immutable> 。 |
| CA2011 | [CA2011:请勿在其资源库中分配属性](ca2011.md) | 属性在其自身的 [set 访问器](/dotnet/csharp/programming-guide/classes-and-structs/using-properties#the-set-accessor)中被意外赋值。 |
| CA2012 | [CA2012:正确使用 ValueTask](ca2012.md) | 从成员调用返回的 ValueTasks 将直接等待。  多次尝试使用 ValueTask 或在已知完成前直接访问一个结果可能会导致异常或损坏。  忽略此类 ValueTask 可能表明出现功能 bug，并可能会降低性能。 |
| CA2013 | [CA2013:请勿将 ReferenceEquals 与值类型结合使用](ca2013.md) | 使用比较值时 <xref:System.Object.ReferenceEquals%2A?displayProperty=fullName> ，如果 objA 和 objB 是值类型，则在将其传递给方法之前将它们装箱 <xref:System.Object.ReferenceEquals%2A> 。 这意味着，即使 objA 和 objB 都表示值类型的同一个实例，该方法也会 <xref:System.Object.ReferenceEquals%2A> 返回 false。 |
| CA2014 | [CA2014：不要在循环中使用 stackalloc。](ca2014.md) | Stackalloc 分配的堆栈空间仅在当前方法的调用结束时释放。  在循环中使用此方法可能会导致无限堆栈增长，并最终产生堆栈溢出情况。 |
| CA2015 | [CA2015：不要为派生自 MemoryManager T 的类型定义终结器 &lt;&gt;](ca2015.md) | 将终结器添加到从派生的类型 <xref:System.Buffers.MemoryManager%601> 时，可能会允许在仍在使用时释放内存 <xref:System.Span%601> 。 |
| CA2016 | [CA2016：将 CancellationToken 参数转发到采用一个该参数的方法](ca2016.md) | 将 `CancellationToken` 参数转发到方法，这些方法采用一个来确保正确传播操作取消通知，或显式传递 `CancellationToken.None` 以指示有意不传播标记。 |
| CA2100 | [CA2100:检查 SQL 查询是否存在安全漏洞](../code-quality/ca2100.md) | 一个方法使用按该方法的字符串参数生成的字符串设置 System.Data.IDbCommand.CommandText 属性。 此规则假定字符串参数中包含用户输入。 基于用户输入生成的 SQL 命令字符串易于受到 SQL 注入式攻击。 |
| CA2101 |[CA2101：为 P/Invoke 字符串参数指定封送处理](../code-quality/ca2101.md) | 某平台调用成员允许部分受信任的调用方，具有一个字符串参数，并且不显式封送该字符串。 这可能导致潜在的安全漏洞。 |
| CA2109 | [CA2109:检查可见的事件处理程序](../code-quality/ca2109.md) | 检测到公共事件处理方法或受保护事件处理方法。 除非绝对必要，否则不应公开事件处理方法。 |
| CA2119 | [CA2119:密封满足私有接口的方法](../code-quality/ca2119.md) | 可继承的公共类型为内部（在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中为 Friend）接口提供可重写的方法实现。 若要修复与此规则的冲突，请禁止方法在程序集外重写。 |
| CA2153 |[CA2153：避免处理损坏状态异常](../code-quality/ca2153.md) | 损坏状态异常 (Cse) 指示进程中存在内存损坏。 如果攻击者可以将攻击放置到损坏的内存区域，则捕获它们（而非允许进程崩溃）可能导致安全漏洞。 |
| CA2200 | [CA2200:再次引发以保留堆栈详细信息](../code-quality/ca2200.md) | 再次引发某个异常，在 throw 语句中显式指定了该异常。 如果通过在 throw 语句中指定异常来重新引发该异常，则引发该异常的原始方法与当前方法之间的方法调用的列表将丢失。 |
| CA2201 | [CA2201:不要引发保留的异常类型](../code-quality/ca2201.md) | 这使得很难检测和调试原始错误。 |
| CA2207 | [CA2207:以内联方式初始化值类型的静态字段](../code-quality/ca2207.md) | 某值类型声明了显式静态构造函数。 要修复与该规则的冲突，请在声明它时初始化所有静态数据并移除静态构造函数。 |
| CA2208 |[CA2208:正确实例化参数异常](../code-quality/ca2208.md) | 调用了异常类型 ArgumentException 或其派生类型的默认（无参数）构造函数，或者向异常类型 ArgumentException 或其派生类型的参数化构造函数传递了错误的字符串参数。 |
| CA2211 |[CA2211:非常量字段不应是可见的](../code-quality/ca2211.md) | 不是常数也不是只读字段的静态字段不是线程安全的。 必须严格控制对这类字段的访问，并需要高级编程技术来同步对类对象的访问。 |
| CA2213 | [CA2213:应释放可释放的字段](../code-quality/ca2213.md) | 实现 System.IDisposable 的类型声明了同样实现 IDisposable 的类型的字段。 字段的 Dispose 方法不由声明类型的 Dispose 方法调用。 |
| CA2214 | [CA2214:不要在构造函数中调用可重写的方法](../code-quality/ca2214.md) | 构造函数调用虚方法时，可能尚未执行调用该方法的实例的构造函数。 |
| CA2215 | [CA2215:Dispose 方法应调用基类释放](../code-quality/ca2215.md) | 如果类型继承自可释放类型，则必须从它自己的 Dispose 方法中调用基类型的 Dispose 方法。 |
| CA2216 |[CA2216:可释放类型应声明终结器](../code-quality/ca2216.md) | 实现 System.IDisposable 并包含建议使用非托管资源的字段的类型未实现 Object.Finalize 所描述的终结器。 |
| CA2217 | [CA2217:不要使用 FlagsAttribute 标记枚举](../code-quality/ca2217.md) |外部可见的枚举使用 FlagsAttribute 标记，并且它包含的一个或多个值不是 2 的幂或不是为该枚举定义的其他值的组合。 |
| CA2219 | [CA2219:在异常子句中不引发异常](../code-quality/ca2219.md) | 如果在 finally 或 fault 子句中引发异常，新异常将隐藏活动异常。 当在 filter 子句中引发异常时，运行时会在不提示的情况下捕捉异常。 这使得很难检测和调试原始错误。 |
| CA2225 | [CA2225:运算符重载具有命名的备用项](../code-quality/ca2225.md) |检测到运算符重载，但未找到预期的指定备用方法。 命名的备用成员提供了对与运算符相同的功能的访问，它提供给开发人员，在用不支持重载运算符的语言进行编程时使用。 |
| CA2226 | [CA2226:运算符应有对称重载](../code-quality/ca2226.md) | 某个类型实现了相等运算符或不等运算符，却未实现相反运算符。 |
| CA2227 |[CA2227:集合属性应为只读](../code-quality/ca2227.md) |使用可写的集合属性，用户可以将该集合替换为不同的集合。 只读属性禁止替换该集合，但仍允许设置单个成员。 |
| CA2229 | [CA2229:实现序列化构造函数](../code-quality/ca2229.md) | 要修复与该规则的冲突，请实现序列化构造函数。 对于密封类，请使构造函数成为私有；否则，请使构造函数成为受保护。 |
| CA2231 | [CA2231:重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231.md) | 值类型重写 Object.Equals，但未实现相等运算符。 |
| CA2234 | [CA2234:传递 System.Uri 对象，而不传递字符串](../code-quality/ca2234.md) | 调用了带有一个字符串参数的方法，该参数的名称中包含“uri”、“URI”、“urn”、“URN”、“url”或“URL”。 此方法的声明类型包含具有 System.Uri 参数的对应方法重载。 |
| CA2235 | [CA2235:标记所有不可序列化的字段](../code-quality/ca2235.md) | 在可以序列化的类型中声明了类型不可序列化的实例字段。 |
| CA2237 | [CA2237:用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237.md) | 若要被公共语言运行时识别为可序列化，类型必须用 SerializableAttribute 特性标记，即使该类型通过实现 ISerializable 接口使用了自定义的序列化例程也是如此。 |
| CA2241 | [CA2241:为格式化方法提供正确的参数](../code-quality/ca2241.md) | 传递给 System.String.Format 的 format 自变量不包含对应于每个对象自变量的格式项，反之亦然。 |
| CA2242 |[CA2242:正确测试 NaN](../code-quality/ca2242.md) | 此表达式对照 Single.Nan 或 Double.Nan 测试某个值。 使用 Single.IsNan(Single) 或 Double.IsNan(Double) 测试该值。 |
| CA2243 |[CA2243:特性字符串文本应正确分析](../code-quality/ca2243.md) | 特性的字符串文本参数不能正确解析为 URL、GUID 或版本。 |
| CA2244 | [CA2244:不要复制已索引的元素初始值设定项](../code-quality/ca2244.md) | 对象初始值设定项具有多个具有相同的常量索引的索引元素初始值设定项。 除最后一个初始值设定项之外的所有都是冗余的。 |
| CA2245 | [CA2245:请勿将属性分配给其自身](../code-quality/ca2245.md) | 属性意外分配给自身。 |
| CA2246 | [CA2246:请勿在同一语句中分配符号及其成员](../code-quality/ca2246.md) | 不建议在同一语句中分配符号及其成员（即，字段或属性）。 如果成员访问权限打算在赋值前使用符号的旧值，或者在此语句的赋值中使用新值，则不清楚。 |
| CA2247 | [CA2247：传递到 TaskCompletionSource 构造函数的参数应为 TaskCreationOptions 枚举，而不是 System.threading.tasks.taskcontinuationoptions 枚举。](../code-quality/ca2247.md) | TaskCompletionSource 具有采用 TaskCreationOptions 的构造函数，这些构造函数控制基础任务，以及采用任务中存储的对象状态的构造函数。  意外传递 System.threading.tasks.taskcontinuationoptions 而不是 TaskCreationOptions 将导致调用将选项视为状态。 |
| CA2248 | [CA2248:向 Enum.HasFlag 提供正确的 enum 参数](../code-quality/ca2248.md) | 作为参数传递给方法调用的枚举类型 `HasFlag` 不同于调用枚举类型。 |
| CA2249 | [CA2249：请考虑使用 String.Contains 而不是 String.IndexOf](../code-quality/ca2249.md) | 对结果的调用 `string.IndexOf` （其中，用于检查是否存在子字符串）可以替换为 `string.Contains` 。 |
| CA2300 | [CA2300：请勿使用不安全的反序列化程序 BinaryFormatte](../code-quality/ca2300.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2301 | [CA2301：在未先设置 BinaryFormatter.Binder 的情况下，请不要调用 BinaryFormatter.Deserialize](../code-quality/ca2301.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2302 | [CA2302：在调用 BinaryFormatter.Deserialize 之前，确保设置 BinaryFormatter.Binder](../code-quality/ca2302.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2305 | [CA2305：请勿使用不安全的反序列化程序 LosFormatter](../code-quality/ca2305.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2310 | [CA2310：请勿使用不安全的反序列化程序 NetDataContractSerializer](../code-quality/ca2310.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2311 | [CA2311：在未先设置 NetDataContractSerializer.Binder 的情况下，请不要反序列化](../code-quality/ca2311.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2312 | [CA2312：确保在反序列化之前设置 NetDataContractSerializer.Binder](../code-quality/ca2312.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2315 | [CA2315：请勿使用不安全的反序列化程序 ObjectStateFormatter](../code-quality/ca2315.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2321 | [CA2321：请勿使用 SimpleTypeResolver 对 JavaScriptSerializer 进行反序列化](../code-quality/ca2321.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2322 | [CA2322：确保在反序列化之前没有使用 SimpleTypeResolver 初始化 JavaScriptSerializer](../code-quality/ca2322.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2326 | [CA2326：请勿使用 None 以外的 TypeNameHandling 值](../code-quality/ca2326.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2327 | [CA2327：不要使用不安全的 JsonSerializerSettings](../code-quality/ca2327.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2328 | [CA2328：确保 JsonSerializerSettings 是安全的](../code-quality/ca2328.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2329 | [CA2329：不要使用不安全的配置反序列化 JsonSerializer](../code-quality/ca2329.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2330 | [CA2330：在反序列化时确保 JsonSerializer 具有安全配置](../code-quality/ca2330.md) | 反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。 |
| CA2350 | [CA2350:确保 DataTable.ReadXml() 的输入受信任](ca2350.md) | <xref:System.Data.DataTable>使用不受信任的输入反序列化时，攻击者可以创建恶意输入来执行拒绝服务攻击。 可能存在未知的远程代码执行漏洞。 |
| CA2351 | [CA2351:确保 DataSet.ReadXml() 的输入受信任](ca2351.md) | <xref:System.Data.DataSet>使用不受信任的输入反序列化时，攻击者可以创建恶意输入来执行拒绝服务攻击。 可能存在未知的远程代码执行漏洞。 |
| CA2352 | [CA2352:可序列化类型中的不安全 DataSet 或 DataTable 容易受到远程代码执行攻击](ca2352.md) | 标记为的类或结构 <xref:System.SerializableAttribute> 包含 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 字段或属性，但不具有 <xref:System.CodeDom.Compiler.GeneratedCodeAttribute> 。 |
| CA2353 | [CA2353:可序列化类型中的不安全 DataSet 或 DataTable](ca2353.md) | 用 XML 序列化特性或数据协定特性标记的类或结构包含 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 字段或属性。 |
| CA2354 | [CA2354:反序列化对象图中的不安全 DataSet 或 DataTable 可能容易受到远程代码执行攻击](ca2354.md) | 使用序列化进行反序列化 <xref:System.Runtime.Serialization.IFormatter?displayProperty=nameWithType> ，强制转换类型的对象图可以包括 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 。 |
| CA2355 | [CA2355:反序列化对象图中的不安全 DataSet 或 DataTable](ca2355.md) | 当强制转换或指定类型的对象图可以包含或时进行反序列化 <xref:System.Data.DataSet> <xref:System.Data.DataTable> 。 |
| CA2356 | [CA2356： web 反序列化对象图中的不安全数据集或 DataTable](ca2356.md) | 具有或的方法 <xref:System.Web.Services.WebMethodAttribute?displayProperty=nameWithType> <xref:System.ServiceModel.OperationContractAttribute?displayProperty=nameWithType> 具有可引用或的参数 <xref:System.Data.DataSet> <xref:System.Data.DataTable> 。 |
| CA2361 | [CA2361：请确保包含 DataSet.ReadXml() 的自动生成的类没有与不受信任的数据一起使用](ca2361.md) | <xref:System.Data.DataSet>使用不受信任的输入反序列化时，攻击者可以创建恶意输入来执行拒绝服务攻击。 可能存在未知的远程代码执行漏洞。 |
| CA2362 | [CA2362：自动生成的可序列化类型中不安全的数据集或数据表易受远程代码执行攻击](ca2362.md) | 当反序列化的不受信任的输入 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 并且反序列化的对象图包含 <xref:System.Data.DataSet> 或时 <xref:System.Data.DataTable> ，攻击者可以创建恶意有效负载来执行远程代码执行攻击。 |
| CA3001 | [CA3001：查看 SQL 注入漏洞的代码](../code-quality/ca3001.md) | 使用不受信任的输入和 SQL 命令时，请注意 SQL 注入攻击。 SQL 注入攻击可以执行恶意的 SQL 命令，从而降低应用程序的安全性和完整性。 |
| CA3002 | [CA3002：查看 XSS 漏洞的代码](../code-quality/ca3002.md) | 处理 web 请求中的不受信任输入时，请注意跨站点脚本 (XSS) 攻击。 XSS 攻击会将不受信任的输入注入原始 HTML 输出，使攻击者可以执行恶意脚本或恶意修改网页中的内容。 |
| CA3003 | [CA3003:查看文件路径注入漏洞的代码](../code-quality/ca3003.md) | 当处理 web 请求中的不受信任输入时，请注意在指定文件路径时使用用户控制输入。 |
| CA3004 | [CA3004：查看信息泄露漏洞的代码](../code-quality/ca3004.md) | 泄露异常信息可让攻击者深入了解应用程序的内部机制，从而帮助攻击者找到其他漏洞来利用这些漏洞。 |
| CA3006 | [CA3006：查看进程命令注入漏洞的代码](../code-quality/ca3006.md) | 使用不受信任的输入时，请注意命令注入攻击。 命令注入攻击可以在基础操作系统上执行恶意命令，从而危及服务器的安全和完整性。 |
| CA3007 | [CA3007：查看公开重定向漏洞的代码](../code-quality/ca3007.md) | 使用不受信任的输入时，请注意开放重定向漏洞。 攻击者可以利用开放的重定向漏洞来使用您的网站来获得合法 URL 的外观，但将不受信任的访问者重定向到仿冒网站或其他恶意网页。 |
| CA3008 | [CA3008：查看 XPath 注入漏洞的代码](../code-quality/ca3008.md) | 使用不受信任的输入时，请注意 XPath 注入式攻击。 使用不受信任输入构造 XPath 查询时，攻击者可能会恶意地操作查询以返回意外的结果，并可能会泄漏所查询的 XML 的内容。 |
| CA3009 | [CA3009：查看 XML 注入漏洞的代码](../code-quality/ca3009.md) | 使用不受信任的输入时，请注意 XML 注入攻击。 |
| CA3010 | [CA3010：查看 XAML 注入漏洞的代码](../code-quality/ca3010.md) | 使用不受信任的输入时，请注意 XAML 注入攻击。 XAML 是一种直接表示对象实例化和执行的标记语言。 这意味着在 XAML 中创建的元素可以与系统资源交互 (例如，网络访问和文件系统 IO) 。 |
| CA3011 | [CA3011：查看 DLL 注入漏洞的代码](../code-quality/ca3011.md) | 使用不受信任的输入时，请注意加载不受信任的代码。 如果你的 web 应用程序加载不受信任的代码，攻击者可能能够将恶意 Dll 注入到你的进程中并执行恶意代码。 |
| CA3012 | [CA3012：查看正则表达式注入漏洞的代码](../code-quality/ca3012.md) | 使用不受信任的输入时，请注意 regex 注入式攻击。 攻击者可以使用 regex 注入来恶意地修改正则表达式，以使 regex 与意外结果匹配，或使 regex 消耗过多的 CPU，导致拒绝服务攻击。 |
| CA3061 | [CA3061：请勿按 URL 添加架构](../code-quality/ca3061.md) | 不要使用 Add 方法的 unsafe 重载，因为这可能会导致危险的外部引用。 |
| CA3075 | [CA3075:不安全的 DTD 处理](../code-quality/ca3075.md) | 如果使用不安全的 DTDProcessing 实例或引用外部实体源，分析器可能会接受不受信任的输入并将敏感信息泄露给攻击者。 |
| CA3076 | [CA3076:不安全的 XSLT 脚本执行](../code-quality/ca3076.md) | 如果 (XSLT) 在 .NET 应用程序不安全地中执行可扩展样式表语言转换，则处理器可能会解析可能向攻击者泄露敏感信息的不受信任的 URI 引用，从而导致拒绝服务和跨站点攻击。 |
| CA3077 | [CA3077:API 设计、XML 文档和 XML 文本读取器中的不安全处理](../code-quality/ca3077.md) | 当设计派生自 XMLDocument 和 XMLTextReader 的 API 时，请注意 DtdProcessing。 当引用或解析外部实体源或设置 XML 中的不安全值时，使用不安全的 DTDProcessing 实例可能会导致信息泄露。 |
| CA3147 | [CA3147:使用 ValidateAntiForgeryToken 标记谓词处理程序](../code-quality/ca3147.md) | 设计 ASP.NET MVC 控制器时，请注意跨站点请求伪造攻击。 跨站点请求伪造攻击可以将经过身份验证的用户的恶意请求发送到 ASP.NET MVC 控制器。 |
| CA5350 | [CA5350:请勿使用弱加密算法](../code-quality/ca5350.md) | 出于多种原因，现今使用弱加密算法和哈希函数，但不应使用它们来保证保密性或它们所保护的数据的完整性。 当此规则在代码中找到 TripleDES、SHA1、或 RIPEMD160 算法时，此规则将触发。|
| CA5351 | [CA5351 不使用损坏的加密算法](../code-quality/ca5351.md) | 损坏的加密算法不安全，强烈建议不要使用。 当此规则在代码中找到 MD5 哈希算法，或者 DES 或 RC2 加密算法时，此规则将触发。 |
| CA5358 | [CA5358：请勿使用不安全的密码模式](../code-quality/ca5358.md) | 请勿使用不安全的密码模式 |
| CA5359 | [CA5359 不禁用证书验证](../code-quality/ca5359.md) | 证书可以帮助验证服务器的身份。 客户端应验证服务器证书，以确保将请求发送到目标服务器。 如果 Servicepointmanager.servercertificatevalidationcallback 始终返回 `true` ，则任何证书将通过验证。 |
| CA5360 | [CA5360 不调用反序列化中的危险方法](../code-quality/ca5360.md) | 不受信任的反序列化是指使用不受信任的数据来滥用应用程序逻辑的漏洞，导致拒绝服务 (DoS) 攻击，甚至在反序列化时执行任意代码。 当应用程序对其控制下的不受信任的数据进行反序列化时，恶意用户经常会滥用这些反序列化功能。 具体而言，就是在反序列化过程中调用危险方法。 成功的反反序列化攻击可能会允许攻击者发起攻击，如 DoS 攻击、身份验证绕过和远程代码执行。 |
| CA5361 | [CA5361：不禁用 SChannel 使用强加密](../code-quality/ca5361.md) | 设置 `Switch.System.Net.DontEnableSchUseStrongCrypto` 为 `true` 受损传出传输层安全性 (TLS) 连接中使用的加密。 较弱的加密可能会危及应用程序与服务器之间通信的机密性，使攻击者更容易窃听敏感数据。 |
| CA5362 | [反序列化对象图中的 CA5362 潜在引用循环](../code-quality/ca5362.md) | 如果反序列化不受信任的数据，则处理反序列化对象图的任何代码都需要处理引用循环，而不会进入无限循环。 这包括作为反序列化回调一部分的代码和在反序列化完成后处理对象图的代码。 否则，攻击者可能会对包含引用周期的恶意数据执行拒绝服务攻击。 |
| CA5363 | [CA5363：请勿禁用请求验证](../code-quality/ca5363.md) | 请求验证是 ASP.NET 中的一项功能，用于检查 HTTP 请求并确定这些请求是否包含可能导致注入攻击（包括跨站点脚本）的潜在危险内容。 |
| CA5364 | [CA5364：不使用已弃用的安全协议](../code-quality/ca5364.md) | 传输层安全 (TLS) 保护计算机之间的通信，最常见的是通过超文本传输协议安全 (HTTPS) 。 较早的 TLS 协议版本不如 TLS 1.2 和 TLS 1.3 安全，更有可能出现新的漏洞。 避免旧协议版本来最大程度地降低风险。 |
| CA5365 | [CA5365 不禁用 HTTP 头检查](../code-quality/ca5365.md) | HTTP 标头检查启用在响应标头中找到的回车符和换行符（\r 和 \n）的编码。 这种编码有助于避免注入攻击，攻击者利用该应用程序回显了标头中包含的不受信任的数据。 |
| CA5366 | [CA5366 使用 XmlReader 进行数据集读取 XML](../code-quality/ca5366.md) | 使用 <xref:System.Data.DataSet> 读取包含不受信任数据的 XML 可能会加载危险的外部引用，应使用 <xref:System.Xml.XmlReader> 具有安全解析程序或禁用 DTD 处理的进行限制。 |
| CA5367 | [CA5367 不序列化包含指针字段的类型](../code-quality/ca5367.md) | 此规则检查是否存在具有指针字段或属性的可序列化类。 无法序列化的成员可以是指针，如使用标记的静态成员或字段 <xref:System.NonSerializedAttribute> 。 |
| CA5368 | [CA5368 为派生自 Page 的类设置 ViewStateUserKey](../code-quality/ca5368.md) | 设置 <xref:System.Web.UI.Page.ViewStateUserKey> 属性可帮助您阻止对应用程序的攻击，方法是允许您为个别用户分配视图状态变量的标识符，使攻击者无法使用该变量生成攻击。 否则，会出现跨站点请求伪造的漏洞。 |
| CA5369 | [CA5369：将 XmlReader 用于反序列化](../code-quality/ca5369.md) | 处理不受信任的 DTD 和 XML 架构可能会启用加载危险的外部引用，这应通过使用具有安全解析程序的 XmlReader 或禁用 DTD 和 XML 内联架构处理来限制。 |
| CA5370 | [CA5370：将 XmlReader 用于验证读取器](../code-quality/ca5370.md) | 处理不受信任的 DTD 和 XML 架构可能会启用加载危险的外部引用。 可以通过将 XmlReader 与安全解析程序结合使用，或者禁用 DTD 和 XML 内联架构处理来限制这种危险加载。 |
| CA5371 | [CA5371：将 XmlReader 用于架构读取](../code-quality/ca5371.md) | 处理不受信任的 DTD 和 XML 架构可能会启用加载危险的外部引用。 将 XmlReader 用于安全解析程序或 DTD 和 XML 内联架构处理将会限制这种情况。 |
| CA5372 | [CA5372：将 XmlReader 用于 XPathDocument](../code-quality/ca5372.md) | 处理来自不受信任数据的 XML 可能会加载危险的外部引用，这可以通过使用具有安全解析程序的 XmlReader 或禁用 DTD 处理来限制。 |
| CA5373 | [CA5373：请勿使用已过时的密钥派生功能](../code-quality/ca5373.md) | 此规则检测弱密钥派生方法和的调用 <xref:System.Security.Cryptography.PasswordDeriveBytes?displayProperty=fullName> `Rfc2898DeriveBytes.CryptDeriveKey` 。 <xref:System.Security.Cryptography.PasswordDeriveBytes?displayProperty=fullName> 使用弱算法 PBKDF1。 |
| CA5374 | [CA5374 不使用 XslTransform](../code-quality/ca5374.md) | 此规则检查 <xref:System.Xml.Xsl.XslTransform?displayProperty=nameWithType> 是否在代码中实例化。 <xref:System.Xml.Xsl.XslTransform?displayProperty=nameWithType> 现已过时，不应使用。 |
| CA5375 | [CA5375 不使用帐户共享访问签名](../code-quality/ca5375.md) | 帐户 SAS 可委派对 blob 容器、表、队列以及服务 SAS 不允许的文件共享上的读取、写入和删除操作的访问权限。 但是，它不支持容器级别的策略，并且具有较低的灵活性和对所授予权限的控制权限。 一旦恶意用户获得，您的存储帐户就会容易泄露。 |
| CA5376 | [CA5376 使用 SharedAccessProtocol HttpsOnly](../code-quality/ca5376.md) | SAS 是不能以纯文本形式在 HTTP 上传输的敏感数据。 |
| CA5377 | [CA5377 使用容器级别访问策略](../code-quality/ca5377.md) | 容器级别的访问策略可以随时修改或撤消。 它提供了更大的灵活性并控制授予的权限。 |
| CA5378 | [CA5378：不禁用 ServicePointManagerSecurityProtocols](../code-quality/ca5378.md) | 设置 `Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols` 以 `true` 限制 Windows Communication FRAMEWORK (WCF) 传输层安全 (tls) 与使用 tls 1.0 的连接。 TLS 版本将不推荐使用。 |
| CA5379 | [CA5379 不使用弱密钥派生函数算法](../code-quality/ca5379.md) | <xref:System.Security.Cryptography.Rfc2898DeriveBytes>类默认使用 <xref:System.Security.Cryptography.HashAlgorithmName.SHA1> 算法。 应指定要在具有 <xref:System.Security.Cryptography.HashAlgorithmName.SHA256> 或更高版本的构造函数的某些重载中使用的哈希算法。 请注意， <xref:System.Security.Cryptography.Rfc2898DeriveBytes.HashAlgorithm> 属性仅具有 `get` 访问器，没有 `overriden` 修饰符。 |
| CA5380 | [CA5380：请勿将证书添加到根存储中](../code-quality/ca5380.md) | 此规则检测将证书添加到 "受信任的根证书颁发机构" 证书存储中的代码。 默认情况下，"受信任的根证书颁发机构" 证书存储区配置为满足 Microsoft 根证书计划要求的一组公共 Ca。 |
| CA5381 | [CA5381：请确保证书未添加到根存储中](../code-quality/ca5381.md) | 此规则检测可能会将证书添加到 "受信任的根证书颁发机构" 证书存储中的代码。 默认情况下，"受信任的根证书颁发机构" 证书存储区配置了一组公共证书颁发机构 (Ca) 满足 Microsoft 根证书计划的要求。 |
| CA5382 | [CA5382 在 ASP.NET Core 中使用安全 cookie](../code-quality/ca5382.md) | 通过 HTTPS 提供的应用程序必须使用安全 cookie，这向浏览器指示该 cookie 只应使用安全套接字层 (SSL) 传输。 |
| CA5383 | [CA5383 确保在 ASP.NET Core 中使用安全 cookie](../code-quality/ca5383.md) | 通过 HTTPS 提供的应用程序必须使用安全 cookie，这向浏览器指示该 cookie 只应使用安全套接字层 (SSL) 传输。 |
| CA5384 | [CA5384 (DSA) 使用数字签名算法 ](../code-quality/ca5384.md) | DSA 是弱非对称加密算法。 |
| CA5385 | [CA5385 使用 Rivest – Rivest-shamir-adleman – Rivest-shamir-adleman (RSA) 具有足够密钥大小的算法](../code-quality/ca5385.md) | 小于2048位的 RSA 密钥更容易受到暴力破解攻击。 |
| CA5386 | [CA5386：避免对 SecurityProtocolType 值进行硬编码](../code-quality/ca5386.md) | 传输层安全 (TLS) 保护计算机之间的通信，最常见的是通过超文本传输协议安全 (HTTPS) 。 协议 1.1 1.0 版本不推荐使用，而 TLS 1.2 和 TLS 1.3 是最新的。 未来，TLS 1.2 和 TLS 1.3 可能已弃用。 若要确保应用程序的安全性，请避免硬编码协议版本，并以至少 .NET Framework v 4.7.1 为目标。 |
| CA5387 | [CA5387 不使用弱密钥派生函数，迭代次数不足](../code-quality/ca5387.md) | 此规则检查是否生成了的加密密钥 <xref:System.Security.Cryptography.Rfc2898DeriveBytes> ，迭代次数小于100000。 较高的迭代次数可帮助缓解字典攻击，尝试猜测生成的加密密钥。 |
| CA5388 | [使用弱密钥派生函数时，CA5388 确保有足够的迭代计数](../code-quality/ca5388.md) | 此规则检查是否生成的加密密钥 <xref:System.Security.Cryptography.Rfc2898DeriveBytes> 带有小于100000的迭代次数。 较高的迭代次数可帮助缓解字典攻击，尝试猜测生成的加密密钥。 |
| CA5389 | [CA5389：请勿将存档项的路径添加到目标文件系统路径中](../code-quality/ca5389.md) | 文件路径可以是相对路径，并且可能会导致文件系统在预期的文件系统目标路径外进行访问，从而导致恶意配置更改并通过 "等待" 等方法执行远程代码。 |
| CA5390 | [CA5390 不对加密密钥进行硬编码](../code-quality/ca5390.md) | 若要成功使用对称算法，密钥必须仅对发送方和接收方是已知的。 当某个密钥是硬编码的，很容易发现它。 即使已编译的二进制文件，恶意用户也可以轻松地将其提取出来。 私钥泄露后，可以直接解密密码文本，而不会再对其进行保护。 |
| CA5391 | [CA5391 使用 ASP.NET Core MVC 控制器中的防伪标记](../code-quality/ca5391.md) | 处理 `POST` 、、 `PUT` `PATCH` 或 `DELETE` 请求而不验证防伪令牌可能易受到跨站点请求伪造攻击。 跨站点请求伪造攻击可以将经过身份验证的用户的恶意请求发送到 ASP.NET Core MVC 控制器。 |
| CA5392 | [CA5392 将 DefaultDllImportSearchPaths 特性用于 P/Invoke](../code-quality/ca5392.md) | 默认情况下，使用探测的 P/Invoke 函数包含 <xref:System.Runtime.InteropServices.DllImportAttribute> 多个目录，其中包含要加载的库的当前工作目录。 对于某些应用程序，这可能是一个安全问题，导致 DLL 劫持。 |
| CA5393 | [CA5393 不使用 unsafe DllImportSearchPath 值](../code-quality/ca5393.md) | 默认 DLL 搜索目录和程序集目录中可能存在恶意 DLL。 或者，根据应用程序的运行位置，应用程序目录中可能存在恶意的 DLL。 |
| CA5394 | [CA5394 不使用不安全的随机性](../code-quality/ca5394.md) | 使用加密弱伪随机数生成器可以允许攻击者预测将生成的安全敏感值。 |
| CA5395 | [操作方法的 CA5395 缺失 HttpVerb 特性](../code-quality/ca5395.md) | 用于创建、编辑、删除或以其他方式修改数据的所有操作方法都需要通过跨站点请求伪造攻击的防伪属性进行保护。 执行 GET 操作应该是不会产生副作用的安全操作，并且不会修改您的持久数据。 |
| CA5396 | [对于 HttpCookie，CA5396 将 HttpOnly 设置为 true](../code-quality/ca5396.md) | 作为深层防御措施，请确保将安全敏感的 HTTP cookie 标记为 HttpOnly。 这表明 web 浏览器应禁止脚本访问 cookie。 注入的恶意脚本是偷窃 cookie 的常见方法。 |
| CA5397 | [CA5397：不使用已弃用的 SslProtocols 值](../code-quality/ca5397.md) | 传输层安全 (TLS) 保护计算机之间的通信，最常见的是通过超文本传输协议安全 (HTTPS) 。 较早的 TLS 协议版本不如 TLS 1.2 和 TLS 1.3 安全，更有可能出现新的漏洞。 避免旧协议版本来最大程度地降低风险。 |
| CA5398 | [CA5398：避免硬编码的 SslProtocols 值](../code-quality/ca5398.md) | 传输层安全 (TLS) 保护计算机之间的通信，最常见的是通过超文本传输协议安全 (HTTPS) 。 协议 1.1 1.0 版本不推荐使用，而 TLS 1.2 和 TLS 1.3 是最新的。 未来，TLS 1.2 和 TLS 1.3 可能已弃用。 若要确保应用程序的安全性，请避免硬编码协议版本。 |
| CA5399 | [CA5399 肯定禁用 HttpClient 证书吊销列表检查](../code-quality/ca5399.md) | 吊销的证书不再受信任。 攻击者可以使用它来传递某些恶意数据或偷窃 HTTPS 通信中的敏感数据。 |
| CA5400 | [CA5400 确保未禁用 HttpClient 证书吊销列表检查](../code-quality/ca5400.md) | 吊销的证书不再受信任。 攻击者可以使用它来传递某些恶意数据或偷窃 HTTPS 通信中的敏感数据。 |
| CA5401 | [CA5401 不将 CreateEncryptor 与非默认 IV 一起使用](../code-quality/ca5401.md) | 对称加密应始终使用不可重复的初始化向量来防止字典攻击。 |
| CA5402 | [CA5402 将 CreateEncryptor 与默认 IV 一起使用](../code-quality/ca5402.md) | 对称加密应始终使用不可重复的初始化向量来防止字典攻击。 |
| CA5403 | [CA5403：请勿硬编码证书](../code-quality/ca5403.md) | `data` `rawData` <xref:System.Security.Cryptography.X509Certificates.X509Certificate> 或构造函数的或参数 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 是硬编码的。 |
| IL3000 | [在发布为单个文件时，IL3000 避免访问程序集文件路径](../code-quality/il3000.md) | 在发布为单一文件时避免使用访问程序集文件路径 |
| IL3001 | [在发布为单文件时，IL3001 避免访问程序集文件路径](../code-quality/il3001.md) | 作为单文件发布时避免访问程序集文件路径 |
