---
title: 安全警告
ms.date: 10/02/2019
ms.topic: reference
f1_keywords:
- vs.codeanalysis.securityrules
helpviewer_keywords:
- security [Visual Studio ALM], Enterprise Templates
- security warnings
- managed code analysis warnings, security warnings
- warnings, security
ms.assetid: 60d4e8ea-230a-494f-aa6a-b91db77540e4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf1f318d8138bb455e965d7df44ae45e192904e3
ms.sourcegitcommit: 535ef05b1e553f0fc66082cd2e0998817eb2a56a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72018762"
---
# <a name="security-warnings"></a>安全警告

安全警告支持更安全的库和应用程序。 这些警告帮助防止程序中出现安全漏洞。 如果你禁用其中的某个警告，你应当在代码中清楚标出原因，同时将你的开发项目通知指定的安全负责人。

## <a name="in-this-section"></a>本节内容

|规则|描述|
|----------|-----------------|
|[CA2100：检查 SQL 查询是否存在安全漏洞 @ no__t-0|一个方法使用按该方法的字符串参数生成的字符串设置 System.Data.IDbCommand.CommandText 属性。 此规则假定字符串参数中包含用户输入。 基于用户输入生成的 SQL 命令字符串易于受到 SQL 注入式攻击。|
|[CA2102：在常规处理程序中捕捉非 CLSCompliant 异常 @ no__t-0|程序集中未标以 RuntimeCompatibilityAttribute 或标以 RuntimeCompatibility(WrapNonExceptionThrows = false) 的某个成员包含一个处理 System.Exception 的 catch 块，而不包含紧跟其后的一般 catch 块。|
|[CA2103：查看命令式 security @ no__t-0|某方法使用命令性安全，并且可能正在使用在请求处于活动状态时可以更改的状态信息或返回值来构造权限。 应尽可能使用声明性安全。|
|[CA2104：不要声明只读可变引用类型 @ no__t-0|外部可见类型包含外部可见的只读字段，该字段为可变的引用类型。 可变类型是实例数据可被修改的类型。|
|[CA2105：数组字段不应为只读 @ no__t-0|向包含数组的字段应用 readonly（在 Visual Basic 中为 ReadOnly）修饰符时，无法将该字段更改为引用其他数组。 但是，可以更改在只读字段中存储的数组的元素。|
|[CA2106：保护断言 @ no__t-0|某个方法断言权限，但不对调用方执行任何安全检查。 如果在不执行任何安全检查的情况下断言安全权限，则会在代码中留下可利用的安全漏洞。|
|[CA2107：查看 deny 并只允许使用 @ no__t-0|使用 PermitOnly 方法和 Codeaccesspermission.deny 安全操作只应由高级了解 .NET 安全的人员使用。 应当对使用这些安全操作的代码进行安全检查。|
|[CA2108：查看值类型 @ no__t 的声明性安全|公共或受保护值类型受数据访问或链接要求保护。|
|[CA2109：检查可见的事件处理程序 @ no__t-0|检测到公共事件处理方法或受保护事件处理方法。 除非绝对必要，否则不应公开事件处理方法。|
|[CA2111：指针不应为 @ no__t-0|指针不是私有、内部或只读指针。 恶意代码可以更改指针的值，这样就有可能访问内存中的任意位置或导致应用程序或系统故障。|
|[CA2112：受保护的类型不应公开字段 @ no__t-0|一个公共或受保护类型包含公共字段，并受链接要求保护。 如果代码可以访问受链接要求保护的类型的实例，则该代码不必满足此链接要求就可以访问该类型的字段。|
|[CA2114：方法 security 应为 @ no__t 类型的超集|一个方法不应同时有同一操作的方法级别和类型级别的声明性安全。|
|[CA2115：调用 GC。使用本机资源时 KeepAlive no__t-0|该规则检测由于在非托管代码仍在使用非托管资源时终止该非托管资源而可能发生的错误。|
|[CA2116：APTCA 方法应只调用 APTCA 方法 @ no__t-0|在完全受信任的程序集具有 APTCA (AllowPartiallyTrustedCallers) 特性时，如果该程序集执行另一个不允许部分受信任调用方的程序集中的代码，则可能存在安全漏洞。|
|[CA2117：APTCA 类型应只扩展 APTCA 基类型 @ no__t-0|在完全受信任的程序集具有 APTCA (AllowPartiallyTrustedCallers) 特性时，如果程序集中的某个类型是从不允许部分受信任调用方的类型继承而来，则可能会产生安全漏洞。|
|[CA2118：查看 SuppressUnmanagedCodeSecurityAttribute 用法 @ no__t-0|SuppressUnmanagedCodeSecurityAttribute 为执行使用 COM 互操作或平台调用的非托管代码的成员更改默认的安全系统行为。 该特性主要用于提高性能；不过，提高性能的同时会显著增加安全风险。|
|[CA2119：密封满足私有接口 @ no__t 的方法|可继承的公共类型为 internal（在 Visual Basic 中为 Friend）接口提供可重写的方法实现。 若要修复与此规则的冲突，请禁止方法在程序集外重写。|
|[CA2120：保护序列化构造函数 @ no__t|此类型的构造函数采用了 System.Runtime.Serialization.SerializationInfo 对象和 System.Runtime.Serialization.StreamingContext 对象（序列化构造函数的签名）。 此构造函数不受安全检查的保护，但类型中的一个或多个常规构造函数受保护。|
|[CA2121：静态构造函数应为私有](../code-quality/ca2121.md)|系统在创建第一个类型实例或引用任何静态成员之前调用静态构造函数。 如果静态构造函数不是私有，则系统以外的代码可以调用它。 根据构造函数中执行的操作，这可能导致意外行为。|
|[CA2122：不要通过链接要求间接公开方法 @ no__t-0|公共或受保护成员具有链接要求，且由不执行任何安全检查的成员调用。 链接请求仅检查直接调用方的权限。|
|[CA2123：重写链接请求应与 base @ no__t 相同-0|该规则将一个方法与其基方法（该基方法为另一个类型中的接口或虚方法）相匹配，然后比较两者的链接请求。 如果与此规则冲突，则恶意调用方只需调用不安全的方法，即可跳过该链接要求。|
|[CA2124：外部 try @ no__t 中的有漏洞的 finally 子句|公共或受保护方法中含有 try/finally 块。 finally 块似乎要重置安全状态，并且自身不包括在某个 finally 块中。|
|[CA2126：类型链接要求需要继承请求 @ no__t-0|一个公共的非密封类型受链接要求保护，并且具有可重写的方法。 类型和方法都不受继承要求保护。|
|[CA2130：安全关键常量应是透明的 @ no__t-0|未对常数值实施透明强制，因为编译器内联常数值以便在运行时不需要查找。 常数字段应为安全透明的，以便代码评审阅者不会假定透明代码不能访问常数。|
|[CA2131：安全关键类型不能参与类型等效性 @ no__t-0|类型参与类型等效性，类型本身（或类型的成员或字段）使用用 securitycriticalattribute 特性进行标记。 对于任何关键的类型或包含参与类型等效的关键方法或字段的类型，将引发此规则。 当 CLR 检测到这样的类型时，在运行时将不会加载它并引发 TypeLoadException。 通常，仅在用户手动实现类型等效而不是通过依赖 tlbimp 和编译器进行类型等效时，才会触发此规则。|
|[CA2132：默认构造函数必须至少与基类型默认构造函数 @ no__t-0 相同|具有 SecurityCriticalAttribute 的类型和成员无法供 Silverlight 应用程序代码使用。 安全关键类型和成员只能供 .NET Framework for Silverlight 类库中的受信任代码使用。 因为派生类中的某个公共或受保护构造必须有与其基类相同或更大的透明度，所以不能从标记为 SecurityCritical 的类派生应用程序中的类。|
|[CA2133：委托必须绑定到具有一致透明度 @ no__t 的方法|将对一个具有以下特点的方法引发此警告：该方法将用 SecurityCriticalAttribute 标记的委托绑定到一个透明的或用 SecuritySafeCriticalAttribute 标记的方法。 还会对另一个具有以下特点的方法引发此警告：该方法将透明的或安全关键的委托绑定到一个关键方法。|
|[CA2134：重写基方法时，方法必须保持一致的透明度 @ no__t-0|当用 SecurityCriticalAttribute 标记的方法重写一个透明的或用 SecuritySafeCriticalAttribute 标记的方法时，将引发此规则。 当一个透明的或用 SecuritySafeCriticalAttribute 标记的方法重写一个用 SecurityCriticalAttribute 标记的方法时，也会引发此规则。 该规则在重写虚方法或实现接口时应用。|
|[CA2135：Level 2 程序集不应包含 Linkdemand @ no__t-0|在级别为 2 的安全规则集中已弃用 LinkDemand。 现在使用 SecurityCriticalAttribute 特性标记方法、类型和字段，而不是使用 LinkDemand 在实时 (JIT) 编译时进行强制安全检查。|
|[CA2136：成员不应具有冲突的透明度注释 @ no__t-0|将透明特性从较大作用域的代码元素应用到较小作用域的元素。 具有较大作用域的代码元素的透明特性优于第一个元素中包含的代码元素的透明特性。 例如，用 SecurityCriticalAttribute 特性标记的类不能包含用 SecuritySafeCriticalAttribute 特性标记的方法。|
|[CA2137：透明方法必须仅包含可验证的 IL @ no__t-0|某个方法包含无法验证的代码或通过引用返回类型。 在尝试通过安全透明代码执行无法验证的 MSIL（Microsoft 中间语言）时将引发此规则。 但是，此规则不包含完整的 IL 验证程序，而是使用试探法来捕捉 MSIL 验证的大部分冲突。|
|[CA2138：透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性 @ no__t 的方法-0|一个安全透明方法调用使用 SuppressUnmanagedCodeSecurityAttribute 特性标记的方法。|
|[CA2139：透明方法不能使用 HandleProcessCorruptingExceptions 属性 @ no__t-0|此规则对任何透明的方法触发，并尝试通过使用 HandleProcessCorruptedStateExceptionsAttribute 特性处理进程损坏异常。 进程损坏异常是 CLR 版本4.0 异常分类（例如 <xref:System.AccessViolationException>）。 HandleProcessCorruptedStateExceptionsAttribute 特性只由安全关键方法使用，并且如果应用于透明的方法，则将被忽略。|
|[CA2140：透明代码不得引用安全关键项 @ no__t-0|标有 SecurityTransparentAttribute 的方法调用标为 SecurityCritical 的非公共成员。 此规则分析混合透明和严重的程序集中的所有方法和类型，并将对透明代码的任何调用标记为未标记为 SecurityTreatAsSafe 的非公共关键代码。|
|[CA2141：透明方法不得满足 LinkDemand](../code-quality/ca2141.md)|安全透明方法调用未用 AllowPartiallyTrustedCallersAttribute (APTCA) 特性标记的程序集中的方法，或者安全透明方法满足某个类型或方法的 LinkDemand。|
|[CA2142：不应通过 Linkdemand @ no__t 保护透明代码-0|对于需要 LinkDemand 来访问它们的透明方法，将会引发此规则。 安全透明代码不应负责验证某个操作的安全，因此不应要求权限。|
|[CA2143：透明方法不应使用安全要求 @ no__t-0|安全透明代码不应负责验证某个操作的安全，因此不应要求权限。 安全透明代码应使用完整的需求来作出安全决策并且安全关键代码不应依赖透明代码以进行完全的请求。|
|[CA2144：透明代码不应从字节数组 @ no__t 加载程序集|透明代码安全检查不像关键代码的安全检查一样全面，因为透明代码不能执行安全敏感的操作。 从字节数组中加载的程序集在不透明的代码中可能不会被注意到，并且该字节数组可能包含确实需要审核的关键或更重要的安全关键代码。|
|[CA2145：不应通过 SuppressUnmanagedCodeSecurityAttribute @ no__t 修饰透明方法|用 SuppressUnmanagedCodeSecurityAttribute 特性修饰的方法有一个隐式的 LinkDemand 作用于调用它的任何方法。 此 LinkDemand 要求调用代码是关键安全的。 用 SecurityCriticalAttribute 特性标记使用 SuppressUnmanagedCodeSecurity 的方法使此要求对方法的调用方更加明显。|
|[CA2146：类型必须至少与其基类型和接口 @ no__t|当派生类型具有的安全透明特性与其基类型或实现的接口不是同样关键时，将引发此规则。 只有关键类型可以从关键基类型派生或实现关键接口，并且只有关键或关键安全类型可以从安全关键基类型派生或实现关键安全接口。|
|[CA2147：透明方法不能使用安全断言 @ no__t-0|此规则分析完全透明或混合透明/关键的程序集中的所有方法和类型，并标记 Assert 的任何声明性或命令性用法。|
|[CA2149：透明方法不得调入本机代码 @ no__t-0|此规则对通过 P/Invoke 直接调用本机代码的任何透明方法引发。 违反此规则会导致级别 2 透明度模型中的 MethodAccessException，以及级别 1 透明度模型中对 UnmanagedCode 的完全要求。|
|[CA2151：具有关键类型的字段应为安全关键 @ no__t-0|若要使用安全关键类型，引用该类型的代码必须是安全关键或安全可靠关键。 即使引用是间接的，也需如此。 因此，具有安全透明字段或安全可靠关键字段具有误导性，因为透明代码仍然无法访问该字段。|
|[CA2153：避免处理损坏状态异常 @ no__t-0|[损坏状态异常 (CSE)](https://msdn.microsoft.com/magazine/dd419661.aspx) 指示进程中存在内存损坏。 如果攻击者可以将攻击放置到损坏的内存区域，则捕获它们（而非允许进程崩溃）可能导致安全漏洞。|
|[CA2300：不要使用不安全的反序列化程序 BinaryFormatter @ no__t-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2301：如果不先设置 BinaryFormatter @ no__t，请不要调用 BinaryFormatter|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2302：请确保在调用 BinaryFormatter 之前设置 BinaryFormatter @ no__t-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2305：不要使用不安全的反序列化程序 LosFormatter @ no__t-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2310：不要使用不安全的反序列化程序 NetDataContractSerializer @ no__t-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2311：不先设置 NetDataContractSerializer，不要反序列化 @ no__t-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2312：确保在反序列化 @ no__t 之前设置 NetDataContractSerializer|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2315：不要使用不安全的反序列化程序 ObjectStateFormatter @ no__t-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2321：不要使用 SimpleTypeResolver @ no__t 反序列化 JavaScriptSerializer|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2322：在反序列化 @ no__t-0 之前，请确保 JavaScriptSerializer 未初始化为 SimpleTypeResolver|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2326：不要使用 None @ no__t 的 TypeNameHandling 值-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2327：不要使用不安全的 JsonSerializerSettings @ no__t-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2328：确保 JsonSerializerSettings 为 secure @ no__t-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2329：不要使用不安全配置 @ no__t 反序列化 JsonSerializer|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2330：反序列化 @ no__t 时确保 JsonSerializer 的安全配置为-0|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA3001：查看 SQL 注入漏洞 @ no__t 的代码|使用不受信任的输入和 SQL 命令时，请注意 SQL 注入攻击。 SQL 注入攻击可以执行恶意的 SQL 命令，从而降低应用程序的安全性和完整性。|
|[CA3002：查看 XSS 漏洞 @ no__t 的代码|当处理 web 请求中的不受信任输入时，请注意跨站点脚本（XSS）攻击。 XSS 攻击会将不受信任的输入注入原始 HTML 输出，使攻击者可以执行恶意脚本或恶意修改网页中的内容。|
|[CA3003：查看文件路径注入漏洞 @ no__t 的代码|当处理 web 请求中的不受信任输入时，请注意在指定文件路径时使用用户控制输入。|
|[CA3004：查看有关信息泄漏漏洞 @ no__t 的代码|泄露异常信息可让攻击者深入了解应用程序的内部机制，从而帮助攻击者找到其他漏洞来利用这些漏洞。|
|[CA3006：查看进程命令注入漏洞 @ no__t 的代码|使用不受信任的输入时，请注意命令注入攻击。 命令注入攻击可以在基础操作系统上执行恶意命令，从而危及服务器的安全和完整性。|
|[CA3007：查看打开重定向漏洞 @ no__t 的代码|使用不受信任的输入时，请注意开放重定向漏洞。 攻击者可以利用开放的重定向漏洞来使用您的网站来获得合法 URL 的外观，但将不受信任的访问者重定向到仿冒网站或其他恶意网页。|
|[CA3008：查看 XPath 注入漏洞 @ no__t 的代码|使用不受信任的输入时，请注意 XPath 注入式攻击。 使用不受信任输入构造 XPath 查询时，攻击者可能会恶意地操作查询以返回意外的结果，并可能会泄漏所查询的 XML 的内容。|
|[CA3009：查看 XML 注入漏洞 @ no__t 的代码|使用不受信任的输入时，请注意 XML 注入攻击。|
|[CA3010：查看 XAML 注入漏洞 @ no__t 的代码|使用不受信任的输入时，请注意 XAML 注入攻击。 XAML 是一种直接表示对象实例化和执行的标记语言。 这意味着在 XAML 中创建的元素可以与系统资源（例如，网络访问和文件系统 IO）交互。|
|[CA3011：查看 DLL 注入漏洞 @ no__t 的代码|使用不受信任的输入时，请注意加载不受信任的代码。 如果你的 web 应用程序加载不受信任的代码，攻击者可能能够将恶意 Dll 注入到你的进程中并执行恶意代码。|
|[CA3012：查看适用于 regex 注入漏洞 @ no__t 的代码|使用不受信任的输入时，请注意 regex 注入式攻击。 攻击者可以使用 regex 注入来恶意地修改正则表达式，以使 regex 与意外结果匹配，或使 regex 消耗过多的 CPU，导致拒绝服务攻击。|
|[CA3061：不按 URL 添加架构 @ no__t-0|不要使用 Add 方法的 unsafe 重载，因为这可能会导致危险的外部引用。|
|[CA3075：非安全 DTD 处理 @ no__t-0|如果使用不安全的 DTDProcessing 实例或引用外部实体源，分析器可能会接受不受信任的输入并将敏感信息泄露给攻击者。|
|[CA3076：不安全的 XSLT 脚本执行 @ no__t-0|如果在 .NET 应用程序中不安全地执行可扩展样式表语言转换 (XSLT)，处理器可能会解析不受信任的 URI 引用，这种引用会把敏感信息泄露给攻击者，从而导致拒绝服务和跨站点攻击。|
|[CA3077：API 设计、XML 文档和 XML 文本读取器中的不安全处理 @ no__t-0|当设计派生自 XMLDocument 和 XMLTextReader 的 API 时，请注意 DtdProcessing。 当引用或解析外部实体源或设置 XML 中的不安全值时，使用不安全的 DTDProcessing 实例可能会导致信息泄露。|
|[CA3147：用 ValidateAntiForgeryToken @ no__t 标记谓词处理程序-0|设计 ASP.NET MVC 控制器时，请注意跨站点请求伪造攻击。 跨站点请求伪造攻击可以将经过身份验证的用户的恶意请求发送到 ASP.NET MVC 控制器。|
|[CA5122 P/Invoke 声明不应为安全临界](../code-quality/ca5122.md)|当方法执行安全敏感性操作时，将被标记为 SecuritySafeCritical，但透明代码使用它们也是安全的。 透明代码决不能通过通过 P/Invoke 直接调用本机代码。 因此，将 P/Invoke 标记为安全关键将使透明代码无法调用它，并且会误导安全分析。|
|[CA5361：不要禁止 SChannel 使用强加密 @ no__t-0|将 @no__t 设置为 `true` 受损传出传输层安全性（TLS）连接中使用的加密。 较弱的加密可能会危及应用程序与服务器之间通信的机密性，使攻击者更容易窃听敏感数据。|
|[CA5363：不要禁用请求验证 @ no__t-0|请求验证是 ASP.NET 中的一项功能，用于检查 HTTP 请求并确定这些请求是否包含可能导致注入攻击（包括跨站点脚本）的潜在危险内容。|
|[CA5364：不要使用已弃用的安全协议 @ no__t-0|传输层安全性（TLS）保护计算机之间的通信，最常见的是通过超文本传输协议（HTTPS）进行通信。 较早的 TLS 协议版本不如 TLS 1.2 和 TLS 1.3 安全，更有可能出现新的漏洞。 避免旧协议版本来最大程度地降低风险。|
|[CA5369：使用 XmlReader 反序列化 @ no__t-0|处理不受信任的 DTD 和 XML 架构可能会启用加载危险的外部引用，这应通过使用具有安全解析程序的 XmlReader 或禁用 DTD 和 XML 内联架构处理来限制。|
|[CA5370：使用 XmlReader 验证读者 @ no__t-0|处理不受信任的 DTD 和 XML 架构可能会启用加载危险的外部引用。 可以通过将 XmlReader 与安全解析程序结合使用，或者禁用 DTD 和 XML 内联架构处理来限制这种危险加载。|
|[CA5371：使用 XmlReader 进行架构读取 @ no__t-0|处理不受信任的 DTD 和 XML 架构可能会启用加载危险的外部引用。 将 XmlReader 用于安全解析程序或 DTD 和 XML 内联架构处理将会限制这种情况。|
|[CA5372：将 XmlReader 用于 XPathDocument @ no__t-0|处理来自不受信任数据的 XML 可能会加载危险的外部引用，这可以通过使用具有安全解析程序的 XmlReader 或禁用 DTD 处理来限制。|
|[CA5373：不要使用过时密钥派生函数 @ no__t-0|此规则检测 <xref:System.Security.Cryptography.PasswordDeriveBytes?displayProperty=fullName> 和 `Rfc2898DeriveBytes.CryptDeriveKey` 的弱密钥派生方法的调用。 <xref:System.Security.Cryptography.PasswordDeriveBytes?displayProperty=fullName> 使用弱算法 PBKDF1。|
|[CA5378：不要禁用 ServicePointManagerSecurityProtocols @ no__t-0|将 @no__t 设置为 `true` 会将 Windows Communication Framework （WCF）传输层安全性（TLS）连接限制为使用 TLS 1.0。 TLS 版本将不推荐使用。|
|[CA5380：不要将证书添加到根存储 @ no__t-0|此规则检测将证书添加到 "受信任的根证书颁发机构" 证书存储中的代码。 默认情况下，"受信任的根证书颁发机构" 证书存储区配置为满足 Microsoft 根证书计划要求的一组公共 Ca。|
|[CA5381：确保证书未添加到根存储 @ no__t-0|此规则检测可能会将证书添加到 "受信任的根证书颁发机构" 证书存储中的代码。 默认情况下，"受信任的根证书颁发机构" 证书存储区使用满足 Microsoft 根证书计划要求的一组公共证书颁发机构（Ca）进行配置。|
|[CA5386：避免硬编码 SecurityProtocolType 值 @ no__t-0|传输层安全性（TLS）保护计算机之间的通信，最常见的是通过超文本传输协议（HTTPS）进行通信。 协议 1.1 1.0 版本不推荐使用，而 TLS 1.2 和 TLS 1.3 是最新的。 未来，TLS 1.2 和 TLS 1.3 可能已弃用。 若要确保应用程序的安全性，请避免硬编码协议版本，并以至少 .NET Framework v 4.7.1 为目标。|
|[CA5389：不要将存档项的路径添加到目标文件系统路径 @ no__t-0|文件路径可以是相对路径，并且可能会导致文件系统在预期的文件系统目标路径外进行访问，从而导致恶意配置更改并通过 "等待" 等方法执行远程代码。|
|[CA5397：不要使用已弃用的 SslProtocols 值 @ no__t-0|ransport 层安全性（TLS）保护计算机之间的通信，最常见的是通过超文本传输协议（HTTPS）进行通信。 较早的 TLS 协议版本不如 TLS 1.2 和 TLS 1.3 安全，更有可能出现新的漏洞。 避免旧协议版本来最大程度地降低风险。|
|[CA5398：避免将硬编码的 SslProtocols 值 @ no__t-0|传输层安全性（TLS）保护计算机之间的通信，最常见的是通过超文本传输协议（HTTPS）进行通信。 协议 1.1 1.0 版本不推荐使用，而 TLS 1.2 和 TLS 1.3 是最新的。 未来，TLS 1.2 和 TLS 1.3 可能已弃用。 若要确保应用程序的安全性，请避免硬编码协议版本。|
