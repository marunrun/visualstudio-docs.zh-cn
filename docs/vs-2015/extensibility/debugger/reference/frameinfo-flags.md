---
title: FRAMEINFO_FLAGS | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- FRAMEINFO_FLAGS
helpviewer_keywords:
- FRAMEINFO_FLAGS enumeration
ms.assetid: 41578062-8455-412a-9d8b-1e1e9dc8d52e
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e5a930e81ff1105ba93ce3c3cff10ee8bff2f7e5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62538429"
---
# <a name="frameinfoflags"></a>FRAMEINFO_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要检索的堆栈帧对象有关的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_FRAMEINFO_FLAGS {  
   FIF_FUNCNAME              = 0x00000001,  
   FIF_RETURNTYPE            = 0x00000002,  
   FIF_ARGS                  = 0x00000004,  
   FIF_LANGUAGE              = 0x00000008,  
   FIF_MODULE                = 0x00000010,  
   FIF_STACKRANGE            = 0x00000020,  
   FIF_FRAME                 = 0x00000040,  
   FIF_DEBUGINFO             = 0x00000080,  
   FIF_STALECODE             = 0x00000100,  
   FIF_ANNOTATEDFRAME        = 0x00000200,  
   FIF_DEBUG_MODULEP         = 0x00000400,  
   FIF_FUNCNAME_FORMAT       = 0x00001000,  
   FIF_FUNCNAME_RETURNTYPE   = 0x00002000,  
   FIF_FUNCNAME_ARGS         = 0x00004000,  
   FIF_FUNCNAME_LANGUAGE     = 0x00008000,  
   FIF_FUNCNAME_MODULE       = 0x00010000,  
   FIF_FUNCNAME_LINES        = 0x00020000,  
   FIF_FUNCNAME_OFFSET       = 0x00040000,  
   FIF_FUNCNAME_ARGS_TYPES   = 0x00100000,  
   FIF_FUNCNAME_ARGS_NAMES   = 0x00200000,  
   FIF_FUNCNAME_ARGS_VALUES  = 0x00400000,  
   FIF_FUNCNAME_ARGS_ALL     = 0x00700000,  
   FIF_ARGS_TYPES            = 0x01000000,  
   FIF_ARGS_NAMES            = 0x02000000,  
   FIF_ARGS_VALUES           = 0x04000000,  
   FIF_ARGS_ALL              = 0x07000000,  
   FIF_ARGS_NOFORMAT         = 0x08000000,  
   FIF_ARGS_NO_FUNC_EVAL     = 0x10000000,  
   FIF_FILTER_NON_USER_CODE  = 0x20000000,  
   FIF_ARGS_NO_TOSTRING      = 0x40000000,  
   FIF_DESIGN_TIME_EXPR_EVAL = 0x80000000  
};  
typedef DWORD FRAMEINFO_FLAGS;  
```  
  
```csharp  
public enum enum_FRAMEINFO_FLAGS {  
   FIF_FUNCNAME              = 0x00000001,  
   FIF_RETURNTYPE            = 0x00000002,  
   FIF_ARGS                  = 0x00000004,  
   FIF_LANGUAGE              = 0x00000008,  
   FIF_MODULE                = 0x00000010,  
   FIF_STACKRANGE            = 0x00000020,  
   FIF_FRAME                 = 0x00000040,  
   FIF_DEBUGINFO             = 0x00000080,  
   FIF_STALECODE             = 0x00000100,  
   FIF_ANNOTATEDFRAME        = 0x00000200,  
   FIF_DEBUG_MODULEP         = 0x00000400,  
   FIF_FUNCNAME_FORMAT       = 0x00001000,  
   FIF_FUNCNAME_RETURNTYPE   = 0x00002000,  
   FIF_FUNCNAME_ARGS         = 0x00004000,  
   FIF_FUNCNAME_LANGUAGE     = 0x00008000,  
   FIF_FUNCNAME_MODULE       = 0x00010000,  
   FIF_FUNCNAME_LINES        = 0x00020000,  
   FIF_FUNCNAME_OFFSET       = 0x00040000,  
   FIF_FUNCNAME_ARGS_TYPES   = 0x00100000,  
   FIF_FUNCNAME_ARGS_NAMES   = 0x00200000,  
   FIF_FUNCNAME_ARGS_VALUES  = 0x00400000,  
   FIF_FUNCNAME_ARGS_ALL     = 0x00700000,  
   FIF_ARGS_TYPES            = 0x01000000,  
   FIF_ARGS_NAMES            = 0x02000000,  
   FIF_ARGS_VALUES           = 0x04000000,  
   FIF_ARGS_ALL              = 0x07000000,  
   FIF_ARGS_NOFORMAT         = 0x08000000,  
   FIF_ARGS_NO_FUNC_EVAL     = 0x10000000,  
   FIF_FILTER_NON_USER_CODE  = 0x20000000,  
   FIF_ARGS_NO_TOSTRING      = 0x40000000,  
   FIF_DESIGN_TIME_EXPR_EVAL = 0x80000000  
};  
```  
  
## <a name="members"></a>成员  
 FIF_FUNCNAME  
 初始化/使用`m_bstrFuncName`字段。  
  
 FIF_RETURNTYPE  
 初始化/使用`m_bstrReturnType`字段。  
  
 FIF_ARGS  
 初始化/使用`m_bstrArgs`字段。  
  
 FIF_LANGUAGE  
 初始化/使用`m_bstrLanguage`字段。  
  
 FIF_MODULE  
 初始化/使用`m_bstrModule`字段。  
  
 FIF_STACKRANGE  
 初始化/用`m_addrMin`和`m_addrMax`（堆栈范围） 字段。  
  
 FIF_FRAME  
 初始化/使用`m_pFrame`字段。  
  
 FIF_DEBUGINFO  
 初始化/使用`m_fHasDebugInfo`字段。  
  
 FIF_STALECODE  
 初始化/使用`m_fStaleCode`字段。  
  
 FIF_ANNOTATEDFRAME  
 初始化/使用`m_fAnnotatedFrame`字段。  
  
 FIF_DEBUG_MODULEP  
 初始化/使用`m_pModule`字段。  
  
 FIF_FUNCNAME_FORMAT  
 设置格式的函数名称。 在返回的结果`m_bstrFunName`填写字段和任何其他字段。  
  
 FIF_FUNCNAME_RETURNTYPE  
 将添加到的返回类型`m_bstrFuncName`字段。  
  
 FIF_FUNCNAME_ARGS  
 将添加到参数`m_bstrFuncName`字段。  
  
 FIF_FUNCNAME_LANGUAGE  
 将添加到语言`m_bstrFuncName`字段。  
  
 FIF_FUNCNAME_MODULE  
 将添加到的模块名称`m_bstrFuncName`字段。  
  
 FIF_FUNCNAME_LINES  
 将添加到的行数`m_bstrFuncName`字段。  
  
 FIF_FUNCNAME_OFFSET  
 将添加到`m_bstrFuncName`字段以字节为单位从行开头的偏移量，如果`FIF_FUNCNAME_LINES`指定。 如果`FIF_FUNCNAME_LINES`未指定，或如果行号不可用，从函数开始将偏移量添加以字节为单位。  
  
 FIF_FUNCNAME_ARGS_TYPES  
 将添加到每个函数自变量的类型`m_bstrFuncName`字段。  
  
 FIF_FUNCNAME_ARGS_NAMES  
 将添加到每个函数参数的名称`m_bstrFuncName`字段。  
  
 FIF_FUNCNAME_ARGS_VALUES  
 将添加到每个函数自变量的值`m_bstrFuncName`字段。  
  
 FIF_FUNCNAME_ARGS_ALL  
 添加类型、 名称和值的所有自变量`m_bstrFuncName`字段。  
  
 FIF_ARGS_TYPES  
 检索自变量类型并将其格式化。  
  
 FIF_ARGS_NAMES  
 参数名称检索并设置格式。  
  
 FIF_ARGS_VALUES  
 检索自变量值并将其格式化。  
  
 FIF_ARGS_ALL  
 检索和格式化类型、 名称和所有参数的值。  
  
 FIF_ARGS_NOFORMAT  
 指定不格式化参数 （例如，进行不添加开始和结束括号的参数列表也不添加参数之间的分隔符）。  
  
 FIF_ARGS_NO_FUNC_EVAL  
 指定检索参数值时不应使用函数 （属性） 求值。  
  
 FIF_FILTER_NON_USER_CODE  
 调试引擎是进行筛选以便不会包含这些非用户代码帧。  
  
 FIF_ARGS_NO_TOSTRING  
 不允许`ToString()`函数求值或格式设置时返回函数自变量。  
  
 FIF_DESIGN_TIME_EXPR_EVAL  
 应从承载的应用程序域而不是宿主进程获取帧信息。  
  
## <a name="remarks"></a>备注  
 这些标志传递给[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)并[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)方法，以指示哪些字段是在初始化[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构。  
  
 这些标志还用于指示哪些字段[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构已使用且有效时返回该结构。 可能的按位组合这些值`OR`。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)   
 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
