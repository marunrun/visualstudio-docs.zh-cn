---
title: 托管代码的“基本更正规则”规则集
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 631f0daf-1d42-4c90-a7dc-1a6a9de64c93
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 6f895506d27c98daf9d69be1a2ea4db5fbe158b7
ms.sourcegitcommit: 034c503ae04e22cf840ccb9770bffd012e40fb2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305465"
---
# <a name="basic-correctness-rules-rule-set-for-managed-code"></a>托管代码的“基本更正规则”规则集

基本更正规则规则集重点介绍了使用框架 Api 时的逻辑错误和常见错误。 基本更正规则包括 "[托管建议规则](managed-recommended-rules-rule-set-for-managed-code.md)" 规则集中的规则。

下表介绍了 Microsoft 基本更正规则集中的所有规则。

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
|[CA2200](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)|再次引发以保留堆栈详细信息|
|[CA2202](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md)|不要多次释放对象|
|[CA2207](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)|以内联方式初始化值类型的静态字段|
|[CA2212](../code-quality/ca2212-do-not-mark-serviced-components-with-webmethod.md)|不要使用 WebMethod 标记服务组件|
|[CA2213](../code-quality/ca2213-disposable-fields-should-be-disposed.md)|应释放可释放的字段|
|[CA2214](../code-quality/ca2214-do-not-call-overridable-methods-in-constructors.md)|不要在构造函数中调用可重写的方法|
|[CA2216](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)|可释放类型应声明终结器|
|[CA2220](../code-quality/ca2220-finalizers-should-call-base-class-finalizer.md)|终结器应调用基类的终结器|
|[CA2229](../code-quality/ca2229-implement-serialization-constructors.md)|实现序列化构造函数|
|[CA2231](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)|重写 ValueType.Equals 时应重载相等运算符|
|[CA2232](../code-quality/ca2232-mark-windows-forms-entry-points-with-stathread.md)|使用 STAThread 标记 Windows 窗体的入口点|
|[CA2235](../code-quality/ca2235-mark-all-non-serializable-fields.md)|标记所有不可序列化的字段|
|[CA2236](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)|对 ISerializable 类型调用基类方法|
|[CA2237](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)|用 SerializableAttribute 标记 ISerializable 类型|
|[CA2238](../code-quality/ca2238-implement-serialization-methods-correctly.md)|正确实现序列化方法|
|[CA2240](../code-quality/ca2240-implement-iserializable-correctly.md)|正确实现 ISerializable|
|[CA2241](../code-quality/ca2241-provide-correct-arguments-to-formatting-methods.md)|为格式化方法提供正确的参数|
|[CA2242](../code-quality/ca2242-test-for-nan-correctly.md)|正确测试 NaN|
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
|[CA2205](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)|使用 Win32 API 的托管等效项|
|[CA2215](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)|Dispose 方法应调用基类释放|
|[CA2221](../code-quality/ca2221-finalizers-should-be-protected.md)|终结器应受到保护|
|[CA2222](../code-quality/ca2222-do-not-decrease-inherited-member-visibility.md)|不要递减继承成员的可见性|
|[CA2223](../code-quality/ca2223-members-should-differ-by-more-than-return-type.md)|成员不应只是返回类型不同|
|[CA2224](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)|重载相等运算符时重写 Equals 方法|
|[CA2226](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)|运算符应有对称重载|
|[CA2227](../code-quality/ca2227-collection-properties-should-be-read-only.md)|集合属性应为只读|
|[CA2239](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)|为可选字段提供反序列化方法|