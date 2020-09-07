---
title: FxCop 规则端口状态
ms.date: 05/21/2019
ms.topic: reference
helpviewer_keywords:
- fxcop rules
- fxcop analyzers, ported rules
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 28429b43295956d29bb9fc04f80ccf7ba1b1e720
ms.sourcegitcommit: 5caad925ca0b5d136416144a279e984836d8f28c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2020
ms.locfileid: "89508361"
---
# <a name="fxcop-rule-port-status"></a>Fxcop 规则端口状态

如果以前在 Visual Studio 中使用了静态代码分析，则可能想知道哪些规则在当前实现中作为 [FxCop 分析器](install-fxcop-analyzers.md)提供。 此页列出了已移植的规则。 请参阅 [Unported 规则](fxcop-unported-rules.md) ，了解尚未移植的规则，以及是否有计划对其进行端口。

## <a name="ported-rules"></a>移植的规则

Roslyn 存储库中自动 [生成的文档页面](https://github.com/dotnet/roslyn-analyzers/blob/master/src/Microsoft.CodeAnalysis.FxCopAnalyzers/Microsoft.CodeAnalysis.FxCopAnalyzers.md) 具有已移植到 FxCop 分析器的最新规则列表。 该页还包含其他信息，例如是否默认启用规则，以及是否有关联的 *代码修复*。  ([代码修补程序](../ide/quick-actions.md) 是 Visual Studio 的灯泡图标菜单中提供的单击一次修复。 ) 

截止到此页上的日期，已移植到 [fxcop 分析器](install-fxcop-analyzers.md) 的 fxcop 规则列表包括：

规则 ID | 标题
--------|---------
[CA1000](ca1000.md) | 不要在泛型类型中声明静态成员
[CA1001](ca1001.md) | 具有可释放字段的类型应该是可释放的
[CA1002](ca1002.md) | 不要公开泛型列表
[CA1003](ca1003.md) | 使用泛型事件处理程序实例
[CA1005](ca1005.md) | 避免泛型类型的参数过多
[CA1008](ca1008.md) | 枚举应具有零值
[CA1010](ca1010.md) | 集合应实现泛型接口
[CA1012](ca1012.md) | 抽象类型不应具有构造函数
[CA1014](ca1014.md) | 用 CLSCompliant 标记程序集
[CA1016](ca1016.md) | 用程序集版本标记程序集
[CA1017](ca1017.md) | 用 ComVisible 标记程序集
[CA1018](ca1018.md) | 用 AttributeUsageAttribute 标记特性
[CA1019](ca1019.md) | 定义特性参数的访问器
[CA1021](ca1021.md) | 避免使用 out 参数
[CA1024](ca1024.md) | 在适用处使用属性
[CA1027](ca1027.md) | 用 FlagsAttribute 标记枚举
[CA1028](ca1028.md) | 枚举存储应为 Int32
[CA1030](ca1030.md) | 在适用处使用事件
[CA1031](ca1031.md) | 不要捕捉一般异常类型
[CA1032](ca1032.md) | 实现标准异常构造函数
[CA1033](ca1033.md) | 接口方法应可由子类型调用
[CA1034](ca1034.md) | 嵌套类型不应是可见的
[CA1036](ca1036.md) | 重写可比较类型中的方法
[CA1040](ca1040.md) | 避免使用空接口
[CA1041](ca1041.md) | 提供 ObsoleteAttribute 消息
[CA1043](ca1043.md) | 将整型或字符串参数用于索引器
[CA1044](ca1044.md) | 属性不应是只写的
[CA1045](ca1045.md) | 不要通过引用来传递类型
[CA1046](ca1046.md) | 不要对引用类型重载相等运算符
[CA1047](ca1047.md) | 不要在密封类型中声明受保护的成员
[CA1050](ca1050.md) | 在命名空间中声明类型
[CA1051](ca1051.md) | 不要声明可见实例字段
[CA1052](ca1052.md) | 静态容器类型应为 static 或 NotInheritable
[CA1053](ca1053.md) | 静态容器类型不应具有构造函数 (CA1053 是 FxCop 分析器的 [CA1052](ca1052.md) 的一部分) 
[CA1054](ca1054.md) | Uri 参数不应为字符串
[CA1055](ca1055.md) | Uri 返回值不应是字符串
[CA1056](ca1056.md) | Uri 属性不应是字符串
[CA1058](ca1058.md) | 类型不应扩展某些基类型
[CA1060](ca1060.md) | 将 pinvoke 移动到本机方法类
[CA1061](ca1061.md) | 不要隐藏基类方法
[CA1062](ca1062.md) | 验证公共方法的参数
[CA1063](ca1063.md) | 正确实现 IDisposable
[CA1064](ca1064.md) | 异常应该是公共的
[CA1065](ca1065.md) | 不要在意外的位置引发异常
[CA1066](ca1066.md) | 类型 {0} 应实现 IEquatable \<T> ，因为它重写 Equals
[CA1067](ca1067.md) | 实现 IEquatable 时，重写对象等于)  (对象\<T>
[CA1303](ca1303.md) | 请不要将文本作为本地化参数传递
[CA1304](ca1304.md) | 指定 CultureInfo
[CA1305](ca1305.md) | 指定 IFormatProvider
[CA1307](ca1307.md) | 为清楚起见指定 StringComparison
[CA1308](ca1308.md) | 将字符串规范化为大写
[CA1309](ca1309.md) | 使用序号字符串比较
[CA1401](ca1401.md) | P/Invokes 应该是不可见的
[CA1501](ca1501.md) | 避免过度继承
[CA1502](ca1502.md) | 避免过度复杂
[CA1505](ca1505.md) | 避免使用无法维护的代码
[CA1506](ca1506.md) | 避免过度类耦合度
[CA1700](ca1700.md) | 不要命名“Reserved”枚举值
[CA1707](ca1707.md) | 标识符不应包含下划线
[CA1708](ca1708.md) | 标识符应以大小写之外的差别进行区分
[CA1710](ca1710.md) | 标识符应具有正确的后缀
[CA1711](ca1711.md) | 标识符应采用正确的后缀
[CA1712](ca1712.md) | 不要将类型名用作枚举值的前缀
[CA1713](ca1713.md) | 事件不应具有 before 或 after 前缀
[CA1714](ca1714.md) | Flags 枚举应采用复数形式的名称
[CA1715](ca1715.md) | 标识符应具有正确的前缀
[CA1716](ca1716.md) | 标识符不应与关键字冲突
[CA1717](ca1717.md) | 只有 FlagsAttribute 枚举应采用复数形式的名称
[CA1720](ca1720.md) | 标识符包含类型名称
[CA1721](ca1721.md) | 属性名不应与 get 方法冲突
[CA1724](ca1724.md) | 类型名不应与命名空间匹配
[CA1725](ca1725.md) | 参数名应与基方法中的声明保持一致
[CA1801](ca1801.md) | 检查未使用的参数
[CA1802](ca1802.md) | 在适当的位置使用文本
[CA1805](ca1805.md) | 不必要地初始化
[CA1806](ca1806.md) | 不要忽略方法结果
[CA1810](ca1810.md) | 以内联方式初始化引用类型的静态字段
[CA1812](ca1812.md) | 避免未实例化的内部类
[CA1813](ca1813.md) | 避免使用非密封特性
[CA1814](ca1814.md) | 与多维数组相比，首选使用交错数组
[CA1815](ca1815.md) | 重写值类型上的 Equals 和相等运算符
[CA1816](ca1816.md) | Dispose 方法应调用 Gc.suppressfinalize
[CA1819](ca1819.md) | 属性不应返回数组
[CA1820](ca1820.md) | 使用字符串长度测试是否有空字符串
[CA1821](ca1821.md) | 移除空终结器
[CA1822](ca1822.md) | 将成员标记为 static
[CA1823](ca1823.md) | 避免未使用的私有字段
[CA1824](ca1824.md) | 用 NeutralResourcesLanguageAttribute 标记程序集
[CA1825](ca1825.md) | 避免长度为零的数组分配。
[CA2000](ca2000.md) | 丢失范围之前释放对象
[CA2002](ca2002.md) | 不要锁定具有弱标识的对象
[CA2100](ca2100.md) | 检查 SQL 查询是否存在安全漏洞
[CA2101](ca2101.md) | 指定对 P/Invoke 字符串参数进行封送处理
[CA2109](ca2109.md) | 检查可见的事件处理程序
[CA2119](ca2119.md) | 密封满足私有接口的方法
[CA2153](ca2153.md) | 请勿捕获损坏状态异常
[CA2200](ca2200.md) | 再次引发以保留堆栈详细信息。
[CA2201](ca2201.md) | 不要引发保留的异常类型
[CA2207](ca2207.md) | 以内联方式初始化值类型的静态字段
[CA2208](ca2208.md) | 正确实例化参数异常
[CA2211](ca2211.md) | 非常量字段不应是可见的
[CA2213](ca2213.md) | 应释放可释放的字段
[CA2214](ca2214.md) | 不要在构造函数中调用可重写的方法
[CA2215](ca2215.md) | Dispose 方法应调用基类释放
[CA2216](ca2216.md) | 可释放类型应声明终结器
[CA2217](ca2217.md) | 不要使用 FlagsAttribute 标记枚举
[CA2219](ca2219.md) | 不在 finally 子句中引发异常
[CA2225](ca2225.md) | 运算符重载具有命名的备用项
[CA2226](ca2226.md) | 运算符应有对称重载
[CA2227](ca2227.md) | 集合属性应为只读
[CA2229](ca2229.md) | 实现序列化构造函数
[CA2231](ca2231.md) | 重写值类型等于时重载相等运算符
[CA2234](ca2234.md) | 传递系统 uri 对象而不是字符串
[CA2235](ca2235.md) | 标记所有不可序列化的字段
[CA2237](ca2237.md) | 用 serializable 标记 ISerializable 类型
[CA2241](ca2241.md) | 为格式化方法提供正确的参数
[CA2242](ca2242.md) | 正确测试 NaN
[CA2243](ca2243.md) | 特性字符串文本应正确分析
[CA2300](ca2300.md) | 请勿使用不安全的反序列化程序 BinaryFormatte
[CA2301](ca2301.md) | 在未先设置 BinaryFormatter.Binder 的情况下，请不要调用 BinaryFormatter.Deserialize
[CA2302](ca2302.md) | 在调用 BinaryFormatter.Deserialize 之前，确保设置 BinaryFormatter.Binder
[CA2305](ca2305.md) | 请勿使用不安全的反序列化程序 LosFormatter
[CA2310](ca2310.md) | 请勿使用不安全的反序列化程序 NetDataContractSerializer
[CA2311](ca2311.md) | 在未先设置 NetDataContractSerializer.Binder 的情况下，请不要反序列化
[CA2312](ca2312.md) | 确保在反序列化之前设置 NetDataContractSerializer.Binder
[CA2315](ca2315.md) | 请勿使用不安全的反序列化程序 ObjectStateFormatter
[CA2321](ca2321.md) | 请勿使用 SimpleTypeResolver 对 JavaScriptSerializer 进行反序列化
[CA2322](ca2322.md) | 确保在反序列化之前没有使用 SimpleTypeResolver 初始化 JavaScriptSerializer
[CA3001](ca3001.md) | 查看 SQL 注入漏洞的代码
[CA3002](ca3002.md) | 查看 XSS 漏洞的代码
[CA3003](ca3003.md) | 查看文件路径注入漏洞的代码
[CA3004](ca3004.md) | 查看信息泄露漏洞的代码
[CA3005](ca3005.md) | 查看 LDAP 注入漏洞的代码
[CA3006](ca3006.md) | 查看进程命令注入漏洞的代码
[CA3007](ca3007.md) | 查看公开重定向漏洞的代码
[CA3008](ca3008.md) | 查看 XPath 注入漏洞的代码
[CA3009](ca3009.md) | 查看 XML 注入漏洞的代码
[CA3010](ca3010.md) | 查看 XAML 注入漏洞的代码
[CA3011](ca3011.md) | 查看 DLL 注入漏洞的代码
[CA3012](ca3012.md) | 查看正则表达式注入漏洞的代码
[CA3061](ca3061.md) | 不按 URL 添加架构
[CA3075](ca3075.md) | XML 中不安全的 DTD 处理
[CA3076](ca3076.md) | 不安全的 XSLT 脚本处理。
[CA3077](ca3077.md) | API 设计、Xml 中和 XmlTextReader 中的不安全处理
[CA3147](ca3147.md) | 用 Validate 防伪标记标记谓词处理程序
[CA5350](ca5350.md) | 请勿使用弱加密算法
[CA5351](ca5351.md) | 不要使用损坏的加密算法
[CA5358](ca5358.md) | 请勿使用不安全的密码模式
CA5359 | 不禁用证书验证
CA5360 | 不要在反序列化中调用危险方法
[CA5361](ca5361.md) | 不要禁止 SChannel 使用强加密
CA5362 | 不要在可序列化类中引用 Self
[CA5363](ca5363.md) | 不禁用请求验证
[CA5364](ca5364.md) | 不要使用已弃用的安全协议
CA5365 | 不禁用 HTTP 头检查
CA5366 | 将 XmlReader 用于数据集读取 Xml
CA5367 | 不要将类型与指针字段序列化
CA5368 | 为从页面派生的类设置 ViewStateUserKey
[CA5369](ca5369.md) | 使用 XmlReader 进行反序列化
[CA5370](ca5370.md) | 使用 XmlReader 验证读取器
[CA5371](ca5371.md) | 使用 XmlReader 进行架构读取
[CA5372](ca5372.md) | 将 XmlReader 用于 XPathDocument
[CA5373](ca5373.md) | 请勿使用已过时的密钥派生功能
CA5374 | 不使用 XslTransform
CA5375 | 不要使用帐户共享访问签名
CA5376 | 使用 SharedAccessProtocol HttpsOnly
CA5377 | 使用容器级别访问策略
[CA5378](ca5378.md) | 不禁用 ServicePointManagerSecurityProtocols
CA5379 | 不要使用弱密钥派生函数算法
CA9999 | 分析器版本不匹配

## <a name="see-also"></a>另请参阅

- [CodeAnalysis. FxCopAnalyzers 规则](https://github.com/dotnet/roslyn-analyzers/blob/master/src/Microsoft.CodeAnalysis.FxCopAnalyzers/Microsoft.CodeAnalysis.FxCopAnalyzers.md)
