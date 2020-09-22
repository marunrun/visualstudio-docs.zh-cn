---
title: 使用规则
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.usagerules
helpviewer_keywords:
- rules, usage
- managed code analysis rules, usage rules
- usage rules
ms.assetid: fe7dc2a3-289d-4bf7-a1e4-0947a81287c4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 45dd58978bb37dd66023d8a28b9babf017bec262
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90806182"
---
# <a name="usage-rules"></a>使用规则

使用规则支持正确使用 .NET。

## <a name="in-this-section"></a>本节内容

|规则|描述|
|----------|-----------------|
|[CA1801:检查未使用的参数](../code-quality/ca1801.md)|方法签名包含一个没有在方法体中使用的参数。|
|[CA1816:正确调用 GC.SuppressFinalize](../code-quality/ca1816.md)|作为 Dispose 的实现的某个方法未调用 GC.SuppressFinalize；或者不是 Dispose 的实现的某个方法调用了 GC.SuppressFinalize；或者某个方法调用了 GC.SuppressFinalize 并传递 this（在 Visual Basic 中是 Me）以外的某个值。|
|[CA2200:再次引发以保留堆栈详细信息](../code-quality/ca2200.md)|再次引发某个异常，在 throw 语句中显式指定了该异常。 如果通过在 throw 语句中指定异常来重新引发该异常，则引发该异常的原始方法与当前方法之间的方法调用的列表将丢失。|
|[CA2201:不要引发保留的异常类型](../code-quality/ca2201.md)|这会使原始错误难以检测和调试。|
|[CA2202:不要多次释放对象](../code-quality/ca2202.md)|某个方法实现所包含的代码路径可能导致对同一对象多次调用 System.IDisposable.Dispose 或与 Dispose 等效的方法（例如，用于某些类型的 Close() 方法）。|
|[CA2207:以内联方式初始化值类型的静态字段](../code-quality/ca2207.md)|某值类型声明了显式静态构造函数。 要修复与该规则的冲突，请在声明它时初始化所有静态数据并移除静态构造函数。|
|[CA2208:正确实例化参数异常](../code-quality/ca2208.md)|调用了异常类型 ArgumentException 或其派生类型的默认（无参数）构造函数，或者向异常类型 ArgumentException 或其派生类型的参数化构造函数传递了错误的字符串参数。|
|[CA2211:非常量字段不应是可见的](../code-quality/ca2211.md)|不是常量或只读的静态字段不是线程安全的。 必须严格控制对此类字段的访问，并且需要使用高级编程技术来同步对类对象的访问。|
|[CA2213:应释放可释放的字段](../code-quality/ca2213.md)|实现 System.IDisposable 的类型声明了同样实现 IDisposable 的类型的字段。 字段的 Dispose 方法不由声明类型的 Dispose 方法调用。|
|[CA2214:不要在构造函数中调用可重写的方法](../code-quality/ca2214.md)|当构造函数调用虚方法时，调用方法的实例的构造函数可能未执行。|
|[CA2215:Dispose 方法应调用基类释放](../code-quality/ca2215.md)|如果类型继承自可释放类型，则必须从它自己的 Dispose 方法中调用基类型的 Dispose 方法。|
|[CA2216:可释放类型应声明终结器](../code-quality/ca2216.md)|一种类型，它实现 IDisposable，并且具有建议使用非托管资源的字段，而不实现对象所描述的终结器。 Finalize。|
|[CA2217:不要使用 FlagsAttribute 标记枚举](../code-quality/ca2217.md)|外部可见的枚举标记有 FlagsAttribute，它具有一个或多个值，这些值不是整数的幂或枚举上的其他已定义值的组合。|
|[CA2219:在异常子句中不引发异常](../code-quality/ca2219.md)|如果在 finally 或 fault 子句中引发异常，新异常将隐藏活动异常。 当在 filter 子句中引发异常时，运行时会在不提示的情况下捕捉异常。 这会使原始错误难以检测和调试。|
|[CA2225:运算符重载具有命名的备用项](../code-quality/ca2225.md)|检测到运算符重载，但未找到预期的指定备用方法。 命名的备用成员提供与运算符相同的功能的访问权限，并且为以不支持重载运算符的语言编写的开发人员提供。|
|[CA2226:运算符应有对称重载](../code-quality/ca2226.md)|类型实现了相等运算符或不相等运算符，并且未实现相反运算符。|
|[CA2227:集合属性应为只读](../code-quality/ca2227.md)|使用可写的集合属性，用户可以将该集合替换为不同的集合。 只读属性禁止替换该集合，但仍允许设置单个成员。|
|[CA2229:实现序列化构造函数](../code-quality/ca2229.md)|要修复与该规则的冲突，请实现序列化构造函数。 对于密封类，请使构造函数成为私有；否则，请使构造函数成为受保护。|
|[CA2231:重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231.md)|值类型会重写 `Object.Equals` ，但不实现相等运算符。|
|[CA2232:使用 STAThread 标记 Windows 窗体的入口点](../code-quality/ca2232.md)|STAThreadAttribute 指示应用程序的 COM 线程模型是单线程单元。 使用 Windows 窗体的任何应用程序的入口点上必须存在此特性；如果没有此特性，则 Windows 组件可能无法正常工作。|
|[CA2233:运算不应溢出](../code-quality/ca2233.md)|在未首先验证操作数的情况下，不应执行算术运算，以确保操作的结果不在涉及的数据类型的可能值范围之外。|
|[CA2234:传递 System.Uri 对象，而不传递字符串](../code-quality/ca2234.md)|调用了带有一个字符串参数的方法，该参数的名称中包含“uri”、“URI”、“urn”、“URN”、“url”或“URL”。  此方法的声明类型包含具有 System.Uri 参数的对应方法重载。|
|[CA2235:标记所有不可序列化的字段](../code-quality/ca2235.md)|在可以序列化的类型中声明了类型不可序列化的实例字段。|
|[CA2236:对 ISerializable 类型调用基类方法](../code-quality/ca2236.md)|若要修复与该规则的冲突，请从相应的派生类型方法或构造函数调用基类型 GetObjectData 方法或序列化构造函数。|
|[CA2237:用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237.md)|要由公共语言运行时识别为可序列化，即使类型通过实现 ISerializable 接口使用自定义序列化例程，也必须使用 SerializableAttribute 特性标记类型。|
|[CA2238:正确实现序列化方法](../code-quality/ca2238.md)|处理序列化事件的方法的签名、返回类型或可见性不正确。|
|[CA2239:为可选字段提供反序列化方法](../code-quality/ca2239.md)|类型具有一个用 OptionalFieldAttribute 特性标记的字段，并且该类型不提供反序列化事件处理方法。|
|[CA2240:正确实现 ISerializable](../code-quality/ca2240.md)|若要修复与此规则的冲突，请使 GetObjectData 方法可见并且可重写，并确保所有实例字段都包括在序列化过程中，或者使用 System.nonserializedattribute 特性显式标记所有实例字段。|
|[CA2241:为格式化方法提供正确的参数](../code-quality/ca2241.md)|传递给 System.string 格式的格式参数不包含对应于每个对象参数的格式项，反之亦然。|
|[CA2242:正确测试 NaN](../code-quality/ca2242.md)|此表达式对照 Single.Nan 或 Double.Nan 测试某个值。 使用 Single.IsNan(Single) 或 Double.IsNan(Double) 测试该值。|
|[CA2243:特性字符串文本应正确分析](../code-quality/ca2243.md)|对于 URL、GUID 或版本，无法正确分析特性的字符串文本参数。|
|[CA2244:不要复制已索引的元素初始值设定项](../code-quality/ca2244.md)|对象初始值设定项具有多个具有相同的常量索引的索引元素初始值设定项。 除最后一个初始值设定项之外的所有都是冗余的。|
|[CA2245:请勿将属性分配给其自身](../code-quality/ca2245.md)|属性意外分配给自身。|
|[CA2246:请勿在同一语句中分配符号及其成员](../code-quality/ca2246.md)|不建议在同一语句中分配符号及其成员（即，字段或属性）。 如果成员访问权限打算在赋值前使用符号的旧值，或者在此语句的赋值中使用新值，则不清楚。|
|[CA2247:传递给 TaskCompletionSource 构造函数的参数应为 TaskCreationOptions 枚举，而不是 TaskContinuationOptions 枚举](../code-quality/ca2246.md)|TaskCompletionSource 具有采用 TaskCreationOptions 的构造函数，这些构造函数控制基础任务，以及采用任务中存储的对象状态的构造函数。  意外传递 System.threading.tasks.taskcontinuationoptions 而不是 TaskCreationOptions 将导致调用将选项视为状态。|
|[CA2248：将正确的 "enum" 参数提供给 "Enum.hasflag\"](../code-quality/ca2248.md)|作为参数传递给方法调用的枚举类型 `HasFlag` 不同于调用枚举类型。|
|[CA2249：请考虑使用 String.Contains 而不是 String.IndexOf](../code-quality/ca2249.md)|对结果的调用 `string.IndexOf` （其中，用于检查是否存在子字符串）可以替换为 `string.Contains` 。|
