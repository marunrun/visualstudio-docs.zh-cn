---
title: 托管代码的“扩展的更正规则”规则集
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 5b181f5b-6c7a-4e46-a783-360e1da427a0
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 96a0b43e6d300d3db425cb7a926d0196566d178b
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349639"
---
# <a name="extended-correctness-rules-rule-set-for-managed-code"></a>托管代码的“扩展的更正规则”规则集

Microsoft 扩展的正确性规则集可最大程度地提高代码分析报告的逻辑和框架使用错误。 对特定方案（如 COM 互操作性和移动应用程序）施加了额外的强调。 如果其中一个方案适用于你的项目或在项目中发现其他问题，则应考虑包含此规则集。

Microsoft 扩展的正确性规则集包括 "[基本更正规则](../code-quality/basic-correctness-rules-rule-set-for-managed-code.md)" 规则集中的规则，其中包含 "[托管建议规则](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md)" 规则集中的规则。

下表介绍了 Microsoft 扩展的正确性规则集中的所有规则。

|规则|描述|
|----------|-----------------|
|[CA1001](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)|具有可释放字段的类型应该是可释放的|
|[CA1009](../code-quality/ca1009-declare-event-handlers-correctly.md)|正确声明事件处理程序|
|[CA1016](../code-quality/ca1016-mark-assemblies-with-assemblyversionattribute.md)|用 AssemblyVersionAttribute 标记程序集|
|[CA1033](../code-quality/ca1033-interface-methods-should-be-callable-by-child-types.md)|接口方法应可由子类型调用|
|[CA1049](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)|拥有本机资源的类型应是可释放的|
|[CA1060](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)|将 P/Invoke 移动到 NativeMethods 类|
|[CA1061](../code-quality/ca1061-do-not-hide-base-class-methods.md)|不要隐藏基类方法|
|[CA1063](../code-quality/ca1063-implement-idisposable-correctly.md)|正确实现 IDisposable|
|[CA1065](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)|不要在意外的位置引发异常|
|[CA1301](../code-quality/ca1301-avoid-duplicate-accelerators.md)|避免快捷键重复|
|[CA1400](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)|P/Invoke 入口点应该存在|
|[CA1401](../code-quality/ca1401-p-invokes-should-not-be-visible.md)|P/Invokes 应该是不可见的|
|[CA1403](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)|自动布局类型不应对 COM 可见|
|[CA1404](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md)|紧接在 P/Invoke 之后调用 GetLastError|
|[CA1405](../code-quality/ca1405-com-visible-type-base-types-should-be-com-visible.md)|COM 可见类型的基类型应对 COM 可见|
|[CA1410](../code-quality/ca1410-com-registration-methods-should-be-matched.md)|应对 COM 注册方法进行匹配|
|[CA1415](../code-quality/ca1415-declare-p-invokes-correctly.md)|正确声明 P/Invoke|
|[CA1821](../code-quality/ca1821.md)|移除空终结器|
|[CA1900](../code-quality/ca1900-value-type-fields-should-be-portable.md)|值类型字段应为可移植字段|
|[CA1901](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)|P/Invoke 声明应为可移植声明|
|[CA2002](../code-quality/ca2002-do-not-lock-on-objects-with-weak-identity.md)|不要锁定具有弱标识的对象|
|[CA2100](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md)|检查 SQL 查询是否存在安全漏洞|
|[CA2101](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)|指定对 P/Invoke 字符串参数进行封送处理|
|[CA2108](../code-quality/ca2108-review-declarative-security-on-value-types.md)|检查有关值类型的声明性安全|
|[CA2111](../code-quality/ca2111-pointers-should-not-be-visible.md)|指针应为不可见|
|[CA2112](../code-quality/ca2112-secured-types-should-not-expose-fields.md)|受保护的类型不应公开字段|
|[CA2114](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md)|方法安全性应是类型安全性的超集|
|[CA2116](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)|APTCA 方法应只调用 APTCA 方法|
|[CA2117](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)|APTCA 类型应只扩展 APTCA 基类型|
|[CA2122](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)|不要使用链接请求间接公开方法|
|[CA2123](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)|重写链接请求应与基相同|
|[CA2124](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md)|在外部 try 块中包装易受攻击的 finally 子句|
|[CA2126](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md)|类型链接请求需要继承请求|
|[CA2131](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md)|安全关键类型不能参与类型等效|
|[CA2132](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md)|默认构造函数必须至少与基类型默认构造函数一样关键|
|[CA2133](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md)|委托必须绑定到具有一致透明度的方法|
|[CA2134](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md)|在重写基方法时，方法必须保持一致的透明度|
|[CA2137](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md)|透明方法只能包含可验证的 IL|
|[CA2138](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md)|透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法|
|[CA2140](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|透明代码不得引用安全关键项|
|[CA2141](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md)|透明方法不得满足 LinkDemand|
|[CA2146](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md)|类型必须至少与其基类型和接口一样关键|
|[CA2147](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|透明方法不得使用安全断言|
|[CA2149](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md)|透明方法不得调入本机代码|
|[CA2200](../code-quality/ca2200.md)|再次引发以保留堆栈详细信息|
|[CA2202](../code-quality/ca2202.md)|不要多次释放对象|
|[CA2207](../code-quality/ca2207.md)|以内联方式初始化值类型的静态字段|
|[CA2212](../code-quality/ca2212.md)|不要使用 WebMethod 标记服务组件|
|[CA2213](../code-quality/ca2213.md)|应释放可释放的字段|
|[CA2214](../code-quality/ca2214.md)|不要在构造函数中调用可重写的方法|
|[CA2216](../code-quality/ca2216.md)|可释放类型应声明终结器|
|[CA2220](../code-quality/ca2220.md)|终结器应调用基类的终结器|
|[CA2229](../code-quality/ca2229.md)|实现序列化构造函数|
|[CA2231](../code-quality/ca2231.md)|重写 ValueType.Equals 时应重载相等运算符|
|[CA2232](../code-quality/ca2232.md)|使用 STAThread 标记 Windows 窗体的入口点|
|[CA2235](../code-quality/ca2235.md)|标记所有不可序列化的字段|
|[CA2236](../code-quality/ca2236.md)|对 ISerializable 类型调用基类方法|
|[CA2237](../code-quality/ca2237.md)|用 SerializableAttribute 标记 ISerializable 类型|
|[CA2238](../code-quality/ca2238.md)|正确实现序列化方法|
|[CA2240](../code-quality/ca2240.md)|正确实现 ISerializable|
|[CA2241](../code-quality/ca2241.md)|为格式化方法提供正确的参数|
|[CA2242](../code-quality/ca2242.md)|正确测试 NaN|
|[CA1008](../code-quality/ca1008-enums-should-have-zero-value.md)|枚举应具有零值|
|[CA1013](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)|重载加法方法和减法方法时重载相等运算符|
|[CA1303](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)|请不要将文本作为本地化参数传递|
|[CA1308](../code-quality/ca1308-normalize-strings-to-uppercase.md)|将字符串规范化为大写|
|[CA1806](../code-quality/ca1806.md)|不要忽略方法结果|
|[CA1816](../code-quality/ca1816.md)|正确调用 GC.SuppressFinalize|
|[CA1819](../code-quality/ca1819.md)|属性不应返回数组|
|[CA1820](../code-quality/ca1820.md)|使用字符串长度测试是否有空字符串|
|[CA1903](../code-quality/ca1903-use-only-api-from-targeted-framework.md)|仅使用目标框架中的 API|
|[CA2004](../code-quality/ca2004-remove-calls-to-gc-keepalive.md)|移除对 GC.KeepAlive 的调用|
|[CA2006](../code-quality/ca2006-use-safehandle-to-encapsulate-native-resources.md)|使用 SafeHandle 封装本机资源|
|[CA2102](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md)|在常规处理程序中捕捉非 CLSCompliant 异常|
|[CA2104](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md)|不要声明只读可变引用类型|
|[CA2105](../code-quality/ca2105-array-fields-should-not-be-read-only.md)|数组字段不应为只读|
|[CA2106](../code-quality/ca2106-secure-asserts.md)|保护断言|
|[CA2115](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)|使用本机资源时调用 GC.KeepAlive|
|[CA2119](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md)|密封满足私有接口的方法|
|[CA2120](../code-quality/ca2120-secure-serialization-constructors.md)|保护序列化构造函数|
|[CA2121](../code-quality/ca2121-static-constructors-should-be-private.md)|静态构造函数应为私有|
|[CA2130](../code-quality/ca2130-security-critical-constants-should-be-transparent.md)|安全关键常量应是透明的|
|[CA2205](../code-quality/ca2205.md)|使用 Win32 API 的托管等效项|
|[CA2215](../code-quality/ca2215.md)|Dispose 方法应调用基类释放|
|[CA2221](../code-quality/ca2221.md)|终结器应受到保护|
|[CA2222](../code-quality/ca2222.md)|不要递减继承成员的可见性|
|[CA2223](../code-quality/ca2223.md)|成员不应只是返回类型不同|
|[CA2224](../code-quality/ca2224.md)|重载相等运算符时重写 Equals 方法|
|[CA2226](../code-quality/ca2226.md)|运算符应有对称重载|
|[CA2227](../code-quality/ca2227.md)|集合属性应为只读|
|[CA2239](../code-quality/ca2239.md)|为可选字段提供反序列化方法|
|[CA1032](../code-quality/ca1032-implement-standard-exception-constructors.md)|实现标准异常构造函数|
|[CA1054](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)|URI 参数不应为字符串|
|[CA1055](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)|URI 返回值不应是字符串|
|[CA1056](../code-quality/ca1056-uri-properties-should-not-be-strings.md)|URI 属性不应是字符串|
|[CA1057](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)|字符串 URI 重载调用 System.Uri 重载|
|[CA1402](../code-quality/ca1402-avoid-overloads-in-com-visible-interfaces.md)|避免在 COM 可见接口中进行重载|
|[CA1406](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md)|避免对 Visual Basic 6 客户端使用 Int64 参数|
|[CA1407](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)|避免在 COM 可见类型中使用静态成员|
|[CA1408](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)|请不要使用 AutoDual ClassInterfaceType|
|[CA1409](../code-quality/ca1409-com-visible-types-should-be-creatable.md)|COM 可见类型应该是可创建的|
|[CA1411](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)|COM 注册方法应该是不可见的|
|[CA1412](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)|将 ComSource 接口标记为 IDispatch|
|[CA1413](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)|避免在 COM 可见值类型中使用非公共字段|
|[CA1414](../code-quality/ca1414-mark-boolean-p-invoke-arguments-with-marshalas.md)|用 MarshalAs 标记布尔型 P/Invoke 参数|
|[CA1600](../code-quality/ca1600-do-not-use-idle-process-priority.md)|不要使用 Idle 进程优先级|
|[CA1601](../code-quality/ca1601-do-not-use-timers-that-prevent-power-state-changes.md)|不要使用阻止电源状态更改的计时器|
|[CA1824](../code-quality/ca1824.md)|用 NeutralResourcesLanguageAttribute 标记程序集|
|[CA2001](../code-quality/ca2001-avoid-calling-problematic-methods.md)|避免调用有问题的方法|
|[CA2003](../code-quality/ca2003-do-not-treat-fibers-as-threads.md)|不要将纤程视为线程|
|[CA2135](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md)|级别 2 程序集不应包含 LinkDemand|
|[CA2136](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|成员不应具有冲突的透明度批注|
|[CA2139](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md)|透明方法不能使用 HandleProcessCorruptingExceptions 特性|
|[CA2142](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)|不应使用 LinkDemand 保护透明代码|
|[CA2143](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md)|透明方法不应使用安全请求|
|[CA2144](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md)|透明代码不应从字节数组加载程序集|
|[CA2145](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md)|不应使用 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法|
|[CA2204](../code-quality/ca2204.md)|文字应正确拼写|
|[CA2211](../code-quality/ca2211.md)|非常量字段不应是可见的|
|[CA2217](../code-quality/ca2217.md)|不要使用 FlagsAttribute 标记枚举|
|[CA2218](../code-quality/ca2218.md)|重写 Equals 时重写 GetHashCode|
|[CA2219](../code-quality/ca2219.md)|在异常子句中不引发异常|
|[CA2225](../code-quality/ca2225.md)|运算符重载具有命名的备用项|
|[CA2228](../code-quality/ca2228.md)|不要发行未发布的资源格式|
|[CA2230](../code-quality/ca2230.md)|对可变数量的参数使用 params|
|[CA2233](../code-quality/ca2233.md)|运算不应溢出|
|[CA2234](../code-quality/ca2234.md)|传递 System.Uri 对象，而不传递字符串|
|[CA2243](../code-quality/ca2243.md)|特性字符串文本应正确分析|