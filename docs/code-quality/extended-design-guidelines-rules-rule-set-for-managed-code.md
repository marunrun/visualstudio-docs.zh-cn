---
title: 托管代码的“扩展的设计准则规则”规则集
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: a338caf2-b75d-4f23-a0f9-3024fa0bceac
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 8062ef99d3c1ad43b633e896617e95851a40930a
ms.sourcegitcommit: c025a5e2013c4955ca685092b13e887ce64aaf64
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91658589"
---
# <a name="extended-design-guidelines-rules-rule-set-for-managed-code"></a>托管代码的“扩展的设计准则规则”规则集

Microsoft 扩展的设计准则规则集对基本设计准则规则进行了扩展，以最大程度地提高所报告的可用性和可维护性问题。 特别强调的是命名准则。 如果你的项目包含库代码，或者如果你想要强制编写易于维护的代码，则应考虑包含此规则集。

扩展的设计准则规则包括 " [基本设计准则规则](../code-quality/basic-design-guideline-rules-rule-set-for-managed-code.md) " 规则集中的所有规则，其中包括 " [托管建议规则](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md) " 规则集中的规则。

下表介绍了 Microsoft 扩展的设计准则规则集中的所有规则。

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
|[CA1000](/dotnet/fundamentals/code-analysis/quality-rules/ca1000)|不要在泛型类型中声明静态成员|
|[CA1002](/dotnet/fundamentals/code-analysis/quality-rules/ca1002)|不要公开泛型列表|
|[CA1003](/dotnet/fundamentals/code-analysis/quality-rules/ca1003)|使用泛型事件处理程序实例|
|[CA1004](../code-quality/ca1004.md)|泛型方法应提供类型参数|
|[CA1005](/dotnet/fundamentals/code-analysis/quality-rules/ca1005)|避免泛型类型的参数过多|
|[CA1006](../code-quality/ca1006.md)|不要将泛型类型嵌套在成员签名中|
|[CA1007](../code-quality/ca1007.md)|在适用处使用泛型|
|[CA1008](/dotnet/fundamentals/code-analysis/quality-rules/ca1008)|枚举应具有零值|
|[CA1010](/dotnet/fundamentals/code-analysis/quality-rules/ca1010)|集合应实现泛型接口|
|[CA1011](../code-quality/ca1011.md)|考虑将基类型作为参数传递|
|[CA1012](/dotnet/fundamentals/code-analysis/quality-rules/ca1012)|抽象类型不应具有构造函数|
|[CA1013](../code-quality/ca1013.md)|重载加法方法和减法方法时重载相等运算符|
|[CA1014](/dotnet/fundamentals/code-analysis/quality-rules/ca1014)|用 CLSCompliantAttribute 标记程序集|
|[CA1017](/dotnet/fundamentals/code-analysis/quality-rules/ca1017)|用 ComVisibleAttribute 标记程序集|
|[CA1018](/dotnet/fundamentals/code-analysis/quality-rules/ca1018)|用 AttributeUsageAttribute 标记特性|
|[CA1019](/dotnet/fundamentals/code-analysis/quality-rules/ca1019)|定义特性参数的访问器|
|[CA1023](../code-quality/ca1023.md)|索引器不应是多维的|
|[CA1024](/dotnet/fundamentals/code-analysis/quality-rules/ca1024)|在适用处使用属性|
|[CA1025](../code-quality/ca1025.md)|用形参数组替换重复的实参|
|[CA1026](../code-quality/ca1026.md)|不应使用默认形参|
|[CA1027](/dotnet/fundamentals/code-analysis/quality-rules/ca1027)|用 FlagsAttribute 标记枚举|
|[CA1028](/dotnet/fundamentals/code-analysis/quality-rules/ca1028)|枚举存储应为 Int32|
|[CA1030](/dotnet/fundamentals/code-analysis/quality-rules/ca1030)|在适用处使用事件|
|[CA1031](/dotnet/fundamentals/code-analysis/quality-rules/ca1031)|不要捕捉一般异常类型|
|[CA1032](/dotnet/fundamentals/code-analysis/quality-rules/ca1032)|实现标准异常构造函数|
|[CA1034](/dotnet/fundamentals/code-analysis/quality-rules/ca1034)|嵌套类型不应是可见的|
|[CA1035](../code-quality/ca1035.md)|ICollection 实现含有强类型成员|
|[CA1036](/dotnet/fundamentals/code-analysis/quality-rules/ca1036)|重写可比较类型中的方法|
|[CA1038](../code-quality/ca1038.md)|枚举数应强类型化|
|[CA1039](../code-quality/ca1039.md)|列表已强类型化|
|[CA1041](/dotnet/fundamentals/code-analysis/quality-rules/ca1041)|提供 ObsoleteAttribute 消息|
|[CA1043](/dotnet/fundamentals/code-analysis/quality-rules/ca1043)|将整型或字符串参数用于索引器|
|[CA1044](/dotnet/fundamentals/code-analysis/quality-rules/ca1044)|属性不应是只写的|
|[CA1046](/dotnet/fundamentals/code-analysis/quality-rules/ca1046)|不要对引用类型重载相等运算符|
|[CA1047](/dotnet/fundamentals/code-analysis/quality-rules/ca1047)|不要在密封类型中声明受保护的成员|
|[CA1048](../code-quality/ca1048.md)|不要在密封类型中声明虚拟成员|
|[CA1050](/dotnet/fundamentals/code-analysis/quality-rules/ca1050)|在命名空间中声明类型|
|[CA1051](/dotnet/fundamentals/code-analysis/quality-rules/ca1051)|不要声明可见实例字段|
|[CA1052](/dotnet/fundamentals/code-analysis/quality-rules/ca1052)|应密封静态容器类型|
|[CA1053](/dotnet/fundamentals/code-analysis/quality-rules/ca1053)|静态容器类型不应具有构造函数|
|[CA1054](/dotnet/fundamentals/code-analysis/quality-rules/ca1054)|URI 参数不应为字符串|
|[CA1055](/dotnet/fundamentals/code-analysis/quality-rules/ca1055)|URI 返回值不应是字符串|
|[CA1056](/dotnet/fundamentals/code-analysis/quality-rules/ca1056)|URI 属性不应是字符串|
|[CA1057](../code-quality/ca1057.md)|字符串 URI 重载调用 System.Uri 重载|
|[CA1058](/dotnet/fundamentals/code-analysis/quality-rules/ca1058)|类型不应扩展某些基类型|
|[CA1059](../code-quality/ca1059.md)|成员不应公开某些具体类型|
|[CA1064](/dotnet/fundamentals/code-analysis/quality-rules/ca1064)|异常应该是公共的|
|[CA1500](../code-quality/ca1500.md)|变量名不应与字段名相同|
|[CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)|避免过度复杂|
|[CA1708](/dotnet/fundamentals/code-analysis/quality-rules/ca1708)|标识符应以大小写之外的差别进行区分|
|[CA1716](/dotnet/fundamentals/code-analysis/quality-rules/ca1716)|标识符不应与关键字冲突|
|[CA1801](/dotnet/fundamentals/code-analysis/quality-rules/ca1801)|检查未使用的参数|
|[CA1804](../code-quality/ca1804.md)|移除未使用的局部变量|
|[CA1809](../code-quality/ca1809.md)|避免过多的局部变量|
|[CA1810](/dotnet/fundamentals/code-analysis/quality-rules/ca1810)|以内联方式初始化引用类型的静态字段|
|[CA1811](../code-quality/ca1811.md)|避免使用未调用的私有代码|
|[CA1812](/dotnet/fundamentals/code-analysis/quality-rules/ca1812)|避免未实例化的内部类|
|[CA1813](/dotnet/fundamentals/code-analysis/quality-rules/ca1813)|避免使用非密封特性|
|[CA1814](/dotnet/fundamentals/code-analysis/quality-rules/ca1814)|与多维数组相比，首选使用交错数组|
|[CA1815](/dotnet/fundamentals/code-analysis/quality-rules/ca1815)|重写值类型上的 Equals 和相等运算符|
|[CA1819](/dotnet/fundamentals/code-analysis/quality-rules/ca1819)|属性不应返回数组|
|[CA1820](/dotnet/fundamentals/code-analysis/quality-rules/ca1820)|使用字符串长度测试是否有空字符串|
|[CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822)|将成员标记为 static|
|[CA1823](/dotnet/fundamentals/code-analysis/quality-rules/ca1823)|避免未使用的私有字段|
|[CA2201](/dotnet/fundamentals/code-analysis/quality-rules/ca2201)|不要引发保留的异常类型|
|[CA2205](../code-quality/ca2205.md)|使用 Win32 API 的托管等效项|
|[CA2208](/dotnet/fundamentals/code-analysis/quality-rules/ca2208)|正确实例化参数异常|
|[CA2211](/dotnet/fundamentals/code-analysis/quality-rules/ca2211)|非常量字段不应是可见的|
|[CA2217](/dotnet/fundamentals/code-analysis/quality-rules/ca2217)|不要使用 FlagsAttribute 标记枚举|
|[CA2219](/dotnet/fundamentals/code-analysis/quality-rules/ca2219)|在异常子句中不引发异常|
|[CA2221](../code-quality/ca2221.md)|终结器应受到保护|
|[CA2222](../code-quality/ca2222.md)|不要递减继承成员的可见性|
|[CA2223](../code-quality/ca2223.md)|成员不应只是返回类型不同|
|[CA2224](../code-quality/ca2224.md)|重载相等运算符时重写 Equals 方法|
|[CA2225](/dotnet/fundamentals/code-analysis/quality-rules/ca2225)|运算符重载具有命名的备用项|
|[CA2226](/dotnet/fundamentals/code-analysis/quality-rules/ca2226)|运算符应有对称重载|
|[CA2227](/dotnet/fundamentals/code-analysis/quality-rules/ca2227)|集合属性应为只读|
|[CA2230](../code-quality/ca2230.md)|对可变数量的参数使用 params|
|[CA2234](/dotnet/fundamentals/code-analysis/quality-rules/ca2234)|传递 System.Uri 对象，而不传递字符串|
|[CA2239](../code-quality/ca2239.md)|为可选字段提供反序列化方法|
|[CA1020](../code-quality/ca1020.md)|避免使用类型极少的命名空间|
|[CA1021](/dotnet/fundamentals/code-analysis/quality-rules/ca1021)|避免使用 out 参数|
|[CA1040](/dotnet/fundamentals/code-analysis/quality-rules/ca1040)|避免使用空接口|
|[CA1045](/dotnet/fundamentals/code-analysis/quality-rules/ca1045)|不要通过引用来传递类型|
|[CA1062](/dotnet/fundamentals/code-analysis/quality-rules/ca1062)|验证公共方法的参数|
|[CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501)|避免过度继承|
|[CA1504](../code-quality/ca1504.md)|检查令人误解的字段名|
|[CA1505](/dotnet/fundamentals/code-analysis/quality-rules/ca1505)|避免使用无法维护的代码|
|[CA1506](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)|避免过度类耦合度|
|[CA1700](/dotnet/fundamentals/code-analysis/quality-rules/ca1700)|不要命名“Reserved”枚举值|
|[CA1701](../code-quality/ca1701.md)|资源字符串组合词应采用正确的大小写|
|[CA1702](../code-quality/ca1702.md)|组合词应采用正确的大小写|
|[CA1703](../code-quality/ca1703.md)|资源字符串应正确拼写|
|[CA1704](../code-quality/ca1704.md)|标识符应正确拼写|
|[CA1707](/dotnet/fundamentals/code-analysis/quality-rules/ca1707)|标识符不应包含下划线|
|[CA1709](../code-quality/ca1709.md)|标识符的大小写应当正确|
|[CA1710](/dotnet/fundamentals/code-analysis/quality-rules/ca1710)|标识符应具有正确的后缀|
|[CA1711](/dotnet/fundamentals/code-analysis/quality-rules/ca1711)|标识符应采用正确的后缀|
|[CA1712](/dotnet/fundamentals/code-analysis/quality-rules/ca1712)|不要将类型名用作枚举值的前缀|
|[CA1713](/dotnet/fundamentals/code-analysis/quality-rules/ca1713)|事件不应具有 before 或 after 前缀|
|[CA1714](/dotnet/fundamentals/code-analysis/quality-rules/ca1714)|Flags 枚举应采用复数形式的名称|
|[CA1715](/dotnet/fundamentals/code-analysis/quality-rules/ca1715)|标识符应具有正确的前缀|
|[CA1717](/dotnet/fundamentals/code-analysis/quality-rules/ca1717)|只有 FlagsAttribute 枚举应采用复数形式的名称|
|[CA1719](../code-quality/ca1719.md)|参数名不应与成员名冲突|
|[CA1720](/dotnet/fundamentals/code-analysis/quality-rules/ca1720)|标识符不应包含类型名称|
|[CA1721](/dotnet/fundamentals/code-analysis/quality-rules/ca1721)|属性名不应与 get 方法冲突|
|[CA1722](../code-quality/ca1722.md)|标识符应采用正确的前缀|
|[CA1724](/dotnet/fundamentals/code-analysis/quality-rules/ca1724)|类型名不应与命名空间冲突|
|[CA1725](/dotnet/fundamentals/code-analysis/quality-rules/ca1725)|参数名应与基方法中的声明保持一致|
|[CA1726](../code-quality/ca1726.md)|使用首选词条|
|[CA2204](../code-quality/ca2204.md)|文字应正确拼写|
