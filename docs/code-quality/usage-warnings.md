---
title: 用法警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.usagerules
helpviewer_keywords:
- warnings, usage
- managed code analysis warnings, usage warnings
- usage warnings
ms.assetid: fe7dc2a3-289d-4bf7-a1e4-0947a81287c4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f58701cbebb4b738b635fac0c2805f07b4a5266f
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349543"
---
# <a name="usage-warnings"></a>用法警告

使用警告支持正确使用 .NET。

## <a name="in-this-section"></a>本节内容

|规则|描述|
|----------|-----------------|
|[CA1801：检查未使用的参数](../code-quality/ca1801.md)|方法签名包含一个没有在方法体中使用的参数。|
|[CA1806：不要忽略方法结果](../code-quality/ca1806.md)|创建一个新对象，但从不使用该对象；或者调用会创建并返回一个新字符串的方法，但从不使用这个新字符串；或者 COM 或 P/Invoke 方法返回一个从不使用的 HRESULT 或错误代码。|
|[CA1816：正确调用 GC.SuppressFinalize](../code-quality/ca1816.md)|作为 Dispose 实现的方法不调用 GC。Gc.suppressfinalize或者不是 Dispose 的实现的方法会调用 GC。Gc.suppressfinalize或方法调用 GC。Gc.suppressfinalize 并传递除此外的其他内容（我在 Visual Basic 中）。|
|[CA2200：再次引发以保留堆栈详细信息](../code-quality/ca2200.md)|再次引发某个异常，在 throw 语句中显式指定了该异常。 如果通过在 throw 语句中指定异常来重新引发该异常，则引发该异常的原始方法与当前方法之间的方法调用的列表将丢失。|
|[CA2201：不要引发保留的异常类型](../code-quality/ca2201.md)|这会使原始错误难以检测和调试。|
|[CA2202：不要多次释放对象](../code-quality/ca2202.md)|某个方法实现所包含的代码路径可能导致对同一对象多次调用 System.IDisposable.Dispose 或与 Dispose 等效的方法（例如，用于某些类型的 Close() 方法）。|
|[CA2204：应正确拼写文本](../code-quality/ca2204.md)|方法体中的文本字符串包含一个或多个未被 Microsoft 拼写检查器库识别的单词。|
|[CA2205：使用 Win32 API 的托管等效项](../code-quality/ca2205.md)|定义了平台调用方法，并提供了具有等效功能的 .NET 方法。|
|[CA2207：以内联方式初始化值类型的静态字段](../code-quality/ca2207.md)|某值类型声明了显式静态构造函数。 要修复与该规则的冲突，请在声明它时初始化所有静态数据并移除静态构造函数。|
|[CA2208：正确实例化参数异常](../code-quality/ca2208.md)|调用了异常类型 ArgumentException 或其派生类型的默认（无参数）构造函数，或者向异常类型 ArgumentException 或其派生类型的参数化构造函数传递了错误的字符串参数。|
|[CA2211：非常量字段不应为可见](../code-quality/ca2211.md)|不是常量或只读的静态字段不是线程安全的。 必须严格控制对此类字段的访问，并且需要使用高级编程技术来同步对类对象的访问。|
|[CA2212：不要使用 WebMethod 标记服务组件](../code-quality/ca2212.md)|从 System.enterpriseservices.servicedcomponent 继承的类型中的方法使用 ServicedComponent. WebMethodAttribute 进行标记。 因为 WebMethodAttribute 和 ServicedComponent 方法在上下文和事务流方面的行为和需求有冲突，所以该方法的行为在某些情况下会不正确。|
|[CA2213：应释放可释放的字段](../code-quality/ca2213.md)|实现 System.IDisposable 的类型声明了同样实现 IDisposable 的类型的字段。 字段的 Dispose 方法不由声明类型的 Dispose 方法调用。|
|[CA2214：不要在构造函数中调用可重写的方法](../code-quality/ca2214.md)|当构造函数调用虚方法时，调用方法的实例的构造函数可能未执行。|
|[CA2215：Dispose 方法应调用基类 Dispose](../code-quality/ca2215.md)|如果类型继承自可释放类型，则必须从它自己的 Dispose 方法中调用基类型的 Dispose 方法。|
|[CA2216：可释放类型应声明终结器](../code-quality/ca2216.md)|一种类型，它实现 IDisposable，并且具有建议使用非托管资源的字段，而不实现对象所描述的终结器。 Finalize。|
|[CA2217：不要使用 FlagsAttribute 标记枚举](../code-quality/ca2217.md)|外部可见的枚举标记有 FlagsAttribute，它具有一个或多个值，这些值不是整数的幂或枚举上的其他已定义值的组合。|
|[CA2218：重写 Equals 时重写 GetHashCode](../code-quality/ca2218.md)|GetHashCode 基于当前实例返回一个适合哈希算法和哈希表之类的数据结构的值。 两个相等的同类型对象必须返回相同的哈希代码。|
|[CA2219：在异常子句中不引发异常](../code-quality/ca2219.md)|如果在 finally 或 fault 子句中引发异常，新异常将隐藏活动异常。 当在 filter 子句中引发异常时，运行时会在不提示的情况下捕捉异常。 这会使原始错误难以检测和调试。|
|[CA2220：终结器应调用基类的终结器](../code-quality/ca2220.md)|终止必须通过继承层次结构传播。 为确保这一点，类型必须从其自身的 Finalize 方法调用它们的基类 Finalize 方法。|
|[CA2221：终结器应受到保护](../code-quality/ca2221.md)|终结器必须使用族访问修饰符。|
|[CA2222：不要递减继承成员的可见性](../code-quality/ca2222.md)|请勿更改继承成员的访问修饰符。 将继承的成员更改为私有成员不能防止调用方访问该方法的基类实现。|
|[CA2223：成员不应只是返回类型不同](../code-quality/ca2223.md)|虽然公共语言运行时允许使用返回类型区分其余部分都相同的成员，但该功能不包含在公共语言规范中，也不是各种 .NET 编程语言的共同功能。|
|[CA2224：重载相等运算符时重写 Equals 方法](../code-quality/ca2224.md)|公共类型实现相等运算符，但不重写对象 Equals。|
|[CA2225：运算符重载具有命名的备用项](../code-quality/ca2225.md)|检测到运算符重载，但未找到预期的指定备用方法。 命名的备用成员提供与运算符相同的功能的访问权限，并且为以不支持重载运算符的语言编写的开发人员提供。|
|[CA2226：运算符应有对称重载](../code-quality/ca2226.md)|类型实现了相等运算符或不相等运算符，并且未实现相反运算符。|
|[CA2227：集合属性应为只读](../code-quality/ca2227.md)|使用可写的集合属性，用户可以将该集合替换为不同的集合。 只读属性禁止替换该集合，但仍允许设置单个成员。|
|[CA2228：不要发行未发布的资源格式](../code-quality/ca2228.md)|使用 .NET 的预发布版本生成的资源文件可能无法由受支持的 .NET 版本使用。|
|[CA2229：实现序列化构造函数](../code-quality/ca2229.md)|要修复与该规则的冲突，请实现序列化构造函数。 对于密封类，请使构造函数成为私有；否则，请使构造函数成为受保护。|
|[CA2230：对可变数量的实参使用形参](../code-quality/ca2230.md)|公共或受保护类型包含一个使用 VarArgs 调用约定（而不是 params 关键字）的公共或受保护方法。|
|[CA2231：重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231.md)|值类型覆盖 `Object.Equals`，但不实现相等运算符。|
|[CA2232：使用 STAThread 标记 Windows 窗体的入口点](../code-quality/ca2232.md)|STAThreadAttribute 指示应用程序的 COM 线程模型是单线程单元。 使用 Windows 窗体的任何应用程序的入口点上必须存在此特性；如果没有此特性，则 Windows 组件可能无法正常工作。|
|[CA2233：运算不应溢出](../code-quality/ca2233.md)|在未首先验证操作数的情况下，不应执行算术运算，以确保操作的结果不在涉及的数据类型的可能值范围之外。|
|[CA2234：传递 System.Uri 对象，而不传递字符串](../code-quality/ca2234.md)|调用了带有一个字符串参数的方法，该参数的名称中包含“uri”、“URI”、“urn”、“URN”、“url”或“URL”。  此方法的声明类型包含具有 System.Uri 参数的对应方法重载。|
|[CA2235：标记所有不可序列化的字段](../code-quality/ca2235.md)|在可以序列化的类型中声明了类型不可序列化的实例字段。|
|[CA2236：对 ISerializable 类型调用基类方法](../code-quality/ca2236.md)|若要修复与该规则的冲突，请从相应的派生类型方法或构造函数调用基类型 GetObjectData 方法或序列化构造函数。|
|[CA2237：以 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237.md)|要由公共语言运行时识别为可序列化，即使类型通过实现 ISerializable 接口使用自定义序列化例程，也必须使用 SerializableAttribute 特性标记类型。|
|[CA2238：正确实现序列化方法](../code-quality/ca2238.md)|处理序列化事件的方法的签名、返回类型或可见性不正确。|
|[CA2239：为可选字段提供反序列化方法](../code-quality/ca2239.md)|类型具有一个用 OptionalFieldAttribute 特性标记的字段，并且该类型不提供反序列化事件处理方法。|
|[CA2240：正确实现 ISerializable](../code-quality/ca2240.md)|若要修复与此规则的冲突，请使 GetObjectData 方法可见并且可重写，并确保所有实例字段都包括在序列化过程中，或者使用 System.nonserializedattribute 特性显式标记所有实例字段。|
|[CA2241：为格式化方法提供正确的参数](../code-quality/ca2241.md)|传递给 System.string 格式的格式参数不包含对应于每个对象参数的格式项，反之亦然。|
|[CA2242：正确测试 NaN](../code-quality/ca2242.md)|此表达式对照 Single.Nan 或 Double.Nan 测试某个值。 使用 Single.IsNan(Single) 或 Double.IsNan(Double) 测试该值。|
|[CA2243：应正确分析特性字符串文本](../code-quality/ca2243.md)|对于 URL、GUID 或版本，无法正确分析特性的字符串文本参数。|
