---
title: “本机最少量规则”规则集
ms.date: 11/04/2016
description: 了解 Visual Studio 中的 "本机最低规则" 规则集。 请参阅针对安全、可靠性和本机代码中的其他关键问题的规则说明。
ms.custom: SEO-VS-2020
ms.topic: reference
ms.assetid: 2d898bc4-fba5-472e-8f09-b0c6b511c5a3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 182c896aea682287f89119217e5d4b8b860b6dcf
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94437078"
---
# <a name="native-minimum-rules-rule-set"></a>“本机最少量规则”规则集

Microsoft 本机最小规则重点关注本机代码中的最关键问题，包括潜在的安全漏洞和应用程序崩溃。

在您为本机项目创建的任何自定义规则集中包含此规则集。

|规则|描述|
|----------|-----------------|
|[C6001](/cpp/code-quality/c6001)|使用未初始化的内存|
|[C6011](/cpp/code-quality/c6011)|取消引用 Null 指针|
|[C6029](/cpp/code-quality/c6029)|未选中的值的使用|
|[C6053](/cpp/code-quality/c6053)|来自调用的零终止|
|[C6059](/cpp/code-quality/c6059)|不正确的串联|
|[C6063](/cpp/code-quality/c6063)|缺少 Format 函数的字符串自变量|
|[C6064](/cpp/code-quality/c6064)|缺少 Format 函数的整型自变量|
|[C6066](/cpp/code-quality/c6066)|缺少 Format 函数的指针自变量|
|[C6067](/cpp/code-quality/c6067)|缺少 Format 函数的字符串指针自变量|
|[C6101](/cpp/code-quality/c6101)|返回未初始化的内存|
|[C6200](/cpp/code-quality/c6200)|索引超出最大缓冲区大小|
|[C6201](/cpp/code-quality/c6201)|索引超出最大堆栈缓冲区大小|
|[C6270](/cpp/code-quality/c6270)|缺少 Format 函数的浮点型自变量|
|[C6271](/cpp/code-quality/c6271)|Format 函数的额外自变量|
|[C6272](/cpp/code-quality/c6272)|Format 函数的非浮点型自变量|
|[C6273](/cpp/code-quality/c6273)|格式函数的非整型参数|
|[C6274](/cpp/code-quality/c6274)|Format 函数的非字符自变量|
|[C6276](/cpp/code-quality/c6276)|无效字符串的强制转换|
|[C6277](/cpp/code-quality/c6277)|无效 CreateProcess 的调用|
|[C6284](/cpp/code-quality/c6284)|Format 函数的无效对象自变量|
|[C6290](/cpp/code-quality/c6290)|逻辑非和按位与的优先级|
|[C6291](/cpp/code-quality/c6291)|逻辑非和按位或的优先级|
|[C6302](/cpp/code-quality/c6302)|Format 函数的无效字符串自变量|
|[C6303](/cpp/code-quality/c6303)|Format 函数的无效宽字符串自变量|
|[C6305](/cpp/code-quality/c6305)|不匹配的大小和计数的使用|
|[C6306](/cpp/code-quality/c6306)|不正确的变量自变量函数的调用|
|[C6328](/cpp/code-quality/c6328)|可能的自变量类型不匹配|
|[C6385](/cpp/code-quality/c6385)|读取溢出|
|[C6386](/cpp/code-quality/c6386)|写入溢出|
|[C6387](/cpp/code-quality/c6387)|无效的参数值|
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
|[C26450](/cpp/code-quality/C26450)|RESULT_OF_ARITHMETIC_OPERATION_PROVABLY_LOSSY|
|[C26451](/cpp/code-quality/C26451)|RESULT_OF_ARITHMETIC_OPERATION_CAST_TO_LARGER_SIZE|
|[C26452](/cpp/code-quality/C26452)|SHIFT_COUNT_NEGATIVE_OR_TOO_BIG|
|[C26453](/cpp/code-quality/C26453)|LEFTSHIFT_NEGATIVE_SIGNED_NUMBER|
|[C26454](/cpp/code-quality/C26454)|RESULT_OF_ARITHMETIC_OPERATION_NEGATIVE_UNSIGNED|
|[C26495](/cpp/code-quality/C26495)|MEMBER_UNINIT|
|[C28021](/cpp/code-quality/c28021)|批注的参数必须为指针型|
|[C28182](/cpp/code-quality/c28182)|取消引用 NULL 指针。 该指针包含与另一指针相同的 NULL 值。|
|[C28202](/cpp/code-quality/c28202)|非法引用非静态成员|
|[C28203](/cpp/code-quality/c28203)|对类成员的不明确的引用。|
|[C28205](/cpp/code-quality/c28205)|\_\_ \_ \_ \_ 在非法上下文中使用成功或失败|
|[C28206](/cpp/code-quality/c28206)|若左操作数指向结构，则使用“->”|
|[C28207](/cpp/code-quality/c28207)|若左操作数是一个结构，则使用“.”|
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
|[C28350](/cpp/code-quality/c28350)|批注介绍了无条件适用的情形。|
|[C28351](/cpp/code-quality/c28351)|批注介绍了在条件中无法使用动态值（变量）的位置。|