---
title: 本机建议规则规则集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 8d845b5a-1b75-4e9d-861a-7c59cb7752af
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a0b2dd8f7e48ea9fe1c1a46daf99302b3c29081f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703190"
---
# <a name="native-recommended-rules-rule-set"></a>“本机建议规则”规则集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本机建议规则重点关注本机代码，包括潜在安全漏洞和应用程序崩溃中最重要、 最常见的问题。  应在你为本机项目创建的任何自定义规则集中包含此规则集。  此规则集用于处理与 Visual Studio 专业版和更高版本。  

|                                      规则                                      |                                                             描述                                                             |
|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
|                       [C6001](../code-quality/c6001.md)                        |                                                     使用未初始化的内存                                                      |
|                       [C6011](../code-quality/c6011.md)                        |                                                     取消引用 Null 指针                                                      |
|                       [C6029](../code-quality/c6029.md)                        |                                                       未选中的值的使用                                                        |
|                       [C6031](../code-quality/c6031.md)                        |                                                        返回值被忽略                                                         |
|                       [C6053](../code-quality/c6053.md)                        |                                                     来自调用的零终止                                                      |
|                       [C6054](../code-quality/c6054.md)                        |                                                      零终止缺失                                                       |
|                       [C6059](../code-quality/c6059.md)                        |                                                          不正确的串联                                                          |
|                       [C6063](../code-quality/c6063.md)                        |                                             缺少 Format 函数的字符串自变量                                              |
|                       [C6064](../code-quality/c6064.md)                        |                                             缺少 Format 函数的整型自变量                                             |
|                       [C6066](../code-quality/c6066.md)                        |                                             缺少 Format 函数的指针自变量                                             |
|                       [C6067](../code-quality/c6067.md)                        |                                         缺少 Format 函数的字符串指针自变量                                          |
|                       [C6101](../code-quality/c6101.md)                        |                                                   返回未初始化的内存                                                    |
|                       [C6200](../code-quality/c6200.md)                        |                                                    索引超出最大缓冲区大小                                                     |
|                       [C6201](../code-quality/c6201.md)                        |                                                 索引超出最大堆栈缓冲区大小                                                  |
|                       [C6214](../code-quality/c6214.md)                        |                                                    强制转换为 HRESULT 到 BOOL 的无效                                                     |
|                       [C6215](../code-quality/c6215.md)                        |                                                    强制转换为 BOOL 到 HRESULT 的无效                                                     |
|                       [C6216](../code-quality/c6216.md)                        |                                           编译器插入的强制转换无效 BOOL 到 HRESULT                                            |
|                       [C6217](../code-quality/c6217.md)                        |                                                    使用 NOT 无效 HRESULT 测试                                                    |
|                       [C6220](../code-quality/c6220.md)                        |                                                    无效的 HRESULT 与-1 的比较                                                    |
|                       [C6226](../code-quality/c6226.md)                        |                                                  无效的 HRESULT 到-1 的赋值                                                   |
|                       [C6230](../code-quality/c6230.md)                        |                                                   无效的 HRESULT 用作 Boolean                                                    |
|                       [C6235](../code-quality/c6235.md)                        |                                                  非零常量的逻辑-或                                                  |
|                       [C6236](../code-quality/c6236.md)                        |                                                  逻辑-或使用非零常量                                                  |
|                       [C6237](../code-quality/c6237.md)                        |                                              零的逻辑的运算丧失副作用                                               |
|                       [C6242](../code-quality/c6242.md)                        |                                                         强制执行局部回退                                                         |
|                       [C6248](../code-quality/c6248.md)                        |                                                         正在创建 Null DACL                                                          |
|                       [C6250](../code-quality/c6250.md)                        |                                                   未释放的地址说明符                                                    |
|                       [C6255](../code-quality/c6255.md)                        |                                                      未受保护的 Alloca 用法                                                      |
|                       [C6258](../code-quality/c6258.md)                        |                                                       使用终止线程                                                        |
|                       [C6259](../code-quality/c6259.md)                        |                                               死信中的代码的按位的或限制开关                                                |
|                       [C6260](../code-quality/c6260.md)                        |                                                       使用的字节算术                                                        |
|                       [C6262](../code-quality/c6262.md)                        |                                                        堆栈使用过多                                                        |
|                       [C6263](../code-quality/c6263.md)                        |                                                        使用在循环中的 Alloca                                                         |
|                       [C6268](../code-quality/c6268.md)                        |                                                     强制转换中缺少括号                                                     |
|                       [C6269](../code-quality/c6269.md)                        |                                                     指针取消引用被忽略                                                     |
|                       [C6270](../code-quality/c6270.md)                        |                                              缺少 Format 函数的浮点型自变量                                              |
|                       [C6271](../code-quality/c6271.md)                        |                                                  Format 函数的额外自变量                                                  |
|                       [C6272](../code-quality/c6272.md)                        |                                                Format 函数的非浮点型自变量                                                |
|                       [C6273](../code-quality/c6273.md)                        |                                               格式函数的非整型参数                                                |
|                       [C6274](../code-quality/c6274.md)                        |                                              Format 函数的非字符自变量                                              |
|                       [C6276](../code-quality/c6276.md)                        |                                                         无效字符串的强制转换                                                         |
|                       [C6277](../code-quality/c6277.md)                        |                                                     无效 CreateProcess 的调用                                                      |
|                       [C6278](../code-quality/c6278.md)                        |                                                  数组新建与标量删除不匹配                                                   |
|                       [C6279](../code-quality/c6279.md)                        |                                                  标量新建与数组删除不匹配                                                   |
|                       [C6280](../code-quality/c6280.md)                        |                                               内存分配与解除分配不匹配                                               |
|                       [C6281](../code-quality/c6281.md)                        |                                                     按位关系优先顺序                                                     |
|                       [C6282](../code-quality/c6282.md)                        |                                                      赋值替换测试                                                       |
|                       [C6283](../code-quality/c6283.md)                        |                                             基元数组新建与标量删除不匹配                                              |
|                       [C6284](../code-quality/c6284.md)                        |                                             Format 函数的无效对象自变量                                              |
|                       [C6285](../code-quality/c6285.md)                        |                                                       逻辑-或常量                                                       |
|                       [C6286](../code-quality/c6286.md)                        |                                               非零逻辑的或丢失的负面影响                                               |
|                       [C6287](../code-quality/c6287.md)                        |                                                           冗余测试                                                            |
|                       [C6288](../code-quality/c6288.md)                        |                                             通过逻辑的互含运算的和为 False                                              |
|                       [C6289](../code-quality/c6289.md)                        |                                              通过逻辑互相排斥的或为 True                                               |
|                       [C6290](../code-quality/c6290.md)                        |                                                 逻辑非和按位与的优先级                                                  |
|                       [C6291](../code-quality/c6291.md)                        |                                                  逻辑非和按位或的优先级                                                  |
|                       [C6292](../code-quality/c6292.md)                        |                                                     循环开始计数最多从最大值                                                     |
|                       [C6293](../code-quality/c6293.md)                        |                                                    循环从最小值向下计数                                                    |
|                       [C6294](../code-quality/c6294.md)                        |                                                      从未执行循环体                                                       |
|                       [C6295](../code-quality/c6295.md)                        |                                                            无限循环                                                            |
|                       [C6296](../code-quality/c6296.md)                        |                                                       仅执行一次的循环                                                       |
|                       [C6297](../code-quality/c6297.md)                        |                                                 移位结果强制转换为更大的大小                                                 |
|                       [C6299](../code-quality/c6299.md)                        |                                                   位域到布尔比较                                                    |
|                       [C6302](../code-quality/c6302.md)                        |                                        Format 函数的无效字符串自变量                                         |
|                       [C6303](../code-quality/c6303.md)                        |                                      Format 函数的无效宽字符串自变量                                      |
|                       [C6305](../code-quality/c6305.md)                        |                                                    不匹配的大小和计数的使用                                                    |
|                       [C6306](../code-quality/c6306.md)                        |                                              不正确的变量自变量函数的调用                                              |
|                       [C6308](../code-quality/c6308.md)                        |                                                            Realloc 泄漏                                                             |
|                       [C6310](../code-quality/c6310.md)                        |                                                  非法的异常筛选器常量                                                  |
|                       [C6312](../code-quality/c6312.md)                        |                                                  异常继续执行循环                                                  |
|                       [C6314](../code-quality/c6314.md)                        |                                                        按位的或优先顺序                                                        |
|                       [C6317](../code-quality/c6317.md)                        |                                                         非非补                                                          |
|                       [C6318](../code-quality/c6318.md)                        |                                                      异常继续搜索                                                      |
|                       [C6319](../code-quality/c6319.md)                        |                                                          按逗号忽略                                                           |
|                       [C6324](../code-quality/c6324.md)                        |                                                字符串复制而不是字符串比较                                                |
|                       [C6328](../code-quality/c6328.md)                        |                                                  可能的自变量类型不匹配                                                   |
|                       [C6331](../code-quality/c6331.md)                        |                                                      VirtualFree 无效标志                                                      |
|                       [C6332](../code-quality/c6332.md)                        |                                                    VirtualFree 无效参数                                                    |
|                       [C6333](../code-quality/c6333.md)                        |                                                      VirtualFree 无效大小                                                       |
|                       [C6335](../code-quality/c6335.md)                        |                                                       泄漏进程句柄                                                        |
|                       [C6381](../code-quality/c6381.md)                        |                                                    关机信息缺失                                                     |
|                       [C6383](../code-quality/c6383.md)                        |                                               元素计数字节的计数缓冲区溢出                                               |
|                       [C6384](../code-quality/c6384.md)                        |                                                        指针大小划分                                                        |
|                       [C6385](../code-quality/c6385.md)                        |                                                            读取溢出                                                             |
|                       [C6386](../code-quality/c6386.md)                        |                                                            写入溢出                                                            |
|                       [C6387](../code-quality/c6387.md)                        |                                                       无效的参数值                                                       |
|                       [C6388](../code-quality/c6388.md)                        |                                                       无效的参数值                                                       |
|                       [C6500](../code-quality/c6500.md)                        |                                                     无效的特性属性                                                      |
|                       [C6501](../code-quality/c6501.md)                        |                                                冲突的特性属性值                                                |
|                       [C6503](../code-quality/c6503.md)                        |                                                      引用不能为 Null                                                      |
|                       [C6504](../code-quality/c6504.md)                        |                                                         在非指针参数中为 Null                                                         |
|                       [C6505](../code-quality/c6505.md)                        |                                                          对 Void 类型使用 MustCheck 属性                                                          |
|                       [C6506](../code-quality/c6506.md)                        |                                                 非指针参数或数组的缓冲区大小                                                 |
| [C6507](https://msdn.microsoft.com/18f88cd1-d035-4403-a6a4-12dd0affcf21)  |                                                  取消引用零处的 Null 不匹配                                                  |
|                       [C6508](../code-quality/c6508.md)                        |                                                      常量缓冲区上的写入权限                                                       |
|                       [C6509](../code-quality/c6509.md)                        |                                                     返回使用的前置条件                                                     |
|                       [C6510](../code-quality/c6510.md)                        |                                                   在非指针参数中以 Null 结尾的参数                                                    |
|                       [C6511](../code-quality/c6511.md)                        |                                                     MustCheck 属性必须为 Yes 或 No                                                     |
|                       [C6513](../code-quality/c6513.md)                        |                                                  没有缓冲区大小的元素大小                                                   |
|                       [C6514](../code-quality/c6514.md)                        |                                                   缓冲区大小超过数组大小                                                    |
|                       [C6515](../code-quality/c6515.md)                        |                                                     非指针参数的缓冲区大小                                                      |
|                       [C6516](../code-quality/c6516.md)                        |                                                     在特性上无属性                                                      |
|                       [C6517](../code-quality/c6517.md)                        |                                                  有效的不可读缓冲区的大小                                                  |
|                       [C6518](../code-quality/c6518.md)                        |                                                不可写的缓冲区的可写入大小                                                 |
| [C6521](https://msdn.microsoft.com/e98d0ae3-6f13-47b2-9a15-15d4055af9ef)  |                                                   取消引用无效大小的字符串                                                   |
|                       [C6522](../code-quality/c6522.md)                        |                                                      无效大小的字符串类型                                                       |
| [C6523](https://msdn.microsoft.com/11397a31-b224-46b0-afb7-d49ca576a3bb)  |                                                    无效大小的字符串参数                                                    |
|                       [C6525](../code-quality/c6525.md)                        |                                              无效大小字符串的不可访问的位置                                               |
| [C6526](https://msdn.microsoft.com/59c590c7-0098-4166-a1ac-87f324596002)  |                                                   无效大小的字符串缓冲区类型                                                   |
|                       [C6527](../code-quality/c6527.md)                        |                         无效的批注：NeedsRelease 属性不用于 void 类型的值                          |
|                       [C6530](../code-quality/c6530.md)                        |                                                  无法识别的格式字符串样式                                                   |
|                       [C6540](../code-quality/c6540.md)                        |            对该函数使用属性批注将使其现有的所有 __declspec 批注无效             |
|                       [C6551](../code-quality/c6551.md)                        |                                         大小规范无效：表达式不可分析                                         |
|                       [C6552](../code-quality/c6552.md)                        |                                         Deref= 或 Notref= 无效：表达式不可分析                                          |
|                       [C6701](../code-quality/c6701.md)                        |                                             该值不是有效的 Yes/No/Maybe 值                                             |
|                       [C6702](../code-quality/c6702.md)                        |                                                   该值不是字符串值                                                   |
|                       [C6703](../code-quality/c6703.md)                        |                                                      该值不是一个数字                                                      |
|                       [C6704](../code-quality/c6704.md)                        |                                               意外的批注表达式错误                                                |
|                       [C6705](../code-quality/c6705.md)                        |                批注自变量的预期数量与批注自变量的实际数量不匹配                 |
|                       [C6706](../code-quality/c6706.md)                        |                                             批注的意外批注错误                                              |
|                       [C6995](../code-quality/c6995.md)                        |                                                     未能保存 XML 日志文件                                                     |
|                      [C26100](../code-quality/c26100.md)                       |                                                           争用条件                                                            |
|                      [C26101](../code-quality/c26101.md)                       |                                            未能正确使用联锁的操作                                            |
|                      [C26110](../code-quality/c26110.md)                       |                                                     调用方未能持有锁                                                     |
|                      [C26111](../code-quality/c26111.md)                       |                                                   调用方未能解除锁                                                    |
|                      [C26112](../code-quality/c26112.md)                       |                                                     调用方无法持有任何锁                                                     |
|                      [C26115](../code-quality/c26115.md)                       |                                                       未能解除锁                                                       |
|                      [C26116](../code-quality/c26116.md)                       |                                                 未能获取或持有锁                                                  |
|                      [C26117](../code-quality/c26117.md)                       |                                                        解除未持有的锁                                                        |
|                      [C26140](../code-quality/c26140.md)                       |                                                  并发 SAL 批注错误                                                   |
|                      [C28020](../code-quality/c28020.md)                       |                                               表达式不是此调用，则返回 true                                               |
|                      [C28021](../code-quality/c28021.md)                       |                                           批注的参数必须为指针型                                           |
|                      [C28022](../code-quality/c28022.md)                       |            有关该函数的函数类与使用定义它的 typedef 上的函数类不匹配。            |
|                      [C28023](../code-quality/c28023.md)                       |         分配或传递的函数应有\_Function_class\_至少一个类批注         |
|                      [C28024](../code-quality/c28024.md)                       | 函数指针分配给将批注与函数类，它不包含在函数类的列表。 |
|                      [C28039](../code-quality/c28039.md)                       |                                     实参的类型应与类型完全匹配                                      |
|                      [C28112](../code-quality/c28112.md)                       |            通过 Interlocked 函数访问的变量始终必须通过 Interlocked 函数访问。            |
|                      [C28113](../code-quality/c28113.md)                       |                                       访问通过 Interlocked 函数的本地变量                                        |
|                      [C28125](../code-quality/c28125.md)                       |                                     必须从调用该函数，在一个 try / except 块                                      |
|                      [C28137](../code-quality/c28137.md)                       |                                    变量参数应为 （文本） 常量                                     |
|                      [C28138](../code-quality/c28138.md)                       |                                          常量参数应改为变量                                           |
|                      [C28159](../code-quality/c28159.md)                       |                                              请考虑改为使用另一个函数。                                               |
|                      [C28160](../code-quality/c28160.md)                       |                                                          错误批注                                                           |
|                      [C28163](../code-quality/c28163.md)                       |                                 该函数应永远不会调用从在一个 try / except 块                                  |
|                      [C28164](../code-quality/c28164.md)                       |             正在参数传递到需要指向的对象 （不是为指针的指针） 的一个函数             |
|                      [C28182](../code-quality/c28182.md)                       |                    取消引用 NULL 指针。 该指针包含与另一指针相同的 NULL 值。                     |
|                      [C28183](../code-quality/c28183.md)                       |                          参数可能是一个值，并且在指针中找到的值的副本                           |
|                      [C28193](../code-quality/c28193.md)                       |                                          该变量可保存一个必须检查的值                                           |
|                      [C28196](../code-quality/c28196.md)                       |                            不满足的要求。 （表达式不的计算结果为 true。）                            |
|                      [C28202](../code-quality/c28202.md)                       |                                               非法引用非静态成员                                                |
|                      [C28203](../code-quality/c28203.md)                       |                                                对类成员的不明确的引用。                                                 |
|                      [C28205](../code-quality/c28205.md)                       |                                      在非法上下文中使用的 \_Success\_ 或 \_On_failure\_                                       |
|                      [C28206](../code-quality/c28206.md)                       |                                              若左操作数指向结构，则使用“->”                                              |
|                      [C28207](../code-quality/c28207.md)                       |                                                  若左操作数是一个结构，则使用“.”                                                  |
|                      [C28209](../code-quality/c28209.md)                       |                                      符号的声明具有冲突的声明                                       |
|                      [C28210](../code-quality/c28210.md)                       |                            __on_failure 上下文的批注不得位于显式的 pre 上下文中                             |
|                      [C28211](../code-quality/c28211.md)                       |                                            SAL_context 所需的静态上下文名称                                             |
|                      [C28212](../code-quality/c28212.md)                       |                                             批注所需的指针表达式                                              |
|                      [C28213](../code-quality/c28213.md)                       |            \_Use_decl_annotations\_ 批注必须用于引用上一个声明，且不对其进行修改。            |
|                      [C28214](../code-quality/c28214.md)                       |                                              特性参数的名称必须为 p1...p9                                              |
|                      [C28215](../code-quality/c28215.md)                       |                               不能将 typefix 应用于已包含 typefix 的参数                               |
|                      [C28216](../code-quality/c28216.md)                       |                   checkReturn 批注仅应用于特定函数参数的后置条件。                    |
|                      [C28217](../code-quality/c28217.md)                       |                       对于函数，批注的参数数目与在文件中找到的数目不匹配                        |
|                      [C28218](../code-quality/c28218.md)                       |                        对于函数参数，批注的参数不匹配，在文件中找到                         |
|                      [C28219](../code-quality/c28219.md)                       |                            批注中的批注参数所需的枚举成员                            |
|                      [C28220](../code-quality/c28220.md)                       |                             批注中的批注参数所需的整数表达式                              |
|                      [C28221](../code-quality/c28221.md)                       |                                   批注中的参数所需的字符串表达式                                    |
|                      [C28222](../code-quality/c28222.md)                       |                                          批注所需的 __yes、\__no 或 \__maybe                                          |
|                      [C28223](../code-quality/c28223.md)                       |                                  未找到批注和参数所需的标记/标识符                                   |
|                      [C28224](../code-quality/c28224.md)                       |                                                   批注需要参数                                                    |
|                      [C28225](../code-quality/c28225.md)                       |                                未在批注中找到所需参数的正确数目                                 |
|                      [C28226](../code-quality/c28226.md)                       |                                     批注也不能为 PrimOp（在当前声明中）                                     |
|                      [C28227](../code-quality/c28227.md)                       |                                     批注也不能为 PrimOp（请参阅上一个声明）                                      |
|                      [C28228](../code-quality/c28228.md)                       |                                        批注参数：在批注中不能使用类型                                         |
|                      [C28229](../code-quality/c28229.md)                       |                                               批注不支持参数                                                |
|                      [C28230](../code-quality/c28230.md)                       |                                                参数类型没有成员。                                                 |
|                      [C28231](../code-quality/c28231.md)                       |                                                  批注仅在数组上有效                                                  |
|                      [C28232](../code-quality/c28232.md)                       |                                          pre、post 或 deref 不适用于任何批注                                          |
|                      [C28233](../code-quality/c28233.md)                       |                                               pre、post 或 dere 适用于块                                                |
|                      [C28234](../code-quality/c28234.md)                       |                                         __at 表达式不适用于当前函数                                          |
|                      [C28235](../code-quality/c28235.md)                       |                                          函数无法作为批注单独存在                                           |
|                      [C28236](../code-quality/c28236.md)                       |                                           批注无法在表达式中使用                                            |
|                      [C28237](../code-quality/c28237.md)                       |                                         不再支持参数上的批注                                          |
|                      [C28238](../code-quality/c28238.md)                       |                 参数上的批注具有多个值：stringValue 和 longValue。 使用 paramn=xxx                  |
|                      [C28239](../code-quality/c28239.md)                       |             参数上的批注包含两个值 stringValue 或 longValue；paramn=xxx。 仅使用 paramn=xxx              |
|                      [C28240](../code-quality/c28240.md)                       |                                        参数上的批注包含 param2，但不包含 param1                                         |
|                      [C28241](../code-quality/c28241.md)                       |                                     未识别参数上的函数的批注                                      |
|                      [C28243](../code-quality/c28243.md)                       |              参数上函数的批注需要的取消引用次数多于已批注的实际类型所允许的次数              |
|                      [C28244](../code-quality/c28244.md)                       |                            函数的批注包含无法分析参数/外部批注                             |
|                      [C28245](../code-quality/c28245.md)                       |                                函数的批注将在非成员函数上批注“this”                                |
|                      [C28246](../code-quality/c28246.md)                       |                           函数的参数批注与参数的类型不匹配                            |
|                      [C28250](../code-quality/c28250.md)                       |                               函数的批注不一致：上一实例发生错误。                                |
|                      [C28251](../code-quality/c28251.md)                       |                                  函数的批注不一致：该实例发生错误。                                  |
|                      [C28252](../code-quality/c28252.md)                       |                      函数的批注不一致：参数在此实例中包含另一个批注。                      |
|                      [C28253](../code-quality/c28253.md)                       |                      函数的批注不一致：参数在此实例中包含另一个批注。                      |
|                      [C28254](../code-quality/c28254.md)                       |                                          批注中不支持 dynamic_cast<>()                                           |
|                      [C28262](../code-quality/c28262.md)                       |                               对于批注，在函数中找到了批注的语法错误                                |
|                      [C28263](../code-quality/c28263.md)                       |                            在条件批注中找到内部批注的语法错误                            |
|                      [C28267](../code-quality/c28267.md)                       |                               在函数中找到了批注的语法错误。                               |
|                      [C28272](../code-quality/c28272.md)                       |                 在检查参数时，函数的批注与函数声明不一致                 |
|                      [C28273](../code-quality/c28273.md)                       |                               对于函数，线索与函数声明不一致                                |
|                      [C28275](../code-quality/c28275.md)                       |                                              \_Macro_value\_ 的参数值为 null                                               |
|                      [C28279](../code-quality/c28279.md)                       |                                      对于符号，已找到“起始”符号，但没有匹配的“结束”符号                                       |
|                      [C28280](../code-quality/c28280.md)                       |                                      对于符号，已找到“结束”符号，但没有匹配的“起始”符号                                      |
|                      [C28282](../code-quality/c28282.md)                       |                                               格式字符串必须位于前置条件中                                               |
|                      [C28285](../code-quality/c28285.md)                       |                                               对于函数，参数中存在语法错误                                               |
|                      [C28286](../code-quality/c28286.md)                       |                                               对于函数，在其结尾附近出现语法错误                                               |
|                      [C28287](../code-quality/c28287.md)                       |                           对于函数，在 \_At\_() 批注中出现语法错误（无法识别的参数名）                           |
|                      [C28288](../code-quality/c28288.md)                       |                             对于函数，在 \_At\_() 批注中出现语法错误（无效的参数名）                              |
|                      [C28289](../code-quality/c28289.md)                       |                           对于函数：ReadableTo 或 WritableTo 没有限制规范作为参数                           |
|                      [C28290](../code-quality/c28290.md)                       |                      函数的批注包含的外部对象数量多于实际的参数数量                       |
|                      [C28291](../code-quality/c28291.md)                       |                                   deref 级别 0 处的 post null/notnull 对于函数无意义。                                   |
|                      [C28300](../code-quality/c28300.md)                       |                                       运算符的不可兼容类型的表达式操作数                                        |
|                      [C28301](../code-quality/c28301.md)                       |                                          函数的第一个声明中不包含任何批注。                                          |
|                      [C28302](../code-quality/c28302.md)                       |                                        在批注中找到多余的 \_Deref\_ 运算符。                                         |
|                      [C28303](../code-quality/c28303.md)                       |                                      在批注中找到含义模糊的 \_Deref\_ 运算符。                                       |
|                      [C28304](../code-quality/c28304.md)                       |                                发现未正确放置的 \_Notref\_ 运算符被应用到令牌。                                 |
|                      [C28305](../code-quality/c28305.md)                       |                                           在分析标记时发现错误。                                            |
|                      [C28306](../code-quality/c28306.md)                       |                                             参数上的批注已弃用                                              |
|                      [C28307](../code-quality/c28307.md)                       |                                             参数上的批注已弃用                                              |
|                      [C28350](../code-quality/c28350.md)                       |                             批注介绍了无条件适用的情形。                              |
|                      [C28351](../code-quality/c28351.md)                       |                    批注介绍了在条件中无法使用动态值（变量）的位置。                     |
