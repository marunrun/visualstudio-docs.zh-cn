---
title: 枚举 （Visual Studio 调试） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- enumerations [Visual Studio SDK]
- debugging [Debugging SDK], enumerations
ms.assetid: 557065bf-081f-4d57-8744-bae02b8a5a6e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1cc4f811c1b1651d6ac5807f754a2d9c97eda2ad
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66337899"
---
# <a name="enumerations-visual-studio-debugging"></a>枚举 (Visual Studio Debugging)
以下是枚举[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试 SDK。

- [AD_PROCESS_ID_TYPE](../../../extensibility/debugger/reference/ad-process-id-type.md)指定如何解释中的进程 ID [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构。

- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)指定地址的类型。

- [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)指定程序集所在的位置。

- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)指定调试引擎 (DE) 的原因，若要将附加到程序节点。

- [BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md)指定断点条件的挂起的样式和绑定断点。

- [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)指定断点的错误类型。

- [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)提供可能用于设置一个断点时指定的其他信息的可选标志。

- [BP_FLAGS90](../../../extensibility/debugger/reference/bp-flags90.md)枚举可用于设置一个断点时指定的附加信息的可选标志的有效值。 此枚举扩展[BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)枚举。

- [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md)指定断点请求断点的位置类型。

- [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)指定将导致触发断点的断点传递计数与相关联的条件。

- [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md)指定是否模拟数据断点或中实现的硬件。

- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)指定绑定的断点以及是否启用它是否存在。

- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)指定断点在代码位置、 是一个数据位置，或另一种类型的断点。

- [BP_UNBOUND_REASON](../../../extensibility/debugger/reference/bp-unbound-reason.md)提供断点是未绑定的原因。

- [BPERESI_FIELDS](../../../extensibility/debugger/reference/bperesi-fields.md)指定要检索有关失败的解决方法的断点信息。

- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)指定要检索有关断点请求信息。

- [BPREQI_FIELDS90](../../../extensibility/debugger/reference/bpreqi-fields90.md)枚举指定断点请求有关的信息要检索的有效值。 此枚举扩展[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)枚举。

- [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md)指定哪些信息是要检索有关断点的成功的解决方法。

- [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)用于确定程序可以停止在到达执行的特定点后执行。

- [CONNECTION_PROTOCOL](../../../extensibility/debugger/reference/connection-protocol.md)一个值，指示正在使用调试服务器和调试包之间进行通信的协议。

- [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md)选择不同类型的构造函数。

- [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)指定用于比较两个内存上下文的条件。

- [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)指定要检索有关内存上下文信息。

- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)描述各种特性[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)或[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)接口。

- [DEBUG_REASON](../../../extensibility/debugger/reference/debug-reason.md)为什么要进行调试中启动进程的指定。

- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)指定要检索有关调试属性对象的信息。

- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)指定要检索有关调试引用对象的信息。

- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)指定反汇编的标志。

- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)指定要检索有关反汇编字段信息。

- [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md)指定反汇编流的作用域。

- [DisplayKind](../../../extensibility/debugger/reference/displaykind.md)枚举的有效的值表示类型的信息，以便从让[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象，并向用户显示。

- [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)指定用于比较两个文档上下文的条件。

- [DUMPTYPE](../../../extensibility/debugger/reference/dumptype.md)指定要转储的程序的状态。

- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)指定如何解释的类型[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。

- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)表示编辑并继续的原因不可用。

- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)指定用于控制表达式求值的标志。

- [EVALFLAGS90](../../../extensibility/debugger/reference/evalflags90.md)枚举的有效值的控制表达式求值的标志。 此枚举扩展[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)枚举。

- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)指定事件属性。

- [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)指定的异常状态。

- [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md)指定要检索有关其信息[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。

- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)指定的字段中包含的类型[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。

- [FIELD_KIND_EX](../../../extensibility/debugger/reference/field-kind-ex.md)枚举其他类型的字段[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象可包含。 此枚举扩展[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)枚举。

- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)指定字段类型修饰符。

- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)指定要检索的堆栈帧对象有关的信息。

- [GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md)指定主机名的类型。

- [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md)指定要从中检索文件的名称类型。

- [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)指定截获异常时要执行的操作。

- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)指定程序的启动方式。

- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)指定要检索特定计算机的信息种类。

- [MACHINE_INFO_FLAGS](../../../extensibility/debugger/reference/machine-info-flags.md)用于描述一台计算机。

- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)指定的消息类型和原因。

- [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md)用于描述模块。

- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)指定调试模块信息的标志。

- [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md)指定符号的模块的状态。

- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)选择用于匹配名称的大小写选项。

- [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md)指定的表达式计算器中的对象的类型。

- [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)指定如何分析表达式。

- [PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md)指定挂起断点 （尚未绑定的断点） 的状态。

- [PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md)指定挂起断点的状态标志。

- [PORT_SUPPLIER_DESCRIPTION_FLAGS](../../../extensibility/debugger/reference/port-supplier-description-flags.md)定义可以检索有关端口提供程序的元数据。

- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)指定何种信息来检索进程。

- [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)描述或指定进程的属性。

- [PROGRAM_DESTROY_FLAGS](../../../extensibility/debugger/reference/program-destroy-flags.md)枚举有效的程序值销毁标志。

- [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)指定与程序提供程序关联的属性。

- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)指定所需属性从程序提供程序中获得。

- [REFERENCE_COMPARE](../../../extensibility/debugger/reference/reference-compare.md)指定的比较引用的类型。

- [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)指定引用类型。

- [SEEK_START](../../../extensibility/debugger/reference/seek-start.md)指定从其开始在反汇编中查找的位置。

- [STEPKIND](../../../extensibility/debugger/reference/stepkind.md)指定用于单步执行步骤种类。

- [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)单步执行指定单步执行单元。

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)指定要检索的符号信息的种类。

- [TEXT_DOC_ATTR_2](../../../extensibility/debugger/reference/text-doc-attr-2.md)介绍文档的属性。

- [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)指定有关要检索的线程的哪些信息。

- [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)指定线程的状态。

## <a name="requirements"></a>要求
 标头： msdbg.h、 sh.h 或 ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)