---
title: FxCop 规则端口状态
ms.date: 05/21/2019
description: 了解已经移植到 Visual Studio 中的 FxCop 分析器的静态代码分析规则。 查看移植规则和移植更新的资源。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- fxcop rules
- fxcop analyzers, ported rules
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: cedd96036a6d0725dbde5f0b11400a20360a20ec
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94348940"
---
# <a name="fxcop-rule-port-status"></a>Fxcop 规则端口状态

如果以前在 Visual Studio 中使用了静态代码分析，则可能想知道哪些规则在当前实现中作为 [FxCop 分析器](install-fxcop-analyzers.md)提供。 此页列出了已移植的规则。 请参阅 [Unported 规则](fxcop-unported-rules.md) ，了解尚未移植的规则，以及是否有计划对其进行端口。

## <a name="ported-rules"></a>移植的规则

Roslyn 存储库中自动 [生成的文档页面](https://github.com/dotnet/roslyn-analyzers/blob/master/src/Microsoft.CodeAnalysis.FxCopAnalyzers/Microsoft.CodeAnalysis.FxCopAnalyzers.md) 具有已移植到 FxCop 分析器的最新规则列表。 该页还包含其他信息，例如是否默认启用规则，以及是否有关联的 *代码修复* 。  ([代码修补程序](../ide/quick-actions.md) 是 Visual Studio 的灯泡图标菜单中提供的单击一次修复。 ) 

截止到此页上的日期，已移植到 [fxcop 分析器](install-fxcop-analyzers.md) 的 fxcop 规则列表包括：

规则 ID | 标题
--------|---------
[CA1000](/dotnet/fundamentals/code-analysis/quality-rules/ca1000) | 不要在泛型类型中声明静态成员
[CA1001](/dotnet/fundamentals/code-analysis/quality-rules/ca1001) | 具有可释放字段的类型应该是可释放的
[CA1002](/dotnet/fundamentals/code-analysis/quality-rules/ca1002) | 不要公开泛型列表
[CA1003](/dotnet/fundamentals/code-analysis/quality-rules/ca1003) | 使用泛型事件处理程序实例
[CA1005](/dotnet/fundamentals/code-analysis/quality-rules/ca1005) | 避免泛型类型的参数过多
[CA1008](/dotnet/fundamentals/code-analysis/quality-rules/ca1008) | 枚举应具有零值
[CA1010](/dotnet/fundamentals/code-analysis/quality-rules/ca1010) | 集合应实现泛型接口
[CA1012](/dotnet/fundamentals/code-analysis/quality-rules/ca1012) | 抽象类型不应具有构造函数
[CA1014](/dotnet/fundamentals/code-analysis/quality-rules/ca1014) | 用 CLSCompliant 标记程序集
[CA1016](/dotnet/fundamentals/code-analysis/quality-rules/ca1016) | 用程序集版本标记程序集
[CA1017](/dotnet/fundamentals/code-analysis/quality-rules/ca1017) | 用 ComVisible 标记程序集
[CA1018](/dotnet/fundamentals/code-analysis/quality-rules/ca1018) | 用 AttributeUsageAttribute 标记特性
[CA1019](/dotnet/fundamentals/code-analysis/quality-rules/ca1019) | 定义特性参数的访问器
[CA1021](/dotnet/fundamentals/code-analysis/quality-rules/ca1021) | 避免使用 out 参数
[CA1024](/dotnet/fundamentals/code-analysis/quality-rules/ca1024) | 在适用处使用属性
[CA1027](/dotnet/fundamentals/code-analysis/quality-rules/ca1027) | 用 FlagsAttribute 标记枚举
[CA1028](/dotnet/fundamentals/code-analysis/quality-rules/ca1028) | 枚举存储应为 Int32
[CA1030](/dotnet/fundamentals/code-analysis/quality-rules/ca1030) | 在适用处使用事件
[CA1031](/dotnet/fundamentals/code-analysis/quality-rules/ca1031) | 不要捕捉一般异常类型
[CA1032](/dotnet/fundamentals/code-analysis/quality-rules/ca1032) | 实现标准异常构造函数
[CA1033](/dotnet/fundamentals/code-analysis/quality-rules/ca1033) | 接口方法应可由子类型调用
[CA1034](/dotnet/fundamentals/code-analysis/quality-rules/ca1034) | 嵌套类型不应是可见的
[CA1036](/dotnet/fundamentals/code-analysis/quality-rules/ca1036) | 重写可比较类型中的方法
[CA1040](/dotnet/fundamentals/code-analysis/quality-rules/ca1040) | 避免使用空接口
[CA1041](/dotnet/fundamentals/code-analysis/quality-rules/ca1041) | 提供 ObsoleteAttribute 消息
[CA1043](/dotnet/fundamentals/code-analysis/quality-rules/ca1043) | 将整型或字符串参数用于索引器
[CA1044](/dotnet/fundamentals/code-analysis/quality-rules/ca1044) | 属性不应是只写的
[CA1045](/dotnet/fundamentals/code-analysis/quality-rules/ca1045) | 不要通过引用来传递类型
[CA1046](/dotnet/fundamentals/code-analysis/quality-rules/ca1046) | 不要对引用类型重载相等运算符
[CA1047](/dotnet/fundamentals/code-analysis/quality-rules/ca1047) | 不要在密封类型中声明受保护的成员
[CA1050](/dotnet/fundamentals/code-analysis/quality-rules/ca1050) | 在命名空间中声明类型
[CA1051](/dotnet/fundamentals/code-analysis/quality-rules/ca1051) | 不要声明可见实例字段
[CA1052](/dotnet/fundamentals/code-analysis/quality-rules/ca1052) | 静态容器类型应为 static 或 NotInheritable
[CA1053](/dotnet/fundamentals/code-analysis/quality-rules/ca1053) | 静态容器类型不应具有构造函数 (CA1053 是 FxCop 分析器的 [CA1052](/dotnet/fundamentals/code-analysis/quality-rules/ca1052) 的一部分) 
[CA1054](/dotnet/fundamentals/code-analysis/quality-rules/ca1054) | Uri 参数不应为字符串
[CA1055](/dotnet/fundamentals/code-analysis/quality-rules/ca1055) | Uri 返回值不应是字符串
[CA1056](/dotnet/fundamentals/code-analysis/quality-rules/ca1056) | Uri 属性不应是字符串
[CA1058](/dotnet/fundamentals/code-analysis/quality-rules/ca1058) | 类型不应扩展某些基类型
[CA1060](/dotnet/fundamentals/code-analysis/quality-rules/ca1060) | 将 pinvoke 移动到本机方法类
[CA1061](/dotnet/fundamentals/code-analysis/quality-rules/ca1061) | 不要隐藏基类方法
[CA1062](/dotnet/fundamentals/code-analysis/quality-rules/ca1062) | 验证公共方法的参数
[CA1063](/dotnet/fundamentals/code-analysis/quality-rules/ca1063) | 正确实现 IDisposable
[CA1064](/dotnet/fundamentals/code-analysis/quality-rules/ca1064) | 异常应该是公共的
[CA1065](/dotnet/fundamentals/code-analysis/quality-rules/ca1065) | 不要在意外的位置引发异常
[CA1066](/dotnet/fundamentals/code-analysis/quality-rules/ca1066) | 类型 {0} 应实现 IEquatable \<T> ，因为它重写 Equals
[CA1067](/dotnet/fundamentals/code-analysis/quality-rules/ca1067) | 实现 IEquatable 时，重写对象等于)  (对象\<T>
[CA1303](/dotnet/fundamentals/code-analysis/quality-rules/ca1303) | 请不要将文本作为本地化参数传递
[CA1304](/dotnet/fundamentals/code-analysis/quality-rules/ca1304) | 指定 CultureInfo
[CA1305](/dotnet/fundamentals/code-analysis/quality-rules/ca1305) | 指定 IFormatProvider
[CA1307](/dotnet/fundamentals/code-analysis/quality-rules/ca1307) | 为清楚起见指定 StringComparison
[CA1308](/dotnet/fundamentals/code-analysis/quality-rules/ca1308) | 将字符串规范化为大写
[CA1309](/dotnet/fundamentals/code-analysis/quality-rules/ca1309) | 使用序号字符串比较
[CA1401](/dotnet/fundamentals/code-analysis/quality-rules/ca1401) | P/Invokes 应该是不可见的
[CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501) | 避免过度继承
[CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502) | 避免过度复杂
[CA1505](/dotnet/fundamentals/code-analysis/quality-rules/ca1505) | 避免使用无法维护的代码
[CA1506](/dotnet/fundamentals/code-analysis/quality-rules/ca1506) | 避免过度类耦合度
[CA1700](/dotnet/fundamentals/code-analysis/quality-rules/ca1700) | 不要命名“Reserved”枚举值
[CA1707](/dotnet/fundamentals/code-analysis/quality-rules/ca1707) | 标识符不应包含下划线
[CA1708](/dotnet/fundamentals/code-analysis/quality-rules/ca1708) | 标识符应以大小写之外的差别进行区分
[CA1710](/dotnet/fundamentals/code-analysis/quality-rules/ca1710) | 标识符应具有正确的后缀
[CA1711](/dotnet/fundamentals/code-analysis/quality-rules/ca1711) | 标识符应采用正确的后缀
[CA1712](/dotnet/fundamentals/code-analysis/quality-rules/ca1712) | 不要将类型名用作枚举值的前缀
[CA1713](/dotnet/fundamentals/code-analysis/quality-rules/ca1713) | 事件不应具有 before 或 after 前缀
[CA1714](/dotnet/fundamentals/code-analysis/quality-rules/ca1714) | Flags 枚举应采用复数形式的名称
[CA1715](/dotnet/fundamentals/code-analysis/quality-rules/ca1715) | 标识符应具有正确的前缀
[CA1716](/dotnet/fundamentals/code-analysis/quality-rules/ca1716) | 标识符不应与关键字冲突
[CA1717](/dotnet/fundamentals/code-analysis/quality-rules/ca1717) | 只有 FlagsAttribute 枚举应采用复数形式的名称
[CA1720](/dotnet/fundamentals/code-analysis/quality-rules/ca1720) | 标识符包含类型名称
[CA1721](/dotnet/fundamentals/code-analysis/quality-rules/ca1721) | 属性名不应与 get 方法冲突
[CA1724](/dotnet/fundamentals/code-analysis/quality-rules/ca1724) | 类型名不应与命名空间匹配
[CA1725](/dotnet/fundamentals/code-analysis/quality-rules/ca1725) | 参数名应与基方法中的声明保持一致
[CA1801](/dotnet/fundamentals/code-analysis/quality-rules/ca1801) | 检查未使用的参数
[CA1802](/dotnet/fundamentals/code-analysis/quality-rules/ca1802) | 在适当的位置使用文本
[CA1805](/dotnet/fundamentals/code-analysis/quality-rules/ca1805) | 不必要地初始化
[CA1806](/dotnet/fundamentals/code-analysis/quality-rules/ca1806) | 不要忽略方法结果
[CA1810](/dotnet/fundamentals/code-analysis/quality-rules/ca1810) | 以内联方式初始化引用类型的静态字段
[CA1812](/dotnet/fundamentals/code-analysis/quality-rules/ca1812) | 避免未实例化的内部类
[CA1813](/dotnet/fundamentals/code-analysis/quality-rules/ca1813) | 避免使用非密封特性
[CA1814](/dotnet/fundamentals/code-analysis/quality-rules/ca1814) | 与多维数组相比，首选使用交错数组
[CA1815](/dotnet/fundamentals/code-analysis/quality-rules/ca1815) | 重写值类型上的 Equals 和相等运算符
[CA1816](/dotnet/fundamentals/code-analysis/quality-rules/ca1816) | Dispose 方法应调用 Gc.suppressfinalize
[CA1819](/dotnet/fundamentals/code-analysis/quality-rules/ca1819) | 属性不应返回数组
[CA1820](/dotnet/fundamentals/code-analysis/quality-rules/ca1820) | 使用字符串长度测试是否有空字符串
[CA1821](/dotnet/fundamentals/code-analysis/quality-rules/ca1821) | 移除空终结器
[CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) | 将成员标记为 static
[CA1823](/dotnet/fundamentals/code-analysis/quality-rules/ca1823) | 避免未使用的私有字段
[CA1824](/dotnet/fundamentals/code-analysis/quality-rules/ca1824) | 用 NeutralResourcesLanguageAttribute 标记程序集
[CA1825](/dotnet/fundamentals/code-analysis/quality-rules/ca1825) | 避免长度为零的数组分配。
[CA2000](/dotnet/fundamentals/code-analysis/quality-rules/ca2000) | 丢失范围之前释放对象
[CA2002](/dotnet/fundamentals/code-analysis/quality-rules/ca2002) | 不要锁定具有弱标识的对象
[CA2100](/dotnet/fundamentals/code-analysis/quality-rules/ca2100) | 检查 SQL 查询是否存在安全漏洞
[CA2101](/dotnet/fundamentals/code-analysis/quality-rules/ca2101) | 指定对 P/Invoke 字符串参数进行封送处理
[CA2109](/dotnet/fundamentals/code-analysis/quality-rules/ca2109) | 检查可见的事件处理程序
[CA2119](/dotnet/fundamentals/code-analysis/quality-rules/ca2119) | 密封满足私有接口的方法
[CA2153](/dotnet/fundamentals/code-analysis/quality-rules/ca2153) | 请勿捕获损坏状态异常
[CA2200](/dotnet/fundamentals/code-analysis/quality-rules/ca2200) | 再次引发以保留堆栈详细信息。
[CA2201](/dotnet/fundamentals/code-analysis/quality-rules/ca2201) | 不要引发保留的异常类型
[CA2207](/dotnet/fundamentals/code-analysis/quality-rules/ca2207) | 以内联方式初始化值类型的静态字段
[CA2208](/dotnet/fundamentals/code-analysis/quality-rules/ca2208) | 正确实例化参数异常
[CA2211](/dotnet/fundamentals/code-analysis/quality-rules/ca2211) | 非常量字段不应是可见的
[CA2213](/dotnet/fundamentals/code-analysis/quality-rules/ca2213) | 应释放可释放的字段
[CA2214](/dotnet/fundamentals/code-analysis/quality-rules/ca2214) | 不要在构造函数中调用可重写的方法
[CA2215](/dotnet/fundamentals/code-analysis/quality-rules/ca2215) | Dispose 方法应调用基类释放
[CA2216](/dotnet/fundamentals/code-analysis/quality-rules/ca2216) | 可释放类型应声明终结器
[CA2217](/dotnet/fundamentals/code-analysis/quality-rules/ca2217) | 不要使用 FlagsAttribute 标记枚举
[CA2219](/dotnet/fundamentals/code-analysis/quality-rules/ca2219) | 不在 finally 子句中引发异常
[CA2225](/dotnet/fundamentals/code-analysis/quality-rules/ca2225) | 运算符重载具有命名的备用项
[CA2226](/dotnet/fundamentals/code-analysis/quality-rules/ca2226) | 运算符应有对称重载
[CA2227](/dotnet/fundamentals/code-analysis/quality-rules/ca2227) | 集合属性应为只读
[CA2229](/dotnet/fundamentals/code-analysis/quality-rules/ca2229) | 实现序列化构造函数
[CA2231](/dotnet/fundamentals/code-analysis/quality-rules/ca2231) | 重写值类型等于时重载相等运算符
[CA2234](/dotnet/fundamentals/code-analysis/quality-rules/ca2234) | 传递系统 uri 对象而不是字符串
[CA2235](/dotnet/fundamentals/code-analysis/quality-rules/ca2235) | 标记所有不可序列化的字段
[CA2237](/dotnet/fundamentals/code-analysis/quality-rules/ca2237) | 用 serializable 标记 ISerializable 类型
[CA2241](/dotnet/fundamentals/code-analysis/quality-rules/ca2241) | 为格式化方法提供正确的参数
[CA2242](/dotnet/fundamentals/code-analysis/quality-rules/ca2242) | 正确测试 NaN
[CA2243](/dotnet/fundamentals/code-analysis/quality-rules/ca2243) | 特性字符串文本应正确分析
[CA2300](/dotnet/fundamentals/code-analysis/quality-rules/ca2300) | 请勿使用不安全的反序列化程序 BinaryFormatte
[CA2301](/dotnet/fundamentals/code-analysis/quality-rules/ca2301) | 在未先设置 BinaryFormatter.Binder 的情况下，请不要调用 BinaryFormatter.Deserialize
[CA2302](/dotnet/fundamentals/code-analysis/quality-rules/ca2302) | 在调用 BinaryFormatter.Deserialize 之前，确保设置 BinaryFormatter.Binder
[CA2305](/dotnet/fundamentals/code-analysis/quality-rules/ca2305) | 请勿使用不安全的反序列化程序 LosFormatter
[CA2310](/dotnet/fundamentals/code-analysis/quality-rules/ca2310) | 请勿使用不安全的反序列化程序 NetDataContractSerializer
[CA2311](/dotnet/fundamentals/code-analysis/quality-rules/ca2311) | 在未先设置 NetDataContractSerializer.Binder 的情况下，请不要反序列化
[CA2312](/dotnet/fundamentals/code-analysis/quality-rules/ca2312) | 确保在反序列化之前设置 NetDataContractSerializer.Binder
[CA2315](/dotnet/fundamentals/code-analysis/quality-rules/ca2315) | 请勿使用不安全的反序列化程序 ObjectStateFormatter
[CA2321](/dotnet/fundamentals/code-analysis/quality-rules/ca2321) | 请勿使用 SimpleTypeResolver 对 JavaScriptSerializer 进行反序列化
[CA2322](/dotnet/fundamentals/code-analysis/quality-rules/ca2322) | 确保在反序列化之前没有使用 SimpleTypeResolver 初始化 JavaScriptSerializer
[CA3001](/dotnet/fundamentals/code-analysis/quality-rules/ca3001) | 查看 SQL 注入漏洞的代码
[CA3002](/dotnet/fundamentals/code-analysis/quality-rules/ca3002) | 查看 XSS 漏洞的代码
[CA3003](/dotnet/fundamentals/code-analysis/quality-rules/ca3003) | 查看文件路径注入漏洞的代码
[CA3004](/dotnet/fundamentals/code-analysis/quality-rules/ca3004) | 查看信息泄露漏洞的代码
[CA3005](/dotnet/fundamentals/code-analysis/quality-rules/ca3005) | 查看 LDAP 注入漏洞的代码
[CA3006](/dotnet/fundamentals/code-analysis/quality-rules/ca3006) | 查看进程命令注入漏洞的代码
[CA3007](/dotnet/fundamentals/code-analysis/quality-rules/ca3007) | 查看公开重定向漏洞的代码
[CA3008](/dotnet/fundamentals/code-analysis/quality-rules/ca3008) | 查看 XPath 注入漏洞的代码
[CA3009](/dotnet/fundamentals/code-analysis/quality-rules/ca3009) | 查看 XML 注入漏洞的代码
[CA3010](/dotnet/fundamentals/code-analysis/quality-rules/ca3010) | 查看 XAML 注入漏洞的代码
[CA3011](/dotnet/fundamentals/code-analysis/quality-rules/ca3011) | 查看 DLL 注入漏洞的代码
[CA3012](/dotnet/fundamentals/code-analysis/quality-rules/ca3012) | 查看正则表达式注入漏洞的代码
[CA3061](/dotnet/fundamentals/code-analysis/quality-rules/ca3061) | 不按 URL 添加架构
[CA3075](/dotnet/fundamentals/code-analysis/quality-rules/ca3075) | XML 中不安全的 DTD 处理
[CA3076](/dotnet/fundamentals/code-analysis/quality-rules/ca3076) | 不安全的 XSLT 脚本处理。
[CA3077](/dotnet/fundamentals/code-analysis/quality-rules/ca3077) | API 设计、Xml 中和 XmlTextReader 中的不安全处理
[CA3147](/dotnet/fundamentals/code-analysis/quality-rules/ca3147) | 用 Validate 防伪标记标记谓词处理程序
[CA5350](/dotnet/fundamentals/code-analysis/quality-rules/ca5350) | 请勿使用弱加密算法
[CA5351](/dotnet/fundamentals/code-analysis/quality-rules/ca5351) | 不要使用损坏的加密算法
[CA5358](/dotnet/fundamentals/code-analysis/quality-rules/ca5358) | 请勿使用不安全的密码模式
CA5359 | 不禁用证书验证
CA5360 | 不要在反序列化中调用危险方法
[CA5361](/dotnet/fundamentals/code-analysis/quality-rules/ca5361) | 不要禁止 SChannel 使用强加密
CA5362 | 不要在可序列化类中引用 Self
[CA5363](/dotnet/fundamentals/code-analysis/quality-rules/ca5363) | 不禁用请求验证
[CA5364](/dotnet/fundamentals/code-analysis/quality-rules/ca5364) | 不要使用已弃用的安全协议
CA5365 | 不禁用 HTTP 头检查
CA5366 | 将 XmlReader 用于数据集读取 Xml
CA5367 | 不要将类型与指针字段序列化
CA5368 | 为从页面派生的类设置 ViewStateUserKey
[CA5369](/dotnet/fundamentals/code-analysis/quality-rules/ca5369) | 使用 XmlReader 进行反序列化
[CA5370](/dotnet/fundamentals/code-analysis/quality-rules/ca5370) | 使用 XmlReader 验证读取器
[CA5371](/dotnet/fundamentals/code-analysis/quality-rules/ca5371) | 使用 XmlReader 进行架构读取
[CA5372](/dotnet/fundamentals/code-analysis/quality-rules/ca5372) | 将 XmlReader 用于 XPathDocument
[CA5373](/dotnet/fundamentals/code-analysis/quality-rules/ca5373) | 请勿使用已过时的密钥派生功能
CA5374 | 不使用 XslTransform
CA5375 | 不要使用帐户共享访问签名
CA5376 | 使用 SharedAccessProtocol HttpsOnly
CA5377 | 使用容器级别访问策略
[CA5378](/dotnet/fundamentals/code-analysis/quality-rules/ca5378) | 不禁用 ServicePointManagerSecurityProtocols
CA5379 | 不要使用弱密钥派生函数算法
CA9999 | 分析器版本不匹配

## <a name="see-also"></a>请参阅

- [CodeAnalysis. FxCopAnalyzers 规则](https://github.com/dotnet/roslyn-analyzers/blob/master/src/Microsoft.CodeAnalysis.FxCopAnalyzers/Microsoft.CodeAnalysis.FxCopAnalyzers.md)
