---
title: “混合建议规则”规则集
ms.date: 11/04/2016
ms.topic: reference
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c29e27160b50a53995b7542680256bfd4e2d8f2
ms.sourcegitcommit: ed4372bb6f4ae64f1fd712b2b253bf91d9ff96bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89600044"
---
# <a name="mixed-recommended-rules-rule-set"></a>“混合建议规则”规则集

Microsoft 混合推荐的规则重点介绍支持公共语言运行时的 c + + 项目中最常见和最关键的问题，包括潜在的安全漏洞、应用程序崩溃和其他重要的逻辑和设计错误。 此规则集包含 " [混合最低规则](mixed-minimum-rules-rule-set.md) " 规则集中的所有规则。

在为支持公共语言运行时的 c + + 项目创建的任何自定义规则集中包含此规则集。

|规则|描述|
|----------|-----------------|
|[C6001](/cpp/code-quality/c6001)|使用未初始化的内存|
|[C6011](/cpp/code-quality/c6011)|取消引用 Null 指针|
|[C6029](/cpp/code-quality/c6029)|未选中的值的使用|
|[C6031](/cpp/code-quality/c6031)|已忽略返回值|
|[C6053](/cpp/code-quality/c6053)|来自调用的零终止|
|[C6054](/cpp/code-quality/c6054)|缺少终止|
|[C6059](/cpp/code-quality/c6059)|不正确的串联|
|[C6063](/cpp/code-quality/c6063)|缺少 Format 函数的字符串自变量|
|[C6064](/cpp/code-quality/c6064)|缺少 Format 函数的整型自变量|
|[C6066](/cpp/code-quality/c6066)|缺少 Format 函数的指针自变量|
|[C6067](/cpp/code-quality/c6067)|缺少 Format 函数的字符串指针自变量|
|[C6101](/cpp/code-quality/c6101)|返回未初始化的内存|
|[C6200](/cpp/code-quality/c6200)|索引超出最大缓冲区大小|
|[C6201](/cpp/code-quality/c6201)|索引超出最大堆栈缓冲区大小|
|[C6214](/cpp/code-quality/c6214)|将 HRESULT 转换为 BOOL 无效|
|[C6215](/cpp/code-quality/c6215)|无效的转换布尔值到 HRESULT|
|[C6216](/cpp/code-quality/c6216)|编译器插入的强制转换布尔值无效|
|[C6217](/cpp/code-quality/c6217)|不包含的 HRESULT 测试无效|
|[C6220](/cpp/code-quality/c6220)|HRESULT 与-1 的比较无效|
|[C6226](/cpp/code-quality/c6226)|HRESULT 赋值无效-1|
|[C6230](/cpp/code-quality/c6230)|HRESULT 用作 Boolean 无效|
|[C6235](/cpp/code-quality/c6235)|带有逻辑或的非零常量|
|[C6236](/cpp/code-quality/c6236)|逻辑或与非零常量|
|[C6237](/cpp/code-quality/c6237)|带有逻辑与失去副作用的零|
|[C6242](/cpp/code-quality/c6242)|强制本地展开|
|[C6248](/cpp/code-quality/c6248)|创建 Null DACL|
|[C6250](/cpp/code-quality/c6250)|未发布地址描述符|
|[C6255](/cpp/code-quality/c6255)|不受保护的 Alloca 使用|
|[C6258](/cpp/code-quality/c6258)|使用终止线程|
|[C6259](/cpp/code-quality/c6259)|按位或限制开关中的死代码|
|[C6260](/cpp/code-quality/c6260)|使用字节算术|
|[C6262](/cpp/code-quality/c6262)|堆栈使用过多|
|[C6263](/cpp/code-quality/c6263)|在循环中使用 Alloca|
|[C6268](/cpp/code-quality/c6268)|强制转换中缺少括号|
|[C6269](/cpp/code-quality/c6269)|忽略指针取消引用|
|[C6270](/cpp/code-quality/c6270)|缺少 Format 函数的浮点型自变量|
|[C6271](/cpp/code-quality/c6271)|Format 函数的额外自变量|
|[C6272](/cpp/code-quality/c6272)|Format 函数的非浮点型自变量|
|[C6273](/cpp/code-quality/c6273)|格式函数的非整型参数|
|[C6274](/cpp/code-quality/c6274)|Format 函数的非字符自变量|
|[C6276](/cpp/code-quality/c6276)|无效字符串的强制转换|
|[C6277](/cpp/code-quality/c6277)|无效 CreateProcess 的调用|
|[C6278](/cpp/code-quality/c6278)|数组-新的标量删除不匹配|
|[C6279](/cpp/code-quality/c6279)|标量-新数组删除不匹配|
|[C6280](/cpp/code-quality/c6280)|内存分配-解除分配不匹配|
|[C6281](/cpp/code-quality/c6281)|按位关系优先顺序|
|[C6282](/cpp/code-quality/c6282)|赋值替换测试|
|[C6283](/cpp/code-quality/c6283)|基元数组-新的标量删除不匹配|
|[C6284](/cpp/code-quality/c6284)|Format 函数的无效对象自变量|
|[C6285](/cpp/code-quality/c6285)|常量的逻辑或|
|[C6286](/cpp/code-quality/c6286)|非零逻辑或丢失副作用|
|[C6287](/cpp/code-quality/c6287)|冗余测试|
|[C6288](/cpp/code-quality/c6288)|通过逻辑与的相互包含并为 False|
|[C6289](/cpp/code-quality/c6289)|基于逻辑或的互斥运算为 True|
|[C6290](/cpp/code-quality/c6290)|逻辑非和按位与的优先级|
|[C6291](/cpp/code-quality/c6291)|逻辑非和按位或的优先级|
|[C6292](/cpp/code-quality/c6292)|循环从最大值计数|
|[C6293](/cpp/code-quality/c6293)|循环从最小值向下计数|
|[C6294](/cpp/code-quality/c6294)|从未执行循环体|
|[C6295](/cpp/code-quality/c6295)|无限循环|
|[C6296](/cpp/code-quality/c6296)|循环只执行一次|
|[C6297](/cpp/code-quality/c6297)|移位强制转换为较大大小的结果|
|[C6299](/cpp/code-quality/c6299)|位域到布尔值比较|
|[C6302](/cpp/code-quality/c6302)|Format 函数的无效字符串自变量|
|[C6303](/cpp/code-quality/c6303)|Format 函数的无效宽字符串自变量|
|[C6305](/cpp/code-quality/c6305)|不匹配的大小和计数的使用|
|[C6306](/cpp/code-quality/c6306)|不正确的变量自变量函数的调用|
|[C6308](/cpp/code-quality/c6308)|Realloc 泄漏|
|[C6310](/cpp/code-quality/c6310)|非法的异常筛选器常量|
|[C6312](/cpp/code-quality/c6312)|异常继续执行循环|
|[C6314](/cpp/code-quality/c6314)|按位或优先顺序|
|[C6317](/cpp/code-quality/c6317)|不非补充|
|[C6318](/cpp/code-quality/c6318)|异常继续搜索|
|[C6319](/cpp/code-quality/c6319)|被逗号忽略|
|[C6324](/cpp/code-quality/c6324)|字符串复制而非字符串比较|
|[C6328](/cpp/code-quality/c6328)|可能的自变量类型不匹配|
|[C6331](/cpp/code-quality/c6331)|VirtualFree 无效标志|
|[C6332](/cpp/code-quality/c6332)|VirtualFree 参数无效|
|[C6333](/cpp/code-quality/c6333)|VirtualFree 大小无效|
|[C6335](/cpp/code-quality/c6335)|泄漏进程句柄|
|[C6381](/cpp/code-quality/c6381)|缺少关闭信息|
|[C6383](/cpp/code-quality/c6383)|元素计数字节计数缓冲区溢出|
|[C6384](/cpp/code-quality/c6384)|指针大小划分|
|[C6385](/cpp/code-quality/c6385)|读取溢出|
|[C6386](/cpp/code-quality/c6386)|写入溢出|
|[C6387](/cpp/code-quality/c6387)|无效的参数值|
|[C6388](/cpp/code-quality/c6388)|无效的参数值|
|[C6500](/cpp/code-quality/c6500)|无效的特性属性|
|[C6501](/cpp/code-quality/c6501)|冲突的特性属性值|
|[C6503](/cpp/code-quality/c6503)|引用不能为 Null|
|[C6504](/cpp/code-quality/c6504)|在非指针参数中为 Null|
|[C6505](/cpp/code-quality/c6505)|对 Void 类型使用 MustCheck 属性|
|[C6506](/cpp/code-quality/c6506)|非指针参数或数组的缓冲区大小|
|[C6508](/cpp/code-quality/c6508)|常量缓冲区上的写入权限|
|[C6509](/cpp/code-quality/c6509)|返回使用的前置条件|
|[C6510](/cpp/code-quality/c6510)|在非指针参数中以 Null 结尾的参数|
|[C6511](/cpp/code-quality/c6511)|MustCheck 属性必须为 Yes 或 No|
|[C6513](/cpp/code-quality/c6513)|没有缓冲区大小的元素大小|
|[C6514](/cpp/code-quality/c6514)|缓冲区大小超过数组大小|
|[C6515](/cpp/code-quality/c6515)|非指针参数的缓冲区大小|
|[C6516](/cpp/code-quality/c6516)|在特性上无属性|
|[C6517](/cpp/code-quality/c6517)|有效的不可读缓冲区的大小|
|[C6518](/cpp/code-quality/c6518)|不可写的缓冲区的可写入大小|
|[C6522](/cpp/code-quality/c6522)|无效大小的字符串类型|
|[C6525](/cpp/code-quality/c6525)|无效大小字符串的不可访问的位置|
|[C6527](/cpp/code-quality/c6527)|无效的批注：“NeedsRelease”属性可能不可用于 void 类型的值|
|[C6530](/cpp/code-quality/c6530)|无法识别的格式字符串样式|
|[C6540](/cpp/code-quality/c6540)|对该函数使用属性批注将使其现有的所有 __declspec 批注无效|
|[C6551](/cpp/code-quality/c6551)|大小规范无效：表达式不可分析|
|[C6552](/cpp/code-quality/c6552)|Deref= 或 Notref= 无效：表达式不可分析|
|[C6701](/cpp/code-quality/c6701)|该值不是有效的 Yes/No/Maybe 值|
|[C6702](/cpp/code-quality/c6702)|该值不是字符串值|
|[C6703](/cpp/code-quality/c6703)|该值不是一个数字|
|[C6704](/cpp/code-quality/c6704)|意外的批注表达式错误|
|[C6705](/cpp/code-quality/c6705)|批注自变量的预期数量与批注自变量的实际数量不匹配|
|[C6706](/cpp/code-quality/c6706)|批注的意外批注错误|
|[C6995](/cpp/code-quality/c6995)|未能保存 XML 日志文件|
|[C26100](/cpp/code-quality/c26100)|争用条件|
|[C26101](/cpp/code-quality/c26101)|未能正确使用联锁操作|
|[C26110](/cpp/code-quality/c26110)|调用方未能持有锁|
|[C26111](/cpp/code-quality/c26111)|调用方未能解除锁|
|[C26112](/cpp/code-quality/c26112)|调用方无法持有任何锁|
|[C26115](/cpp/code-quality/c26115)|未能解除锁定|
|[C26116](/cpp/code-quality/c26116)|未能获取或持有锁|
|[C26117](/cpp/code-quality/c26117)|释放解除持有锁|
|[C26140](/cpp/code-quality/c26140)|并发 SAL 批注错误|
|[C28020](/cpp/code-quality/c28020)|此调用中的表达式不为 true|
|[C28021](/cpp/code-quality/c28021)|批注的参数必须为指针型|
|[C28022](/cpp/code-quality/c28022)|此函数的函数类 (es) 与用于定义它的 typedef 上的函数类 (es) 不匹配。|
|[C28023](/cpp/code-quality/c28023)|分配或传递的函数应该 \_ \_ 至少有一个类的函数类 \_ 注释 (es) |
|[C28024](/cpp/code-quality/c28024)|向其分配的函数指针是用函数类进行批注的，函数类不包含在函数类中 (es) 列表。|
|[C28039](/cpp/code-quality/c28039)|实参的类型应与类型完全匹配|
|[C28112](/cpp/code-quality/c28112)|通过互锁函数访问的变量必须始终通过联锁函数访问。|
|[C28113](/cpp/code-quality/c28113)|通过互锁函数访问本地变量|
|[C28125](/cpp/code-quality/c28125)|必须从 try/except 块中调用函数|
|[C28137](/cpp/code-quality/c28137)|变量参数应是 (文本) 常量|
|[C28138](/cpp/code-quality/c28138)|常数参数应改为变量|
|[C28159](/cpp/code-quality/c28159)|请考虑改用其他函数。|
|[C28160](/cpp/code-quality/c28160)|错误批注|
|[C28163](/cpp/code-quality/c28163)|绝不应从 try/except 块中调用函数|
|[C28164](/cpp/code-quality/c28164)|参数被传递到一个函数，该函数需要指向对象的指针 (不是指向指针的指针) |
|[C28182](/cpp/code-quality/c28182)|取消引用 NULL 指针。 该指针包含与另一指针相同的 NULL 值。|
|[C28183](/cpp/code-quality/c28183)|参数可以是一个值，并且是在指针中找到的值的副本|
|[C28193](/cpp/code-quality/c28193)|变量保存一个必须检查的值|
|[C28196](/cpp/code-quality/c28196)|不满足要求。  (表达式的计算结果不为 true。 ) |
|[C28202](/cpp/code-quality/c28202)|非法引用非静态成员|
|[C28203](/cpp/code-quality/c28203)|对类成员的不明确的引用。|
|[C28205](/cpp/code-quality/c28205)|\_\_ \_ \_ \_ 在非法上下文中使用成功或失败|
|[C28206](/cpp/code-quality/c28206)|若左操作数指向结构，则使用“->”|
|[C28207](/cpp/code-quality/c28207)|若左操作数是一个结构，则使用“.”|
|[C28209](/cpp/code-quality/c28209)|符号的声明具有冲突的声明|
|[C28210](/cpp/code-quality/c28210)|__on_failure 上下文的批注不得位于显式的 pre 上下文中|
|[C28211](/cpp/code-quality/c28211)|SAL_context 所需的静态上下文名称|
|[C28212](/cpp/code-quality/c28212)|批注所需的指针表达式|
|[C28213](/cpp/code-quality/c28213)|\_Use \_ decl \_ 批注 \_ 批注必须用于引用之前的声明，而无需修改。|
|[C28214](/cpp/code-quality/c28214)|特性参数的名称必须为 p1...p9|
|[C28215](/cpp/code-quality/c28215)|不能将 typefix 应用于已包含 typefix 的参数|
|[C28216](/cpp/code-quality/c28216)|checkReturn 批注仅应用于特定函数参数的后置条件。|
|[C28217](/cpp/code-quality/c28217)|对于函数，批注的参数数目与在文件中找到的数目不匹配|
|[C28218](/cpp/code-quality/c28218)|对于函数参数，批注的参数与在文件中找到的参数不匹配|
|[C28219](/cpp/code-quality/c28219)|批注中的批注参数所需的枚举成员|
|[C28220](/cpp/code-quality/c28220)|批注中的批注参数所需的整数表达式|
|[C28221](/cpp/code-quality/c28221)|批注中的参数所需的字符串表达式|
|[C28222](/cpp/code-quality/c28222)|批注所需的 __yes、\__no 或 \__maybe|
|[C28223](/cpp/code-quality/c28223)|未找到批注和参数所需的标记/标识符|
|[C28224](/cpp/code-quality/c28224)|批注需要参数|
|[C28225](/cpp/code-quality/c28225)|未在批注中找到所需参数的正确数目|
|[C28226](/cpp/code-quality/c28226)|批注也不能为 PrimOp（在当前声明中）|
|[C28227](/cpp/code-quality/c28227)|批注也不能为 PrimOp（请参阅上一个声明）|
|[C28228](/cpp/code-quality/c28228)|批注参数：在批注中不能使用类型|
|[C28229](/cpp/code-quality/c28229)|批注不支持参数|
|[C28230](/cpp/code-quality/c28230)|参数类型没有成员。|
|[C28231](/cpp/code-quality/c28231)|批注仅在数组上有效|
|[C28232](/cpp/code-quality/c28232)|pre、post 或 deref 不适用于任何批注|
|[C28233](/cpp/code-quality/c28233)|pre、post 或 dere 适用于块|
|[C28234](/cpp/code-quality/c28234)|__at 表达式不适用于当前函数|
|[C28235](/cpp/code-quality/c28235)|函数无法作为批注单独存在|
|[C28236](/cpp/code-quality/c28236)|批注无法在表达式中使用|
|[C28237](/cpp/code-quality/c28237)|不再支持参数上的批注|
|[C28238](/cpp/code-quality/c28238)|参数上的批注具有多个值：stringValue 和 longValue。 使用 paramn=xxx|
|[C28239](/cpp/code-quality/c28239)|参数上的批注包含两个值 stringValue 或 longValue；paramn=xxx。 仅使用 paramn=xxx|
|[C28240](/cpp/code-quality/c28240)|参数上的批注包含 param2，但不包含 param1|
|[C28241](/cpp/code-quality/c28241)|未识别参数上的函数的批注|
|[C28243](/cpp/code-quality/c28243)|参数上函数的批注需要的取消引用次数多于已批注的实际类型所允许的次数|
|[C28244](/cpp/code-quality/c28244)|函数的批注包含无法分析的参数/外部批注|
|[C28245](/cpp/code-quality/c28245)|函数的批注将在非成员函数上批注“this”|
|[C28246](/cpp/code-quality/c28246)|函数的参数批注与参数的类型不匹配|
|[C28250](/cpp/code-quality/c28250)|函数的批注不一致：上一实例发生错误。|
|[C28251](/cpp/code-quality/c28251)|函数的批注不一致：该实例发生错误。|
|[C28252](/cpp/code-quality/c28252)|函数的批注不一致：参数在此实例中包含另一个批注。|
|[C28253](/cpp/code-quality/c28253)|函数的批注不一致：参数在此实例中包含另一个批注。|
|[C28254](/cpp/code-quality/c28254)|批注中不支持 dynamic_cast<>()|
|[C28262](/cpp/code-quality/c28262)|对于批注，在函数中找到了批注的语法错误|
|[C28263](/cpp/code-quality/c28263)|在条件批注中找到内部批注的语法错误|
|[C28267](/cpp/code-quality/c28267)|在函数中找到了批注的语法错误。|
|[C28272](/cpp/code-quality/c28272)|在检查参数时，函数的批注与函数声明不一致|
|[C28273](/cpp/code-quality/c28273)|对于函数，线索与函数声明不一致|
|[C28275](/cpp/code-quality/c28275)|\_宏值的参数 \_ \_ 为 null|
|[C28279](/cpp/code-quality/c28279)|对于符号，已找到“起始”符号，但没有匹配的“结束”符号|
|[C28280](/cpp/code-quality/c28280)|对于符号，已找到“结束”符号，但没有匹配的“起始”符号|
|[C28282](/cpp/code-quality/c28282)|格式字符串必须位于前置条件中|
|[C28285](/cpp/code-quality/c28285)|对于函数，参数中存在语法错误|
|[C28286](/cpp/code-quality/c28286)|对于函数，在其结尾附近出现语法错误|
|[C28287](/cpp/code-quality/c28287)|对于函数，在 \_At\_() 批注中出现语法错误（无法识别的参数名）|
|[C28288](/cpp/code-quality/c28288)|对于函数，在 \_At\_() 批注中出现语法错误（无效的参数名）|
|[C28289](/cpp/code-quality/c28289)|对于函数：ReadableTo 或 WritableTo 没有用作参数的限制规范|
|[C28290](/cpp/code-quality/c28290)|函数的批注包含的外部对象数量多于实际的参数数量|
|[C28291](/cpp/code-quality/c28291)|deref 级别 0 处的 post null/notnull 对于函数无意义。|
|[C28300](/cpp/code-quality/c28300)|运算符的不可兼容类型的表达式操作数|
|[C28301](/cpp/code-quality/c28301)|函数的第一个声明中不包含任何批注。|
|[C28302](/cpp/code-quality/c28302)|在批注中找到多余的 \_Deref\_ 运算符。|
|[C28303](/cpp/code-quality/c28303)|在批注中找到含义模糊的 \_Deref\_ 运算符。|
|[C28304](/cpp/code-quality/c28304)|发现未正确放置的 \_Notref\_ 运算符被应用到令牌。|
|[C28305](/cpp/code-quality/c28305)|在分析标记时发现错误。|
|[C28306](/cpp/code-quality/c28306)|参数上的批注为 sal|
|[C28307](/cpp/code-quality/c28307)|参数上的批注为 sal|
|[C28350](/cpp/code-quality/c28350)|批注介绍了无条件适用的情形。|
|[C28351](/cpp/code-quality/c28351)|批注介绍了在条件中无法使用动态值（变量）的位置。|
|[CA1001](../code-quality/ca1001.md)|具有可释放字段的类型应该是可释放的|
|[CA1009](../code-quality/ca1009.md)|正确声明事件处理程序|
|[CA1016](../code-quality/ca1016.md)|用 AssemblyVersionAttribute 标记程序集|
|[CA1033](../code-quality/ca1033.md)|接口方法应可由子类型调用|
|[CA1049](../code-quality/ca1049.md)|拥有本机资源的类型应是可释放的|
|[CA1060](../code-quality/ca1060.md)|将 P/Invoke 移动到 NativeMethods 类|
|[CA1061](../code-quality/ca1061.md)|不要隐藏基类方法|
|[CA1063](../code-quality/ca1063.md)|正确实现 IDisposable|
|[CA1065](../code-quality/ca1065.md)|不要在意外的位置引发异常|
|[CA1301](../code-quality/ca1301.md)|避免快捷键重复|
|[CA1400](../code-quality/ca1400.md)|P/Invoke 入口点应该存在|
|[CA1401](../code-quality/ca1401.md)|P/Invokes 应该是不可见的|
|[CA1403](../code-quality/ca1403.md)|自动布局类型不应对 COM 可见|
|[CA1404](../code-quality/ca1404.md)|紧接在 P/Invoke 之后调用 GetLastError|
|[CA1405](../code-quality/ca1405.md)|COM 可见类型的基类型应对 COM 可见|
|[CA1410](../code-quality/ca1410.md)|应对 COM 注册方法进行匹配|
|[CA1415](../code-quality/ca1415.md)|正确声明 P/Invoke|
|[CA1821](../code-quality/ca1821.md)|移除空终结器|
|[CA1900](../code-quality/ca1900.md)|值类型字段应为可移植字段|
|[CA1901](../code-quality/ca1901.md)|P/Invoke 声明应为可移植声明|
|[CA2002](../code-quality/ca2002.md)|不要锁定具有弱标识的对象|
|[CA2100](../code-quality/ca2100.md)|检查 SQL 查询是否存在安全漏洞|
|[CA2101](../code-quality/ca2101.md)|指定对 P/Invoke 字符串参数进行封送处理|
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