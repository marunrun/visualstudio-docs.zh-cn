---
title: 托管代码的“基本更正规则”规则集
ms.date: 11/04/2016
description: 了解 Visual Studio 中的 "基本更正规则" 规则集，其中重点介绍了逻辑错误和常见的框架 API 错误。 请参阅规则说明。
ms.custom: SEO-VS-2020
ms.topic: reference
ms.assetid: 631f0daf-1d42-4c90-a7dc-1a6a9de64c93
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 532cab657403cf8761d2b53304131b70a951a7ff
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94348484"
---
# <a name="basic-correctness-rules-rule-set-for-managed-code"></a>托管代码的“基本更正规则”规则集

基本更正规则规则集重点介绍了使用框架 Api 时的逻辑错误和常见错误。 基本更正规则包括 " [托管建议规则](managed-recommended-rules-rule-set-for-managed-code.md) " 规则集中的规则。

下表介绍了 Microsoft 基本更正规则集中的所有规则。

|规则|描述|
|----------|-----------------|
|[CA1001](/dotnet/fundamentals/code-analysis/quality-rules/ca1001)|具有可释放字段的类型应该是可释放的|
|[CA1009](../code-quality/ca1009.md)|正确声明事件处理程序|
|[CA1016](/dotnet/fundamentals/code-analysis/quality-rules/ca1016)|用 AssemblyVersionAttribute 标记程序集|
|[CA1033](/dotnet/fundamentals/code-analysis/quality-rules/ca1033)|接口方法应可由子类型调用|
|[CA1049](../code-quality/ca1049.md)|拥有本机资源的类型应是可释放的|
|[CA1060](/dotnet/fundamentals/code-analysis/quality-rules/ca1060)|将 P/Invoke 移动到 NativeMethods 类|
|[CA1061](/dotnet/fundamentals/code-analysis/quality-rules/ca1061)|不要隐藏基类方法|
|[CA1063](/dotnet/fundamentals/code-analysis/quality-rules/ca1063)|正确实现 IDisposable|
|[CA1065](/dotnet/fundamentals/code-analysis/quality-rules/ca1065)|不要在意外的位置引发异常|
|[CA1301](../code-quality/ca1301.md)|避免快捷键重复|
|[CA1400](../code-quality/ca1400.md)|P/Invoke 入口点应该存在|
|[CA1401](/dotnet/fundamentals/code-analysis/quality-rules/ca1401)|P/Invokes 应该是不可见的|
|[CA1403](../code-quality/ca1403.md)|自动布局类型不应对 COM 可见|
|[CA1404](../code-quality/ca1404.md)|紧接在 P/Invoke 之后调用 GetLastError|
|[CA1405](../code-quality/ca1405.md)|COM 可见类型的基类型应对 COM 可见|
|[CA1410](../code-quality/ca1410.md)|应对 COM 注册方法进行匹配|
|[CA1415](../code-quality/ca1415.md)|正确声明 P/Invoke|
|[CA1821](/dotnet/fundamentals/code-analysis/quality-rules/ca1821)|移除空终结器|
|[CA1900](../code-quality/ca1900.md)|值类型字段应为可移植字段|
|[CA1901](../code-quality/ca1901.md)|P/Invoke 声明应为可移植声明|
|[CA2002](/dotnet/fundamentals/code-analysis/quality-rules/ca2002)|不要锁定具有弱标识的对象|
|[CA2100](/dotnet/fundamentals/code-analysis/quality-rules/ca2100)|检查 SQL 查询是否存在安全漏洞|
|[CA2101](/dotnet/fundamentals/code-analysis/quality-rules/ca2101)|指定对 P/Invoke 字符串参数进行封送处理|
|[CA2108](../code-quality/ca2108.md)|检查有关值类型的声明性安全|
|[CA2111](../code-quality/ca2111.md)|指针应为不可见|
|[CA2112](../code-quality/ca2112.md)|受保护的类型不应公开字段|
|[CA2114](../code-quality/ca2114.md)|方法安全性应是类型安全性的超集|
|[CA2116](../code-quality/ca2116.md)|APTCA 方法应只调用 APTCA 方法|
|[CA2117](../code-quality/ca2117.md)|APTCA 类型应只扩展 APTCA 基类型|
|[CA2122](../code-quality/ca2122.md)|不要使用链接请求间接公开方法|
|[CA2123](../code-quality/ca2123.md)|重写链接请求应与基相同|
|[CA2124](../code-quality/ca2124.md)|在外部 try 块中包装易受攻击的 finally 子句|
|[CA2126](../code-quality/ca2126.md)|类型链接请求需要继承请求|
|[CA2131](../code-quality/ca2131.md)|安全关键类型不能参与类型等效|
|[CA2132](../code-quality/ca2132.md)|默认构造函数必须至少与基类型默认构造函数一样关键|
|[CA2133](../code-quality/ca2133.md)|委托必须绑定到具有一致透明度的方法|
|[CA2134](../code-quality/ca2134.md)|在重写基方法时，方法必须保持一致的透明度|
|[CA2137](../code-quality/ca2137.md)|透明方法只能包含可验证的 IL|
|[CA2138](../code-quality/ca2138.md)|透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法|
|[CA2140](../code-quality/ca2140.md)|透明代码不得引用安全关键项|
|[CA2141](../code-quality/ca2141.md)|透明方法不得满足 LinkDemand|
|[CA2146](../code-quality/ca2146.md)|类型必须至少与其基类型和接口一样关键|
|[CA2147](../code-quality/ca2147.md)|透明方法不得使用安全断言|
|[CA2149](../code-quality/ca2149.md)|透明方法不得调入本机代码|
|[CA2200](/dotnet/fundamentals/code-analysis/quality-rules/ca2200)|再次引发以保留堆栈详细信息|
|[CA2202](../code-quality/ca2202.md)|不要多次释放对象|
|[CA2207](/dotnet/fundamentals/code-analysis/quality-rules/ca2207)|以内联方式初始化值类型的静态字段|
|[CA2212](../code-quality/ca2212.md)|不要使用 WebMethod 标记服务组件|
|[CA2213](/dotnet/fundamentals/code-analysis/quality-rules/ca2213)|应释放可释放的字段|
|[CA2214](/dotnet/fundamentals/code-analysis/quality-rules/ca2214)|不要在构造函数中调用可重写的方法|
|[CA2216](/dotnet/fundamentals/code-analysis/quality-rules/ca2216)|可释放类型应声明终结器|
|[CA2220](../code-quality/ca2220.md)|终结器应调用基类的终结器|
|[CA2229](/dotnet/fundamentals/code-analysis/quality-rules/ca2229)|实现序列化构造函数|
|[CA2231](/dotnet/fundamentals/code-analysis/quality-rules/ca2231)|重写 ValueType.Equals 时应重载相等运算符|
|[CA2232](../code-quality/ca2232.md)|使用 STAThread 标记 Windows 窗体的入口点|
|[CA2235](/dotnet/fundamentals/code-analysis/quality-rules/ca2235)|标记所有不可序列化的字段|
|[CA2236](../code-quality/ca2236.md)|对 ISerializable 类型调用基类方法|
|[CA2237](/dotnet/fundamentals/code-analysis/quality-rules/ca2237)|用 SerializableAttribute 标记 ISerializable 类型|
|[CA2238](../code-quality/ca2238.md)|正确实现序列化方法|
|[CA2240](../code-quality/ca2240.md)|正确实现 ISerializable|
|[CA2241](/dotnet/fundamentals/code-analysis/quality-rules/ca2241)|为格式化方法提供正确的参数|
|[CA2242](/dotnet/fundamentals/code-analysis/quality-rules/ca2242)|正确测试 NaN|
|[CA1008](/dotnet/fundamentals/code-analysis/quality-rules/ca1008)|枚举应具有零值|
|[CA1013](../code-quality/ca1013.md)|重载加法方法和减法方法时重载相等运算符|
|[CA1303](/dotnet/fundamentals/code-analysis/quality-rules/ca1303)|请不要将文本作为本地化参数传递|
|[CA1308](/dotnet/fundamentals/code-analysis/quality-rules/ca1308)|将字符串规范化为大写|
|[CA1806](/dotnet/fundamentals/code-analysis/quality-rules/ca1806)|不要忽略方法结果|
|[CA1816](/dotnet/fundamentals/code-analysis/quality-rules/ca1816)|正确调用 GC.SuppressFinalize|
|[CA1819](/dotnet/fundamentals/code-analysis/quality-rules/ca1819)|属性不应返回数组|
|[CA1820](/dotnet/fundamentals/code-analysis/quality-rules/ca1820)|使用字符串长度测试是否有空字符串|
|[CA1903](../code-quality/ca1903.md)|仅使用目标框架中的 API|
|[CA2004](../code-quality/ca2004.md)|移除对 GC.KeepAlive 的调用|
|[CA2006](../code-quality/ca2006.md)|使用 SafeHandle 封装本机资源|
|[CA2102](../code-quality/ca2102.md)|在常规处理程序中捕捉非 CLSCompliant 异常|
|[CA2104](../code-quality/ca2104.md)|不要声明只读可变引用类型|
|[CA2105](../code-quality/ca2105.md)|数组字段不应为只读|
|[CA2106](../code-quality/ca2106.md)|保护断言|
|[CA2115](../code-quality/ca2115.md)|使用本机资源时调用 GC.KeepAlive|
|[CA2119](/dotnet/fundamentals/code-analysis/quality-rules/ca2119)|密封满足私有接口的方法|
|[CA2120](../code-quality/ca2120.md)|保护序列化构造函数|
|[CA2121](../code-quality/ca2121.md)|静态构造函数应为私有|
|[CA2130](../code-quality/ca2130.md)|安全关键常量应是透明的|
|[CA2205](../code-quality/ca2205.md)|使用 Win32 API 的托管等效项|
|[CA2215](/dotnet/fundamentals/code-analysis/quality-rules/ca2215)|Dispose 方法应调用基类释放|
|[CA2221](../code-quality/ca2221.md)|终结器应受到保护|
|[CA2222](../code-quality/ca2222.md)|不要递减继承成员的可见性|
|[CA2223](../code-quality/ca2223.md)|成员不应只是返回类型不同|
|[CA2224](../code-quality/ca2224.md)|重载相等运算符时重写 Equals 方法|
|[CA2226](/dotnet/fundamentals/code-analysis/quality-rules/ca2226)|运算符应有对称重载|
|[CA2227](/dotnet/fundamentals/code-analysis/quality-rules/ca2227)|集合属性应为只读|
|[CA2239](../code-quality/ca2239.md)|为可选字段提供反序列化方法|
