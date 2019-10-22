---
title: 托管代码的 "安全规则" 规则集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 564aeac6-03fa-41b0-b655-88179f0ab01b
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 66d1c3feb33ae1a42478f7742fb0491bff3441e2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72605429"
---
# <a name="security-rules-rule-set-for-managed-code"></a>托管代码的“安全规则”规则集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你应包括 Microsoft 安全规则规则集，以最大程度地提高报告的潜在安全问题的数量。

|规则|描述|
|----------|-----------------|
|[CA2100](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md)|检查 SQL 查询是否存在安全漏洞|
|[CA2102](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md)|在常规处理程序中捕捉非 CLSCompliant 异常|
|[CA2103](../code-quality/ca2103-review-imperative-security.md)|检查命令性安全|
|[CA2104](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md)|不要声明只读可变引用类型|
|[CA2105](../code-quality/ca2105-array-fields-should-not-be-read-only.md)|数组字段不应为只读|
|[CA2106](../code-quality/ca2106-secure-asserts.md)|保护断言|
|[CA2107](../code-quality/ca2107-review-deny-and-permit-only-usage.md)|检查 deny 权限和 permit only 权限的使用情况|
|[CA2108](../code-quality/ca2108-review-declarative-security-on-value-types.md)|检查有关值类型的声明性安全|
|[CA2109](../code-quality/ca2109-review-visible-event-handlers.md)|检查可见的事件处理程序|
|[CA2111](../code-quality/ca2111-pointers-should-not-be-visible.md)|指针应为不可见|
|[CA2112](../code-quality/ca2112-secured-types-should-not-expose-fields.md)|受保护的类型不应公开字段|
|[CA2114](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md)|方法安全性应是类型安全性的超集|
|[CA2115](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)|使用本机资源时调用 GC.KeepAlive|
|[CA2116](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)|APTCA 方法应只调用 APTCA 方法|
|[CA2117](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)|APTCA 类型应只扩展 APTCA 基类型|
|[CA2118](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md)|检查 SuppressUnmanagedCodeSecurityAttribute 用法|
|[CA2119](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md)|密封满足私有接口的方法|
|[CA2120](../code-quality/ca2120-secure-serialization-constructors.md)|保护序列化构造函数|
|[CA2121](../code-quality/ca2121-static-constructors-should-be-private.md)|静态构造函数应为私有|
|[CA2122](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)|不要使用链接请求间接公开方法|
|[CA2123](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)|重写链接请求应与基相同|
|[CA2124](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md)|在外部 try 块中包装易受攻击的 finally 子句|
|[CA2126](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md)|类型链接请求需要继承请求|
|[CA2130](../code-quality/ca2130-security-critical-constants-should-be-transparent.md)|安全关键常量应是透明的|
|[CA2131](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md)|安全关键类型不能参与类型等效|
|[CA2132](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md)|默认构造函数必须至少与基类型默认构造函数一样关键|
|[CA2133](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md)|委托必须绑定到具有一致透明度的方法|
|[CA2134](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md)|在重写基方法时，方法必须保持一致的透明度|
|[CA2135](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md)|级别 2 程序集不应包含 LinkDemand|
|[CA2136](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|成员不应具有冲突的透明度批注|
|[CA2137](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md)|透明方法只能包含可验证的 IL|
|[CA2138](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md)|透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法|
|[CA2139](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md)|透明方法不能使用 HandleProcessCorruptingExceptions 特性|
|[CA2140](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|透明代码不得引用安全关键项|
|[CA2141](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md)|透明方法不得满足 LinkDemand|
|[CA2142](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)|不应使用 LinkDemand 保护透明代码|
|[CA2143](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md)|透明方法不应使用安全请求|
|[CA2144](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md)|透明代码不应从字节数组加载程序集|
|[CA2145](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md)|不应使用 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法|
|[CA2146](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md)|类型必须至少与其基类型和接口一样关键|
|[CA2147](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|透明方法不得使用安全断言|
|[CA2149](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md)|透明方法不得调入本机代码|
|[CA2210](../code-quality/ca2210-assemblies-should-have-valid-strong-names.md)|程序集应具有有效的强名称|
