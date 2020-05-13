---
title: 枚举（可视化工作室调试） |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- enumerations [Visual Studio SDK]
- debugging [Debugging SDK], enumerations
ms.assetid: 557065bf-081f-4d57-8744-bae02b8a5a6e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 80ad4db1090857d87e28d90d8478fbdea0905e86
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737134"
---
# <a name="enumerations-visual-studio-debugging"></a>枚举 (Visual Studio Debugging)
以下是调试 SDK 的[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]枚举。

- [AD_PROCESS_ID_TYPE](../../../extensibility/debugger/reference/ad-process-id-type.md)指定如何在[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构中解释进程 ID。

- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)指定地址的类型。

- [程序集分解](../../../extensibility/debugger/reference/assemblylocresolution.md)指定程序集的位置。

- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)指定调试引擎 （DE） 附加到程序节点的原因。

- [BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md)指定挂起和绑定断点的断点条件样式。

- [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)指定断点的错误类型。

- [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)提供可选标志，用于在设置断点时指定其他信息。

- [BP_FLAGS90](../../../extensibility/debugger/reference/bp-flags90.md)枚举可选标志的有效值，这些标记可用于在设置断点时指定其他信息。 此枚举扩展了[BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)枚举。

- [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md)指定断点请求的断点的位置类型。

- [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)指定与断点通过计数关联的条件，这将导致断点触发。

- [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md)指定数据断点是在硬件中模拟还是实现。

- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)指定绑定断点是否存在以及是否启用了该断点。

- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)指定断点是位于代码位置、数据位置还是其他类型的断点。

- [BP_UNBOUND_REASON](../../../extensibility/debugger/reference/bp-unbound-reason.md)给出断点未绑定的原因。

- [BPERESI_FIELDS](../../../extensibility/debugger/reference/bperesi-fields.md)指定要检索的关于断点解析失败的信息。

- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)指定要检索的关于断点请求的信息。

- [BPREQI_FIELDS90](../../../extensibility/debugger/reference/bpreqi-fields90.md)枚举指定要检索的关于断点请求的信息的有效值。 此枚举扩展了[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)枚举。

- [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md)指定要检索哪些有关断点成功解析的信息。

- [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)用于确定程序在到达执行中的特定点后是否可以停止执行。

- [CONNECTION_PROTOCOL](../../../extensibility/debugger/reference/connection-protocol.md)指示用于在调试服务器和调试包之间通信的协议的值。

- [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md)选择不同类型的构造函数。

- [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)指定比较两个内存上下文的条件。

- [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)指定要检索有关内存上下文的信息。

- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)描述[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)或[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)接口的各种属性。

- [DEBUG_REASON](../../../extensibility/debugger/reference/debug-reason.md)指定启动进程以进行调试的原因。

- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)指定要检索的有关调试属性对象的哪些信息。

- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)指定要检索的有关调试引用对象的哪些信息。

- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)指定拆卸的标志。

- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)指定要检索的有关拆解字段的信息。

- [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md)指定拆解流的范围。

- [显示金德](../../../extensibility/debugger/reference/displaykind.md)枚举表示要从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象获取的信息类型并显示给用户的有效值。

- [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)指定比较两个文档上下文的条件。

- [转储类型](../../../extensibility/debugger/reference/dumptype.md)指定要转储的程序状态。

- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)指定如何解释[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象的类型。

- [恩奇不可用原因](../../../extensibility/debugger/reference/encunavailablereason.md)表示"编辑"和"继续"不可用的原因。

- [埃瓦尔克](../../../extensibility/debugger/reference/evalflags.md)指定控制表达式计算的标志。

- [EVALFLAGS90](../../../extensibility/debugger/reference/evalflags90.md)枚举控制表达式计算的标志的有效值。 此枚举扩展了[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)枚举。

- [事件属性](../../../extensibility/debugger/reference/eventattributes.md)指定事件属性。

- [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)指定异常状态。

- [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md)指定要检索的关于[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象的信息。

- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)指定[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象中包含的字段类型。

- [FIELD_KIND_EX](../../../extensibility/debugger/reference/field-kind-ex.md)枚举[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象可以包含的其他类型的字段。 此枚举扩展[了FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)枚举。

- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)指定字段类型的修饰符。

- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)指定要检索有关堆栈帧对象的信息。

- [GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md)指定主机名的类型。

- [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md)指定要检索的文件的名称类型。

- [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)指定在拦截异常时要执行的操作。

- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)指定如何启动程序。

- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)指定要检索特定计算机的信息类型。

- [MACHINE_INFO_FLAGS](../../../extensibility/debugger/reference/machine-info-flags.md)用于描述机器。

- [消息类型](../../../extensibility/debugger/reference/messagetype.md)指定消息类型和原因。

- [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md)用于描述模块。

- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)指定调试模块信息的标志。

- [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md)指定模块的符号状态。

- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)选择匹配名称的案例选项。

- [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md)从表达式赋值器指定对象的类型。

- [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)指定如何解析表达式。

- [PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md)指定挂起断点的状态（尚未绑定的断点）。

- [PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md)指定挂起的断点状态标志。

- [PORT_SUPPLIER_DESCRIPTION_FLAGS](../../../extensibility/debugger/reference/port-supplier-description-flags.md)定义可以检索的关于端口供应商的元数据。

- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)指定要检索进程的信息类型。

- [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)描述或指定进程的属性。

- [PROGRAM_DESTROY_FLAGS](../../../extensibility/debugger/reference/program-destroy-flags.md)枚举程序的有效值销毁标志。

- [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)指定与程序提供程序关联的属性。

- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)指定从程序提供程序获取的所需属性。

- [REFERENCE_COMPARE](../../../extensibility/debugger/reference/reference-compare.md)指定引用的比较类型。

- [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)指定引用类型。

- [SEEK_START](../../../extensibility/debugger/reference/seek-start.md)指定在拆解中开始查找的位置。

- [步进](../../../extensibility/debugger/reference/stepkind.md)指定步进的步骤类型。

- [步进单元](../../../extensibility/debugger/reference/stepunit.md)指定步进的步骤单元。

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)指定要检索的符号信息类型。

- [TEXT_DOC_ATTR_2](../../../extensibility/debugger/reference/text-doc-attr-2.md)描述文档的属性。

- [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)指定有关要检索的线程的信息。

- [线程状态](../../../extensibility/debugger/reference/threadstate.md)指定线程的状态。

## <a name="requirements"></a>要求
 标题： msdbg.h、 sh.h 或 ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
