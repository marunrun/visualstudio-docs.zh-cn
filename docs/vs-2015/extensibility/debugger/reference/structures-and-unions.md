---
title: 结构和联合 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- structures [Visual Studio SDK]
ms.assetid: 9ff0a8f8-1ee6-4fdd-8b80-206436ff589b
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f882eae12e700fe86ab747cc7ffbe3b5744298af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204838"
---
# <a name="structures-and-unions"></a>结构和联合
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

下面是 Visual Studio 调试 SDK 中的结构和联合。  
  
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)  
 指定进程 ID，该 ID 可以是系统 ID 或 GUID。  
  
 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)  
 描述引发断点的条件。  
  
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)  
 描述错误断点的解决方法，包括位置、程序和线程。  
  
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)  
 指定用于描述断点位置的结构类型。  
  
 [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)  
 定义用于描述代码中某个地址处的断点位置的组件。  
  
 [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)  
 描述直接绑定到正在调试的程序中的地址的断点位置。  
  
 [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)  
 描述代码源文件中的行的位置。  
  
 [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)  
 描述代码中某个函数的断点偏移位置。  
  
 [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)  
 用于根据用户可从 IDE 中输入的字符串设置代码断点。  
  
 [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)  
 用于设置数据断点，这些断点基于用户可从 IDE 中输入的字符串。  
  
 [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)  
 描述特定位置的断点解析。  
  
 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)  
 描述在之前传递了断点的计数和条件。  
  
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)  
 包含实现断点所需的信息。  
  
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)  
 包含实现断点所需的信息 (与 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 结构相同，但) 提供供应商 GUID、约束和跟踪点信息。  
  
 [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)  
 描述代码断点的位置。  
  
 [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)  
 描述绑定数据断点的结果。  
  
 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)  
 描述代码断点或数据断点的绑定断点信息。  
  
 [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)  
 指定断点解析位置的结构。  
  
 [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md)  
 描述字符串的数组。  
  
 [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)  
 指定来自元数据的字段类型的相关信息。  
  
 [CODE_PATH](../../../extensibility/debugger/reference/code-path.md)  
 描述对函数或方法的调用。  
  
 [COMPUTER_INFO](../../../extensibility/debugger/reference/computer-info.md)  
 描述运行调试器的计算机。  
  
 [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)  
 介绍 Guid 列表。  
  
 [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)  
 描述内存上下文或代码上下文。  
  
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)  
 描述正在调试的程序中的地址。  
  
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)  
 表示多种不同类型的地址之一。  
  
 [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)  
 标识自定义查看器或类型可视化工具。  
  
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)  
 描述一个调试属性，该属性反过来描述具有名称、类型和值的分层性质的对象。  
  
 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)  
 描述引用。  
  
 [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)  
 介绍如何在 IDE 中显示。  
  
 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)  
 描述由正在调试的程序引发的异常或运行时错误。  
  
 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)  
 描述本地变量、参数或其他字段。  
  
 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)  
 描述堆栈帧。  
  
 [GUID_ARRAY](../../../extensibility/debugger/reference/guid-array.md)  
 描述可用调试引擎的唯一标识符的数组。  
  
 [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)  
 用于设置模块的 JustMyCode 信息。  
  
 [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)  
 描述特定的计算机。  
  
 [METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)  
 描述数组中的数组元素。  
  
 [METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)  
 描述类或结构的字段的地址。  
  
 [METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)  
 描述一个范围内的本地变量的地址， (通常是函数或方法) 。  
  
 [METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)  
 描述类的方法的地址。  
  
 [METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)  
 描述方法或函数的参数。  
  
 [METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)  
 描述方法或函数的返回值。  
  
 [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)  
 描述取自元数据的字段类型。  
  
 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)  
 描述特定模块 (DLL、EXE 或程序集) 。  
  
 [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)  
 介绍有关已搜索的符号搜索路径的状态信息。  
  
 [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)  
 描述本机地址。  
  
 [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)  
 描述从 PDB 符号获取的字段类型。  
  
 [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)  
 描述准备绑定到代码位置的断点状态。  
  
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)  
 描述进程。  
  
 [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)  
 描述表示程序节点的 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象的列表。  
  
 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)  
 描述在计算机上运行的进程。  
  
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)  
 描述给定文本中的行和列的位置。  
  
 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)  
 介绍线程的属性。  
  
 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)  
 描述字段的类型。  
  
 [UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)  
 描述物理地址。  
  
 [UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)  
 描述与 `this` Visual Basic) 中 (的指针相关的地址 `Me` 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg、sh .h 或 ee  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
