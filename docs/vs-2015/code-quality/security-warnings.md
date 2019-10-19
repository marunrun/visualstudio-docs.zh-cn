---
title: 安全警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.securityrules
helpviewer_keywords:
- security [Visual Studio ALM], Enterprise Templates
- security warnings
- managed code analysis warnings, security warnings
- warnings, security
ms.assetid: 60d4e8ea-230a-494f-aa6a-b91db77540e4
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b5e30768ac6fa8c3c140156b94082bb2306efb51
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655204"
---
# <a name="security-warnings"></a>安全警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

安全警告支持更安全的库和应用程序。 这些警告帮助防止程序中出现安全漏洞。 如果你禁用其中的某个警告，你应当在代码中清楚标出原因，同时将你的开发项目通知指定的安全负责人。

## <a name="in-this-section"></a>本节内容

|规则|描述|
|----------|-----------------|
|[CA2100：检查 SQL 查询中是否有安全漏洞](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md)|一个方法使用按该方法的字符串参数生成的字符串设置 System.Data.IDbCommand.CommandText 属性。 此规则假定字符串参数中包含用户输入。 基于用户输入生成的 SQL 命令字符串易于受到 SQL 注入式攻击。|
|[CA2102：在常规处理程序中捕捉非 CLSCompliant 异常](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md)|程序集中未标以 RuntimeCompatibilityAttribute 或标以 RuntimeCompatibility(WrapNonExceptionThrows = false) 的某个成员包含一个处理 System.Exception 的 catch 块，而不包含紧跟其后的一般 catch 块。|
|[CA2103：检查命令性安全](../code-quality/ca2103-review-imperative-security.md)|某方法使用命令性安全，并且可能正在使用在请求处于活动状态时可以更改的状态信息或返回值来构造权限。 应尽可能使用声明性安全。|
|[CA2104：不要声明只读可变引用类型](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md)|外部可见类型包含外部可见的只读字段，该字段为可变的引用类型。 可变类型是实例数据可被修改的类型。|
|[CA2105：数组字段不应为只读](../code-quality/ca2105-array-fields-should-not-be-read-only.md)|向包含数组的字段应用 readonly（在 Visual Basic 中为 ReadOnly）修饰符时，无法将该字段更改为引用其他数组。 但是，可以更改在只读字段中存储的数组的元素。|
|[CA2106：保护断言](../code-quality/ca2106-secure-asserts.md)|某个方法断言权限，但不对调用方执行任何安全检查。 如果在不执行任何安全检查的情况下断言安全权限，则会在代码中留下可利用的安全漏洞。|
|[CA2107：检查 deny 权限和 permit only 权限的使用情况](../code-quality/ca2107-review-deny-and-permit-only-usage.md)|PermitOnly 方法和 CodeAccessPermission.Deny 安全操作只应由掌握 .NET Framework 高级安全知识的人员使用。 应当对使用这些安全操作的代码进行安全检查。|
|[CA2108：检查有关值类型的声明性安全](../code-quality/ca2108-review-declarative-security-on-value-types.md)|公共或受保护值类型受数据访问或链接要求保护。|
|[CA2109：检查可见的事件处理程序](../code-quality/ca2109-review-visible-event-handlers.md)|检测到公共事件处理方法或受保护事件处理方法。 除非绝对必要，否则不应公开事件处理方法。|
|[CA2111：指针应为不可见](../code-quality/ca2111-pointers-should-not-be-visible.md)|指针不是私有、内部或只读指针。 恶意代码可以更改指针的值，这样就有可能访问内存中的任意位置或导致应用程序或系统故障。|
|[CA2112：受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)|一个公共或受保护类型包含公共字段，并受链接要求保护。 如果代码可以访问受链接要求保护的类型的实例，则该代码不必满足此链接要求就可以访问该类型的字段。|
|[CA2114：方法安全性应是类型安全性的超集](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md)|一个方法不应同时有同一操作的方法级别和类型级别的声明性安全。|
|[CA2115：使用本机资源时调用 GC.KeepAlive](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)|该规则检测由于在非托管代码仍在使用非托管资源时终止该非托管资源而可能发生的错误。|
|[CA2116：APTCA 方法应只调用 APTCA 方法](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)|在完全受信任的程序集具有 APTCA (AllowPartiallyTrustedCallers) 特性时，如果该程序集执行另一个不允许部分受信任调用方的程序集中的代码，则可能存在安全漏洞。|
|[CA2117：APTCA 类型应只扩展 APTCA 基类型](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)|在完全受信任的程序集具有 APTCA (AllowPartiallyTrustedCallers) 特性时，如果程序集中的某个类型是从不允许部分受信任调用方的类型继承而来，则可能会产生安全漏洞。|
|[CA2118：检查 SuppressUnmanagedCodeSecurityAttribute 用法](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md)|SuppressUnmanagedCodeSecurityAttribute 为执行使用 COM 互操作或平台调用的非托管代码的成员更改默认的安全系统行为。 该特性主要用于提高性能；不过，提高性能的同时会显著增加安全风险。|
|[CA2119：密封满足私有接口的方法](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md)|可继承的公共类型为 internal（在 Visual Basic 中为 Friend）接口提供可重写的方法实现。 若要修复与此规则的冲突，请禁止方法在程序集外重写。|
|[CA2120：保护序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)|此类型的构造函数采用了 System.Runtime.Serialization.SerializationInfo 对象和 System.Runtime.Serialization.StreamingContext 对象（序列化构造函数的签名）。 此构造函数不受安全检查的保护，但类型中的一个或多个常规构造函数受保护。|
|[CA2121：静态构造函数应为私有](../code-quality/ca2121-static-constructors-should-be-private.md)|系统在创建第一个类型实例或引用任何静态成员之前调用静态构造函数。 如果静态构造函数不是私有，则系统以外的代码可以调用它。 根据构造函数中执行的操作，这可能导致意外行为。|
|[CA2122：不要使用链接请求间接公开方法](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)|公共或受保护成员具有链接要求，且由不执行任何安全检查的成员调用。 链接请求仅检查直接调用方的权限。|
|[CA2123：重写的链接请求应与基相同](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)|该规则将一个方法与其基方法（该基方法为另一个类型中的接口或虚方法）相匹配，然后比较两者的链接请求。 如果与此规则冲突，则恶意调用方只需调用不安全的方法，即可跳过该链接要求。|
|[CA2124：在外部 try 块中包装易受攻击的 finally 子句](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md)|公共或受保护方法中含有 try/finally 块。 finally 块似乎要重置安全状态，并且自身不包括在某个 finally 块中。|
|[CA2126：类型链接请求需要继承请求](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md)|一个公共的非密封类型受链接要求保护，并且具有可重写的方法。 类型和方法都不受继承要求保护。|
|[CA2136：成员不应有相互冲突的透明度注释](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|在完全透明的程序集中不能出现关键代码。 此规则分析完全透明的程序集在类型、字段和方法级别是否有任何 SecurityCritical 批注。|
|[CA2147：透明方法不得使用安全断言](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|此规则分析完全透明或混合透明/关键的程序集中的所有方法和类型，并标记 Assert 的任何声明性或命令性用法。|
|[CA2140：透明代码不得引用安全关键项](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|标有 SecurityTransparentAttribute 的方法调用标为 SecurityCritical 的非公共成员。 此规则分析混合透明/关键的程序集中的所有方法和类型，并标记透明代码中对未标为 SecurityTreatAsSafe 的非公共关键代码的任何调用。|

|[CA2130：安全关键常量应是透明的](../code-quality/ca2130-security-critical-constants-should-be-transparent.md)|未对常数值实施透明强制，因为编译器内联常数值以便在运行时不需要查找。 常数字段应为安全透明的，以便代码评审阅者不会假定透明代码不能访问常数。|
|-----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|[CA2131：安全关键类型不能参与类型等效](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md)|某个类型参与了类型等效性，该类型本身或该类型的成员或字段用 SecurityCriticalAttribute 特性标记。 对于任何关键的类型或包含参与类型等效的关键方法或字段的类型，将引发此规则。 当 CLR 检测到这样的类型时，在运行时将不会加载它并引发 TypeLoadException。 通常，仅在用户手动实现类型等效而不是通过依赖 tlbimp 和编译器进行类型等效时，才会触发此规则。|
|[CA2132：默认构造函数必须至少与基类型默认构造函数具有同样的关键性](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md)|具有 SecurityCriticalAttribute 的类型和成员无法供 Silverlight 应用程序代码使用。 安全关键类型和成员只能供 .NET Framework for Silverlight 类库中的受信任代码使用。 因为派生类中的某个公共或受保护构造必须有与其基类相同或更大的透明度，所以不能从标记为 SecurityCritical 的类派生应用程序中的类。|
|[CA2133：委托必须绑定到具有一致透明度的方法](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md)|将对一个具有以下特点的方法引发此警告：该方法将用 SecurityCriticalAttribute 标记的委托绑定到一个透明的或用 SecuritySafeCriticalAttribute 标记的方法。 还会对另一个具有以下特点的方法引发此警告：该方法将透明的或安全关键的委托绑定到一个关键方法。|
|[CA2134：在重写基方法时，方法必须保持一致的透明度](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md)|当用 SecurityCriticalAttribute 标记的方法重写一个透明的或用 SecuritySafeCriticalAttribute 标记的方法时，将引发此规则。 当一个透明的或用 SecuritySafeCriticalAttribute 标记的方法重写一个用 SecurityCriticalAttribute 标记的方法时，也会引发此规则。 该规则在重写虚方法或实现接口时应用。|
|[CA2135：级别 2 程序集不应包含 LinkDemand](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md)|在级别为 2 的安全规则集中已弃用 LinkDemand。 现在使用 SecurityCriticalAttribute 特性标记方法、类型和字段，而不是使用 LinkDemand 在实时 (JIT) 编译时进行强制安全检查。|
|[CA2136：成员不应有相互冲突的透明度注释](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|将透明特性从较大作用域的代码元素应用到较小作用域的元素。 具有较大作用域的代码元素的透明特性优于第一个元素中包含的代码元素的透明特性。 例如，用 SecurityCriticalAttribute 特性标记的类不能包含用 SecuritySafeCriticalAttribute 特性标记的方法。|
|[CA2137：透明方法必须仅包含可验证 IL](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md)|某个方法包含无法验证的代码或通过引用返回类型。 在尝试通过安全透明代码执行无法验证的 MSIL（Microsoft 中间语言）时将引发此规则。 但是，此规则不包含完整的 IL 验证程序，而是使用试探法来捕捉 MSIL 验证的大部分冲突。|
|[CA2138：透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md)|一个安全透明方法调用使用 SuppressUnmanagedCodeSecurityAttribute 特性标记的方法。|
|[CA2139：透明方法不能使用 HandleProcessCorruptingExceptions 特性](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md)|对于任何透明的并尝试通过使用 HandleProcessCorruptedStateExceptionsAttribute 特性处理进程损坏异常的方法，将引发此规则。 进程损坏异常属于异常的 CLR 版本 4.0 异常分类（例如，AccessViolationException）。 HandleProcessCorruptedStateExceptionsAttribute 特性只由安全关键方法使用，并且如果应用于透明的方法，则将被忽略。|
|[CA2140：透明代码不得引用安全关键项](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|用 SecurityCriticalAttribute 特性标记的代码元素是安全关键的。 透明方法不能使用安全关键元素。 如果透明类型尝试使用安全关键类型，则会引发 TypeAccessException、MethodAccessException 或 FieldAccessException。|
|[CA2141：透明方法不得满足 LinkDemand](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md)|安全透明方法调用未用 AllowPartiallyTrustedCallersAttribute (APTCA) 特性标记的程序集中的方法，或者安全透明方法满足某个类型或方法的 LinkDemand。|
|[CA2142：不应使用 LinkDemand 保护透明代码](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)|对于需要 LinkDemand 来访问它们的透明方法，将会引发此规则。 安全透明代码不应负责验证某个操作的安全，因此不应要求权限。|
|[CA2143：透明方法不应使用安全要求](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md)|安全透明代码不应负责验证某个操作的安全，因此不应要求权限。 安全透明代码应使用完整的需求来作出安全决策并且安全关键代码不应依赖透明代码以进行完全的请求。|
|[CA2144：透明代码不应从字节数组加载程序集](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md)|透明代码安全检查不像关键代码的安全检查一样全面，因为透明代码不能执行安全敏感的操作。 从字节数组中加载的程序集在不透明的代码中可能不会被注意到，并且该字节数组可能包含确实需要审核的关键或更重要的安全关键代码。|
|[CA2145：不应使用 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md)|用 SuppressUnmanagedCodeSecurityAttribute 特性修饰的方法有一个隐式的 LinkDemand 作用于调用它的任何方法。 此 LinkDemand 要求调用代码是关键安全的。 用 SecurityCriticalAttribute 特性标记使用 SuppressUnmanagedCodeSecurity 的方法使此要求对方法的调用方更加明显。|
|[CA2146：类型必须至少与其基类型和接口一样关键](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md)|当派生类型具有的安全透明特性与其基类型或实现的接口不是同样关键时，将引发此规则。 只有关键类型可以从关键基类型派生或实现关键接口，并且只有关键或关键安全类型可以从安全关键基类型派生或实现关键安全接口。|
|[CA2147：透明方法不得使用安全断言](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|标记为 SecurityTransparentAttribute 的代码未被授予足够的权限进行断言。|
|[CA2149：透明方法不得调入本机代码](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md)|对于直接调用到本机代码中（例如通过使用 P/Invoke）的任何透明方法，将引发此规则。 违反此规则会导致级别 2 透明度模型中的 MethodAccessException，以及级别 1 透明度模型中对 UnmanagedCode 的完全要求。|
|[CA2151：具有关键类型的字段应是安全关键的](../code-quality/ca2151-fields-with-critical-types-should-be-security-critical.md)|若要使用安全关键类型，引用该类型的代码必须是安全关键或安全可靠关键。 即使引用是间接的，也需如此。 因此，具有安全透明字段或安全可靠关键字段具有误导性，因为透明代码仍然无法访问该字段。|
|[CA5122 P/Invoke 声明不应为安全临界](../code-quality/ca5122-p-invoke-declarations-should-not-be-safe-critical.md)|当方法执行安全敏感性操作时，将被标记为 SecuritySafeCritical，但透明代码使用它们也是安全的。 透明代码决不能通过通过 P/Invoke 直接调用本机代码。 因此，将 P/Invoke 标记为安全关键将使透明代码无法调用它，并且会误导安全分析。|
|[CA2153：避免处理损坏状态异常](../code-quality/ca2153-avoid-handling-corrupted-state-exceptions.md)|[损坏状态异常 (CSE)](https://msdn.microsoft.com/magazine/dd419661.aspx) 指示进程中存在内存损坏。 如果攻击者可以将攻击放置到损坏的内存区域，则捕获它们（而非允许进程崩溃）可能导致安全漏洞。|
|[CA3075：不安全的 DTD 处理](../code-quality/ca3075-insecure-dtd-processing.md)|如果使用不安全的 DTDProcessing 实例或引用外部实体源，分析器可能会接受不受信任的输入并将敏感信息泄露给攻击者。|
|[CA3076：不安全的 XSLT 脚本执行](../code-quality/ca3076-insecure-xslt-script-execution.md)|如果在 .NET 应用程序中不安全地执行可扩展样式表语言转换 (XSLT)，处理器可能会解析不受信任的 URI 引用，这种引用会把敏感信息泄露给攻击者，从而导致拒绝服务和跨站点攻击。|
|[CA3077：API 设计、XML 文档和 XML 文本读取器中的不安全处理](../code-quality/ca3077-insecure-processing-in-api-design-xml-document-and-xml-text-reader.md)|当设计派生自 XMLDocument 和 XMLTextReader 的 API 时，请注意 DtdProcessing。  当引用或解析外部实体源或设置 XML 中的不安全值时，使用不安全的 DTDProcessing 实例可能会导致信息泄露。|
