---
title: 托管代码的“托管建议规则”规则集
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 1d1160f8-4e51-4e70-99cd-82ad10ee7b32
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 2c0b5fb735309e87dab31631d088f14ac9fa9d41
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349523"
---
# <a name="managed-recommended-rules-rule-set-for-managed-code"></a>托管代码的“托管建议规则”规则集

使用 "Microsoft 托管建议规则" 规则集来重点关注托管代码中最关键的问题，包括潜在的安全漏洞、应用程序崩溃和其他重要的逻辑和设计错误。 此规则集包括 "[托管最小规则](managed-minimum-rules-rule-set-for-managed-code.md)" 规则集中的所有规则。

在你为项目创建的任何自定义规则集中包含此规则集。

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