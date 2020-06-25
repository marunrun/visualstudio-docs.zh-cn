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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d8fbeb9b1631e9cefa132f50a13dc5cf4db58c9d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283367"
---
# <a name="security-warnings"></a>安全警告

安全警告支持更安全的库和应用程序。 这些警告帮助防止程序中出现安全漏洞。 如果你禁用其中的某个警告，你应当在代码中清楚标出原因，同时将你的开发项目通知指定的安全负责人。

## <a name="in-this-section"></a>本节内容

|规则|说明|
|----------|-----------------|
|[CA2100:检查 SQL 查询是否存在安全漏洞](../code-quality/ca2100.md)|一个方法使用按该方法的字符串参数生成的字符串设置 System.Data.IDbCommand.CommandText 属性。 此规则假定字符串参数中包含用户输入。 基于用户输入生成的 SQL 命令字符串易于受到 SQL 注入式攻击。|
|[CA2102:在常规处理程序中捕捉非 CLSCompliant 异常](../code-quality/ca2102.md)|程序集中未标以 RuntimeCompatibilityAttribute 或标以 RuntimeCompatibility(WrapNonExceptionThrows = false) 的某个成员包含一个处理 System.Exception 的 catch 块，而不包含紧跟其后的一般 catch 块。|
|[CA2103:检查命令性安全](../code-quality/ca2103.md)|某方法使用命令性安全，并且可能正在使用在请求处于活动状态时可以更改的状态信息或返回值来构造权限。 应尽可能使用声明性安全。|
|[CA2104:不要声明只读可变引用类型](../code-quality/ca2104.md)|外部可见类型包含外部可见的只读字段，该字段为可变的引用类型。 可变类型是实例数据可被修改的类型。|
|[CA2105:数组字段不应为只读](../code-quality/ca2105.md)|向包含数组的字段应用 readonly（在 Visual Basic 中为 ReadOnly）修饰符时，无法将该字段更改为引用其他数组。 但是，可以更改在只读字段中存储的数组的元素。|
|[CA2106:保护断言](../code-quality/ca2106.md)|某个方法断言权限，但不对调用方执行任何安全检查。 如果在不执行任何安全检查的情况下断言安全权限，则会在代码中留下可利用的安全漏洞。|
|[CA2107:检查 deny 权限和 permit only 权限的使用情况](../code-quality/ca2107.md)|使用 PermitOnly 方法和 Codeaccesspermission.deny 安全操作只应由高级了解 .NET 安全的人员使用。 应当对使用这些安全操作的代码进行安全检查。|
|[CA2108:检查有关值类型的声明性安全](../code-quality/ca2108.md)|公共或受保护值类型受数据访问或链接要求保护。|
|[CA2109:检查可见的事件处理程序](../code-quality/ca2109.md)|检测到公共事件处理方法或受保护事件处理方法。 除非绝对必要，否则不应公开事件处理方法。|
|[CA2111:指针应为不可见](../code-quality/ca2111.md)|指针不是私有、内部或只读指针。 恶意代码可以更改指针的值，这样就有可能访问内存中的任意位置或导致应用程序或系统故障。|
|[CA2112:受保护的类型不应公开字段](../code-quality/ca2112.md)|一个公共或受保护类型包含公共字段，并受链接要求保护。 如果代码可以访问受链接要求保护的类型的实例，则该代码不必满足此链接要求就可以访问该类型的字段。|
|[CA2114:方法安全性应是类型安全性的超集](../code-quality/ca2114.md)|一个方法不应同时有同一操作的方法级别和类型级别的声明性安全。|
|[CA2115:使用本机资源时调用 GC.KeepAlive](../code-quality/ca2115.md)|该规则检测由于在非托管代码仍在使用非托管资源时终止该非托管资源而可能发生的错误。|
|[CA2116:APTCA 方法应只调用 APTCA 方法](../code-quality/ca2116.md)|在完全受信任的程序集具有 APTCA (AllowPartiallyTrustedCallers) 特性时，如果该程序集执行另一个不允许部分受信任调用方的程序集中的代码，则可能存在安全漏洞。|
|[CA2117:APTCA 类型应只扩展 APTCA 基类型](../code-quality/ca2117.md)|在完全受信任的程序集具有 APTCA (AllowPartiallyTrustedCallers) 特性时，如果程序集中的某个类型是从不允许部分受信任调用方的类型继承而来，则可能会产生安全漏洞。|
|[CA2118:检查 SuppressUnmanagedCodeSecurityAttribute 用法](../code-quality/ca2118.md)|SuppressUnmanagedCodeSecurityAttribute 为执行使用 COM 互操作或平台调用的非托管代码的成员更改默认的安全系统行为。 该特性主要用于提高性能；不过，提高性能的同时会显著增加安全风险。|
|[CA2119:密封满足私有接口的方法](../code-quality/ca2119.md)|可继承的公共类型为 internal（在 Visual Basic 中为 Friend）接口提供可重写的方法实现。 若要修复与此规则的冲突，请禁止方法在程序集外重写。|
|[CA2120:保护序列化构造函数](../code-quality/ca2120.md)|此类型的构造函数采用了 System.Runtime.Serialization.SerializationInfo 对象和 System.Runtime.Serialization.StreamingContext 对象（序列化构造函数的签名）。 此构造函数不受安全检查的保护，但类型中的一个或多个常规构造函数受保护。|
|[CA2121:静态构造函数应为私有](../code-quality/ca2121.md)|系统在创建第一个类型实例或引用任何静态成员之前调用静态构造函数。 如果静态构造函数不是私有，则系统以外的代码可以调用它。 根据构造函数中执行的操作，这可能导致意外行为。|
|[CA2122:不要使用链接请求间接公开方法](../code-quality/ca2122.md)|公共或受保护成员具有链接要求，且由不执行任何安全检查的成员调用。 链接请求仅检查直接调用方的权限。|
|[CA2123:重写链接请求应与基相同](../code-quality/ca2123.md)|该规则将一个方法与其基方法（该基方法为另一个类型中的接口或虚方法）相匹配，然后比较两者的链接请求。 如果与此规则冲突，则恶意调用方只需调用不安全的方法，即可跳过该链接要求。|
|[CA2124:在外部 try 块中包装易受攻击的 finally 子句](../code-quality/ca2124.md)|公共或受保护方法中含有 try/finally 块。 finally 块似乎要重置安全状态，并且自身不包括在某个 finally 块中。|
|[CA2126:类型链接请求需要继承请求](../code-quality/ca2126.md)|一个公共的非密封类型受链接要求保护，并且具有可重写的方法。 类型和方法都不受继承要求保护。|
|[CA2130:安全关键常量应是透明的](../code-quality/ca2130.md)|未对常数值实施透明强制，因为编译器内联常数值以便在运行时不需要查找。 常数字段应为安全透明的，以便代码评审阅者不会假定透明代码不能访问常数。|
|[CA2131:安全关键类型不能参与类型等效](../code-quality/ca2131.md)|类型参与类型等效性，类型本身（或类型的成员或字段）使用用 securitycriticalattribute 特性进行标记。 对于任何关键的类型或包含参与类型等效的关键方法或字段的类型，将引发此规则。 当 CLR 检测到这样的类型时，在运行时将不会加载它并引发 TypeLoadException。 通常，仅在用户手动实现类型等效而不是通过依赖 tlbimp 和编译器进行类型等效时，才会触发此规则。|
|[CA2132:默认构造函数必须至少与基类型默认构造函数一样关键](../code-quality/ca2132.md)|具有 SecurityCriticalAttribute 的类型和成员无法供 Silverlight 应用程序代码使用。 安全关键类型和成员只能供 .NET Framework for Silverlight 类库中的受信任代码使用。 因为派生类中的某个公共或受保护构造必须有与其基类相同或更大的透明度，所以不能从标记为 SecurityCritical 的类派生应用程序中的类。|
|[CA2133:委托必须绑定到具有一致透明度的方法](../code-quality/ca2133.md)|将对一个具有以下特点的方法引发此警告：该方法将用 SecurityCriticalAttribute 标记的委托绑定到一个透明的或用 SecuritySafeCriticalAttribute 标记的方法。 还会对另一个具有以下特点的方法引发此警告：该方法将透明的或安全关键的委托绑定到一个关键方法。|
|[CA2134:在重写基方法时，方法必须保持一致的透明度](../code-quality/ca2134.md)|当用 SecurityCriticalAttribute 标记的方法重写一个透明的或用 SecuritySafeCriticalAttribute 标记的方法时，将引发此规则。 当一个透明的或用 SecuritySafeCriticalAttribute 标记的方法重写一个用 SecurityCriticalAttribute 标记的方法时，也会引发此规则。 该规则在重写虚方法或实现接口时应用。|
|[CA2135:级别 2 程序集不应包含 LinkDemand](../code-quality/ca2135.md)|在级别为 2 的安全规则集中已弃用 LinkDemand。 现在使用 SecurityCriticalAttribute 特性标记方法、类型和字段，而不是使用 LinkDemand 在实时 (JIT) 编译时进行强制安全检查。|
|[CA2136:成员不应具有冲突的透明度批注](../code-quality/ca2136.md)|将透明特性从较大作用域的代码元素应用到较小作用域的元素。 具有较大作用域的代码元素的透明特性优于第一个元素中包含的代码元素的透明特性。 例如，用 SecurityCriticalAttribute 特性标记的类不能包含用 SecuritySafeCriticalAttribute 特性标记的方法。|
|[CA2137:透明方法只能包含可验证的 IL](../code-quality/ca2137.md)|某个方法包含无法验证的代码或通过引用返回类型。 在尝试通过安全透明代码执行无法验证的 MSIL（Microsoft 中间语言）时将引发此规则。 但是，此规则不包含完整的 IL 验证程序，而是使用试探法来捕捉 MSIL 验证的大部分冲突。|
|[CA2138:透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法](../code-quality/ca2138.md)|一个安全透明方法调用使用 SuppressUnmanagedCodeSecurityAttribute 特性标记的方法。|
|[CA2139:透明方法不能使用 HandleProcessCorruptingExceptions 特性](../code-quality/ca2139.md)|此规则对任何透明的方法触发，并尝试通过使用 HandleProcessCorruptedStateExceptionsAttribute 特性处理进程损坏异常。 进程损坏异常是异常（如）的 CLR 版本4.0 异常分类 <xref:System.AccessViolationException> 。 HandleProcessCorruptedStateExceptionsAttribute 特性只由安全关键方法使用，并且如果应用于透明的方法，则将被忽略。|
|[CA2140:透明代码不得引用安全关键项](../code-quality/ca2140.md)|标有 SecurityTransparentAttribute 的方法调用标为 SecurityCritical 的非公共成员。 此规则分析混合透明和严重的程序集中的所有方法和类型，并将对透明代码的任何调用标记为未标记为 SecurityTreatAsSafe 的非公共关键代码。|
|[CA2141：透明方法不得满足 LinkDemand](../code-quality/ca2141.md)|安全透明方法调用未用 AllowPartiallyTrustedCallersAttribute (APTCA) 特性标记的程序集中的方法，或者安全透明方法满足某个类型或方法的 LinkDemand。|
|[CA2142:不应使用 LinkDemand 保护透明代码](../code-quality/ca2142.md)|对于需要 LinkDemand 来访问它们的透明方法，将会引发此规则。 安全透明代码不应负责验证某个操作的安全，因此不应要求权限。|
|[CA2143:透明方法不应使用安全请求](../code-quality/ca2143.md)|安全透明代码不应负责验证某个操作的安全，因此不应要求权限。 安全透明代码应使用完整的需求来作出安全决策并且安全关键代码不应依赖透明代码以进行完全的请求。|
|[CA2144:透明代码不应从字节数组加载程序集](../code-quality/ca2144.md)|透明代码安全检查不像关键代码的安全检查一样全面，因为透明代码不能执行安全敏感的操作。 从字节数组中加载的程序集在不透明的代码中可能不会被注意到，并且该字节数组可能包含确实需要审核的关键或更重要的安全关键代码。|
|[CA2145:不应使用 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法](../code-quality/ca2145.md)|用 SuppressUnmanagedCodeSecurityAttribute 特性修饰的方法有一个隐式的 LinkDemand 作用于调用它的任何方法。 此 LinkDemand 要求调用代码是关键安全的。 用 SecurityCriticalAttribute 特性标记使用 SuppressUnmanagedCodeSecurity 的方法使此要求对方法的调用方更加明显。|
|[CA2146:类型必须至少与其基类型和接口一样关键](../code-quality/ca2146.md)|当派生类型具有的安全透明特性与其基类型或实现的接口不是同样关键时，将引发此规则。 只有关键类型可以从关键基类型派生或实现关键接口，并且只有关键或关键安全类型可以从安全关键基类型派生或实现关键安全接口。|
|[CA2147:透明方法不得使用安全断言](../code-quality/ca2147.md)|此规则分析完全透明或混合透明/关键的程序集中的所有方法和类型，并标记 Assert 的任何声明性或命令性用法。|
|[CA2149:透明方法不得调入本机代码](../code-quality/ca2149.md)|此规则对通过 P/Invoke 直接调用本机代码的任何透明方法引发。 违反此规则会导致级别 2 透明度模型中的 MethodAccessException，以及级别 1 透明度模型中对 UnmanagedCode 的完全要求。|
|[CA2151:具有关键类型的字段应为安全关键的](../code-quality/ca2151.md)|若要使用安全关键类型，引用该类型的代码必须是安全关键或安全可靠关键。 即使引用是间接的，也需如此。 因此，具有安全透明字段或安全可靠关键字段具有误导性，因为透明代码仍然无法访问该字段。|
|[CA2153:避免处理损坏状态异常](../code-quality/ca2153.md)|[损坏状态异常 (CSE)](https://msdn.microsoft.com/magazine/dd419661.aspx) 指示进程中存在内存损坏。 如果攻击者可以将攻击放置到损坏的内存区域，则捕获它们（而非允许进程崩溃）可能导致安全漏洞。|
|[CA2300：请勿使用不安全的反序列化程序 BinaryFormatte](../code-quality/ca2300.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2301：在未先设置 BinaryFormatter.Binder 的情况下，请不要调用 BinaryFormatter.Deserialize](../code-quality/ca2301.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2302：在调用 BinaryFormatter.Deserialize 之前，确保设置 BinaryFormatter.Binder](../code-quality/ca2302.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2305：请勿使用不安全的反序列化程序 LosFormatter](../code-quality/ca2305.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2310：请勿使用不安全的反序列化程序 NetDataContractSerializer](../code-quality/ca2310.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2311：在未先设置 NetDataContractSerializer.Binder 的情况下，请不要反序列化](../code-quality/ca2311.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2312：确保在反序列化之前设置 NetDataContractSerializer.Binder](../code-quality/ca2312.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2315：请勿使用不安全的反序列化程序 ObjectStateFormatter](../code-quality/ca2315.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2321：请勿使用 SimpleTypeResolver 对 JavaScriptSerializer 进行反序列化](../code-quality/ca2321.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2322：确保在反序列化之前没有使用 SimpleTypeResolver 初始化 JavaScriptSerializer](../code-quality/ca2322.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2326：请勿使用 None 以外的 TypeNameHandling 值](../code-quality/ca2326.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2327：不要使用不安全的 JsonSerializerSettings](../code-quality/ca2327.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2328：确保 JsonSerializerSettings 是安全的](../code-quality/ca2328.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2329：不要使用不安全的配置反序列化 JsonSerializer](../code-quality/ca2329.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA2330：在反序列化时确保 JsonSerializer 具有安全配置](../code-quality/ca2330.md)|反序列化不受信任的数据时，不安全的反会很容易 攻击者可能会修改序列化的数据，使其包含意外类型，以注入具有恶意副作用的对象。|
|[CA3001：查看 SQL 注入漏洞的代码](../code-quality/ca3001.md)|使用不受信任的输入和 SQL 命令时，请注意 SQL 注入攻击。 SQL 注入攻击可以执行恶意的 SQL 命令，从而降低应用程序的安全性和完整性。|
|[CA3002：查看 XSS 漏洞的代码](../code-quality/ca3002.md)|当处理 web 请求中的不受信任输入时，请注意跨站点脚本（XSS）攻击。 XSS 攻击会将不受信任的输入注入原始 HTML 输出，使攻击者可以执行恶意脚本或恶意修改网页中的内容。|
|[CA3003:查看文件路径注入漏洞的代码](../code-quality/ca3003.md)|当处理 web 请求中的不受信任输入时，请注意在指定文件路径时使用用户控制输入。|
|[CA3004：查看信息泄露漏洞的代码](../code-quality/ca3004.md)|泄露异常信息可让攻击者深入了解应用程序的内部机制，从而帮助攻击者找到其他漏洞来利用这些漏洞。|
|[CA3006：查看进程命令注入漏洞的代码](../code-quality/ca3006.md)|使用不受信任的输入时，请注意命令注入攻击。 命令注入攻击可以在基础操作系统上执行恶意命令，从而危及服务器的安全和完整性。|
|[CA3007：查看公开重定向漏洞的代码](../code-quality/ca3007.md)|使用不受信任的输入时，请注意开放重定向漏洞。 攻击者可以利用开放的重定向漏洞来使用您的网站来获得合法 URL 的外观，但将不受信任的访问者重定向到仿冒网站或其他恶意网页。|
|[CA3008：查看 XPath 注入漏洞的代码](../code-quality/ca3008.md)|使用不受信任的输入时，请注意 XPath 注入式攻击。 使用不受信任输入构造 XPath 查询时，攻击者可能会恶意地操作查询以返回意外的结果，并可能会泄漏所查询的 XML 的内容。|
|[CA3009：查看 XML 注入漏洞的代码](../code-quality/ca3009.md)|使用不受信任的输入时，请注意 XML 注入攻击。|
|[CA3010：查看 XAML 注入漏洞的代码](../code-quality/ca3010.md)|使用不受信任的输入时，请注意 XAML 注入攻击。 XAML 是一种直接表示对象实例化和执行的标记语言。 这意味着在 XAML 中创建的元素可以与系统资源（例如，网络访问和文件系统 IO）交互。|
|[CA3011：查看 DLL 注入漏洞的代码](../code-quality/ca3011.md)|使用不受信任的输入时，请注意加载不受信任的代码。 如果你的 web 应用程序加载不受信任的代码，攻击者可能能够将恶意 Dll 注入到你的进程中并执行恶意代码。|
|[CA3012：查看正则表达式注入漏洞的代码](../code-quality/ca3012.md)|使用不受信任的输入时，请注意 regex 注入式攻击。 攻击者可以使用 regex 注入来恶意地修改正则表达式，以使 regex 与意外结果匹配，或使 regex 消耗过多的 CPU，导致拒绝服务攻击。|
|[CA3061：请勿按 URL 添加架构](../code-quality/ca3061.md)|不要使用 Add 方法的 unsafe 重载，因为这可能会导致危险的外部引用。|
|[CA3075:不安全的 DTD 处理](../code-quality/ca3075.md)|如果使用不安全的 DTDProcessing 实例或引用外部实体源，分析器可能会接受不受信任的输入并将敏感信息泄露给攻击者。|
|[CA3076:不安全的 XSLT 脚本执行](../code-quality/ca3076.md)|如果在 .NET 应用程序不安全地中执行可扩展样式表语言转换（XSLT），处理器可能会解析不受信任的 URI 引用，这些引用可能会将敏感信息泄露给攻击者，从而导致拒绝服务和跨站点攻击。|
|[CA3077:API 设计、XML 文档和 XML 文本读取器中的不安全处理](../code-quality/ca3077.md)|当设计派生自 XMLDocument 和 XMLTextReader 的 API 时，请注意 DtdProcessing。 当引用或解析外部实体源或设置 XML 中的不安全值时，使用不安全的 DTDProcessing 实例可能会导致信息泄露。|
|[CA3147:使用 ValidateAntiForgeryToken 标记谓词处理程序](../code-quality/ca3147.md)|设计 ASP.NET MVC 控制器时，请注意跨站点请求伪造攻击。 跨站点请求伪造攻击可以将经过身份验证的用户的恶意请求发送到 ASP.NET MVC 控制器。|
|[CA5122 P/Invoke 声明不应是安全关键的](../code-quality/ca5122.md)|当方法执行安全敏感性操作时，将被标记为 SecuritySafeCritical，但透明代码使用它们也是安全的。 透明代码决不能通过通过 P/Invoke 直接调用本机代码。 因此，将 P/Invoke 标记为安全关键将使透明代码无法调用它，并且会误导安全分析。|
|[CA5359:请勿禁用证书验证](../code-quality/ca5359.md)|证书可以帮助验证服务器的身份。 客户端应验证服务器证书，以确保将请求发送到目标服务器。 如果 Servicepointmanager.servercertificatevalidationcallback 始终返回 `true` ，则任何证书将通过验证。|
|[CA5360：不要调用反序列化中的危险方法](../code-quality/ca5360.md)|不受信任的反序列化是指使用不受信任的数据来滥用应用程序的逻辑，导致拒绝服务（DoS）攻击，甚至是在反序列化时执行任意代码时出现的漏洞。 当应用程序对其控制下的不受信任的数据进行反序列化时，恶意用户经常会滥用这些反序列化功能。 具体而言，就是在反序列化过程中调用危险方法。 成功的反反序列化攻击可能会允许攻击者发起攻击，如 DoS 攻击、身份验证绕过和远程代码执行。|
|[CA5361：不禁用 SChannel 使用强加密](../code-quality/ca5361.md)|将设置 `Switch.System.Net.DontEnableSchUseStrongCrypto` 为 `true` 受损传出传输层安全性（TLS）连接中使用的加密。 较弱的加密可能会危及应用程序与服务器之间通信的机密性，使攻击者更容易窃听敏感数据。|
|[CA5362:反序列化对象图中存在潜在引用循环](../code-quality/ca5362.md)|如果反序列化不受信任的数据，则处理反序列化对象图的任何代码都需要处理引用循环，而不会进入无限循环。 这包括作为反序列化回调一部分的代码和在反序列化完成后处理对象图的代码。 否则，攻击者可能会对包含引用周期的恶意数据执行拒绝服务攻击。|
|[CA5363：请勿禁用请求验证](../code-quality/ca5363.md)|请求验证是 ASP.NET 中的一项功能，用于检查 HTTP 请求并确定这些请求是否包含可能导致注入攻击（包括跨站点脚本）的潜在危险内容。|
|[CA5364：不使用已弃用的安全协议](../code-quality/ca5364.md)|传输层安全性（TLS）保护计算机之间的通信，最常见的是通过超文本传输协议（HTTPS）进行通信。 较早的 TLS 协议版本不如 TLS 1.2 和 TLS 1.3 安全，更有可能出现新的漏洞。 避免旧协议版本来最大程度地降低风险。|
|[CA5365:请勿禁用 HTTP 头检查](../code-quality/ca5365.md)|HTTP 标头检查启用在响应标头中找到的回车符和换行符（\r 和 \n）的编码。 这种编码有助于避免注入攻击，攻击者利用该应用程序回显了标头中包含的不受信任的数据。|
|[CA5366:将 XmlReader 用于数据集读取 XML](../code-quality/ca5366.md)|使用 <xref:System.Data.DataSet> 读取包含不受信任数据的 XML 可能会加载危险的外部引用，应使用 <xref:System.Xml.XmlReader> 具有安全解析程序或禁用 DTD 处理的进行限制。|
|[CA5367:请勿序列化具有 Pointer 字段的类型](../code-quality/ca5367.md)|此规则检查是否存在具有指针字段或属性的可序列化类。 无法序列化的成员可以是指针，如使用标记的静态成员或字段 <xref:System.NonSerializedAttribute> 。|
|[CA5368:针对派生自 Page 的类设置 ViewStateUserKey](../code-quality/ca5368.md)|设置 <xref:System.Web.UI.Page.ViewStateUserKey> 属性可帮助您阻止对应用程序的攻击，方法是允许您为个别用户分配视图状态变量的标识符，使攻击者无法使用该变量生成攻击。 否则，会出现跨站点请求伪造的漏洞。|
|[CA5369：将 XmlReader 用于反序列化](../code-quality/ca5369.md)|处理不受信任的 DTD 和 XML 架构可能会启用加载危险的外部引用，这应通过使用具有安全解析程序的 XmlReader 或禁用 DTD 和 XML 内联架构处理来限制。|
|[CA5370：将 XmlReader 用于验证读取器](../code-quality/ca5370.md)|处理不受信任的 DTD 和 XML 架构可能会启用加载危险的外部引用。 可以通过将 XmlReader 与安全解析程序结合使用，或者禁用 DTD 和 XML 内联架构处理来限制这种危险加载。|
|[CA5371：将 XmlReader 用于架构读取](../code-quality/ca5371.md)|处理不受信任的 DTD 和 XML 架构可能会启用加载危险的外部引用。 将 XmlReader 用于安全解析程序或 DTD 和 XML 内联架构处理将会限制这种情况。|
|[CA5372：将 XmlReader 用于 XPathDocument](../code-quality/ca5372.md)|处理来自不受信任数据的 XML 可能会加载危险的外部引用，这可以通过使用具有安全解析程序的 XmlReader 或禁用 DTD 处理来限制。|
|[CA5373：请勿使用已过时的密钥派生功能](../code-quality/ca5373.md)|此规则检测弱密钥派生方法和的调用 <xref:System.Security.Cryptography.PasswordDeriveBytes?displayProperty=fullName> `Rfc2898DeriveBytes.CryptDeriveKey` 。 <xref:System.Security.Cryptography.PasswordDeriveBytes?displayProperty=fullName>使用弱算法 PBKDF1。|
|[CA5374:请勿使用 XslTransform](../code-quality/ca5374.md)|此规则检查 <xref:System.Xml.Xsl.XslTransform?displayProperty=nameWithType> 是否在代码中实例化。 <xref:System.Xml.Xsl.XslTransform?displayProperty=nameWithType>现已过时，不应使用。|
|[CA5375：不使用帐户共享访问签名](../code-quality/ca5375.md)|帐户 SAS 可委派对 blob 容器、表、队列以及服务 SAS 不允许的文件共享上的读取、写入和删除操作的访问权限。 但是，它不支持容器级别的策略，并且具有较低的灵活性和对所授予权限的控制权限。 一旦恶意用户获得，您的存储帐户就会容易泄露。|
|[CA5376：使用 SharedAccessProtocol HttpsOnly](../code-quality/ca5376.md)|SAS 是不能以纯文本形式在 HTTP 上传输的敏感数据。|
|[CA5377：使用容器级别访问策略](../code-quality/ca5377.md)|容器级别的访问策略可以随时修改或撤消。 它提供了更大的灵活性并控制授予的权限。|
|[CA5378：不禁用 ServicePointManagerSecurityProtocols](../code-quality/ca5378.md)|用于 `Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols` 将 `true` Windows Communication FRAMEWORK （WCF）传输层安全性（TLS）连接限制为使用 TLS 1.0 的设置。 TLS 版本将不推荐使用。|
|[CA5379:请勿使用弱密钥派生功能算法](../code-quality/ca5379.md)|<xref:System.Security.Cryptography.Rfc2898DeriveBytes>类默认使用 <xref:System.Security.Cryptography.HashAlgorithmName.SHA1> 算法。 应指定要在具有 <xref:System.Security.Cryptography.HashAlgorithmName.SHA256> 或更高版本的构造函数的某些重载中使用的哈希算法。 请注意， <xref:System.Security.Cryptography.Rfc2898DeriveBytes.HashAlgorithm> 属性仅具有 `get` 访问器，没有 `overriden` 修饰符。|
|[CA5380：请勿将证书添加到根存储中](../code-quality/ca5380.md)|此规则检测将证书添加到 "受信任的根证书颁发机构" 证书存储中的代码。 默认情况下，"受信任的根证书颁发机构" 证书存储区配置为满足 Microsoft 根证书计划要求的一组公共 Ca。|
|[CA5381：请确保证书未添加到根存储中](../code-quality/ca5381.md)|此规则检测可能会将证书添加到 "受信任的根证书颁发机构" 证书存储中的代码。 默认情况下，"受信任的根证书颁发机构" 证书存储区使用满足 Microsoft 根证书计划要求的一组公共证书颁发机构（Ca）进行配置。|
|[CA5382:在 ASP.NET Core 中使用安全 Cookie](../code-quality/ca5382.md)|通过 HTTPS 提供的应用程序必须使用安全 cookie，这向浏览器指示该 cookie 只应使用传输层安全性（TLS）传输。|
|[CA5383:确保在 ASP.NET Core 中使用安全 Cookie](../code-quality/ca5383.md)|通过 HTTPS 提供的应用程序必须使用安全 cookie，这向浏览器指示该 cookie 只应使用传输层安全性（TLS）传输。|
|[CA5384:不使用数字签名算法(DSA)](../code-quality/ca5384.md)|DSA 是弱非对称加密算法。|
|[CA5385:设置具有足够密钥大小的 Rivest–Shamir–Adleman (RSA)算法](../code-quality/ca5385.md)|小于2048位的 RSA 密钥更容易受到暴力破解攻击。|
|[CA5386：避免对 SecurityProtocolType 值进行硬编码](../code-quality/ca5386.md)|传输层安全性（TLS）保护计算机之间的通信，最常见的是通过超文本传输协议（HTTPS）进行通信。 协议 1.1 1.0 版本不推荐使用，而 TLS 1.2 和 TLS 1.3 是最新的。 未来，TLS 1.2 和 TLS 1.3 可能已弃用。 若要确保应用程序的安全性，请避免硬编码协议版本，并以至少 .NET Framework v 4.7.1 为目标。|
|[CA5387:请勿使用迭代计数不足的弱密钥派生功能](../code-quality/ca5387.md)|此规则检查是否生成了的加密密钥 <xref:System.Security.Cryptography.Rfc2898DeriveBytes> ，迭代次数小于100000。 较高的迭代次数可帮助缓解字典攻击，尝试猜测生成的加密密钥。|
|[CA5388:使用弱密钥派生功能时，请确保迭代计数足够大](../code-quality/ca5388.md)|此规则检查是否生成的加密密钥 <xref:System.Security.Cryptography.Rfc2898DeriveBytes> 带有小于100000的迭代次数。 较高的迭代次数可帮助缓解字典攻击，尝试猜测生成的加密密钥。|
|[CA5389：请勿将存档项的路径添加到目标文件系统路径中](../code-quality/ca5389.md)|文件路径可以是相对路径，并且可能会导致文件系统在预期的文件系统目标路径外进行访问，从而导致恶意配置更改并通过 "等待" 等方法执行远程代码。|
|[CA5390:请勿编码加密密钥](../code-quality/ca5390.md)|若要成功使用对称算法，密钥必须仅对发送方和接收方是已知的。 当某个密钥是硬编码的，很容易发现它。 即使已编译的二进制文件，恶意用户也可以轻松地将其提取出来。 私钥泄露后，可以直接解密密码文本，而不会再对其进行保护。|
|[CA5391：使用 ASP.NET Core MVC 控制器中的防伪标记](../code-quality/ca5391.md)|处理 `POST` 、、 `PUT` `PATCH` 或 `DELETE` 请求而不验证防伪令牌可能易受到跨站点请求伪造攻击。 跨站点请求伪造攻击可以将经过身份验证的用户的恶意请求发送到 ASP.NET Core MVC 控制器。|
|[CA5392：将 DefaultDllImportSearchPaths 特性用于 P/Invoke](../code-quality/ca5392.md)|默认情况下，使用探测的 P/Invoke 函数包含 <xref:System.Runtime.InteropServices.DllImportAttribute> 多个目录，其中包含要加载的库的当前工作目录。 对于某些应用程序，这可能是一个安全问题，导致 DLL 劫持。|
|[CA5393：不使用 unsafe DllImportSearchPath 值](../code-quality/ca5393.md)|默认 DLL 搜索目录和程序集目录中可能存在恶意 DLL。 或者，根据应用程序的运行位置，应用程序目录中可能存在恶意的 DLL。|
|[CA5394:请勿使用不安全的随机性](../code-quality/ca5394.md)|使用加密弱伪随机数生成器可以允许攻击者预测将生成的安全敏感值。|
|[CA5395：缺少操作方法的 HttpVerb 属性](../code-quality/ca5395.md)|用于创建、编辑、删除或以其他方式修改数据的所有操作方法都需要通过跨站点请求伪造攻击的防伪属性进行保护。 执行 GET 操作应该是不会产生副作用的安全操作，并且不会修改您的持久数据。|
|[CA5396:将 HttpCookie 的 HttpOnly 设置为 true](../code-quality/ca5396.md)|作为深层防御措施，请确保将安全敏感的 HTTP cookie 标记为 HttpOnly。 这表明 web 浏览器应禁止脚本访问 cookie。 注入的恶意脚本是偷窃 cookie 的常见方法。|
|[CA5397:不使用已弃用的 SslProtocols 值](../code-quality/ca5397.md)|传输层安全性（TLS）保护计算机之间的通信，最常见的是通过超文本传输协议（HTTPS）进行通信。 较早的 TLS 协议版本不如 TLS 1.2 和 TLS 1.3 安全，更有可能出现新的漏洞。 避免旧协议版本来最大程度地降低风险。|
|[CA5398:避免硬编码的 SslProtocols 值](../code-quality/ca5398.md)|传输层安全性（TLS）保护计算机之间的通信，最常见的是通过超文本传输协议（HTTPS）进行通信。 协议 1.1 1.0 版本不推荐使用，而 TLS 1.2 和 TLS 1.3 是最新的。 未来，TLS 1.2 和 TLS 1.3 可能已弃用。 若要确保应用程序的安全性，请避免硬编码协议版本。|
|[CA5399:绝对禁用 HttpClient 证书吊销列表检查](../code-quality/ca5399.md)|吊销的证书不再受信任。 攻击者可以使用它来传递某些恶意数据或偷窃 HTTPS 通信中的敏感数据。|
|[CA5400:确保未禁用 HttpClient 证书吊销列表检查](../code-quality/ca5400.md)|吊销的证书不再受信任。 攻击者可以使用它来传递某些恶意数据或偷窃 HTTPS 通信中的敏感数据。|
|[CA5401:不要将 CreateEncryptor 与非默认 IV 结合使用](../code-quality/ca5401.md)|对称加密应始终使用不可重复的初始化向量来防止字典攻击。|
|[CA5402:将 CreateEncryptor 与默认 IV 结合使用](../code-quality/ca5402.md)|对称加密应始终使用不可重复的初始化向量来防止字典攻击。|
