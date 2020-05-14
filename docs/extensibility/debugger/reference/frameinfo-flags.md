---
title: FRAMEINFO_FLAGS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FRAMEINFO_FLAGS
helpviewer_keywords:
- FRAMEINFO_FLAGS enumeration
ms.assetid: 41578062-8455-412a-9d8b-1e1e9dc8d52e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3510726400623c5ddf3e7a4d58a4903763b91245
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736797"
---
# <a name="frameinfo_flags"></a>FRAMEINFO_FLAGS
指定要检索有关堆栈帧对象的信息。

## <a name="syntax"></a>语法

```cpp
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

## <a name="fields"></a>字段
`FIF_FUNCNAME`\
初始化/使用`m_bstrFuncName`字段。

`FIF_RETURNTYPE`\
初始化/使用`m_bstrReturnType`字段。

`FIF_ARGS`\
初始化/使用`m_bstrArgs`字段。

`FIF_LANGUAGE`\
初始化/使用`m_bstrLanguage`字段。

`FIF_MODULE`\
初始化/使用`m_bstrModule`字段。

`FIF_STACKRANGE`\
初始化/使用`m_addrMin`和`m_addrMax`（堆栈范围） 字段。

`FIF_FRAME`\
初始化/使用`m_pFrame`字段。

`FIF_DEBUGINFO`\
初始化/使用`m_fHasDebugInfo`字段。

`FIF_STALECODE`\
初始化/使用`m_fStaleCode`字段。

`FIF_ANNOTATEDFRAME`\
初始化/使用`m_fAnnotatedFrame`字段。

`FIF_DEBUG_MODULEP`\
初始化/使用`m_pModule`字段。

`FIF_FUNCNAME_FORMAT`\
设置函数名称的格式。 结果在字段中返回，`m_bstrFunName`并且不会填写其他字段。

`FIF_FUNCNAME_RETURNTYPE`\
将返回类型添加到`m_bstrFuncName`字段中。

`FIF_FUNCNAME_ARGS`\
将参数添加到`m_bstrFuncName`字段中。

`FIF_FUNCNAME_LANGUAGE`\
将语言添加到`m_bstrFuncName`字段中。

`FIF_FUNCNAME_MODULE`\
将模块名称添加到`m_bstrFuncName`字段中。

`FIF_FUNCNAME_LINES`\
将行数添加到`m_bstrFuncName`字段中。

`FIF_FUNCNAME_OFFSET`\
如果`FIF_FUNCNAME_LINES`指定，`m_bstrFuncName`则从行的开头向字段添加偏移量（以字节为单位）。 如果未`FIF_FUNCNAME_LINES`指定，或者如果行号不可用，则从函数的开头添加偏移以字节为单位。

`FIF_FUNCNAME_ARGS_TYPES`\
将每个函数参数的类型添加到`m_bstrFuncName`字段中。

`FIF_FUNCNAME_ARGS_NAMES`\
将每个函数参数的名称添加到`m_bstrFuncName`字段中。

`FIF_FUNCNAME_ARGS_VALUES`\
将每个函数参数的值添加到`m_bstrFuncName`字段中。

`FIF_FUNCNAME_ARGS_ALL`\
将所有参数的类型、名称和值添加到`m_bstrFuncName`字段中。

`FIF_ARGS_TYPES`\
将检索参数类型并设置格式。

`FIF_ARGS_NAMES`\
检索参数名称并设置格式。

`FIF_ARGS_VALUES`\
将检索参数值并设置格式。

`FIF_ARGS_ALL`\
检索并格式化所有参数的类型、名称和值。

`FIF_ARGS_NOFORMAT`\
指定不格式化参数（例如，不要在参数列表周围添加首和闭括号，也不在参数之间添加分隔符）。

`FIF_ARGS_NO_FUNC_EVAL`\
指定在检索参数值时不应使用函数（属性）计算。

`FIF_FILTER_NON_USER_CODE`\
调试引擎是筛选非用户代码帧，以便不包含这些帧。

`FIF_ARGS_NO_TOSTRING`\
返回函数参数`ToString()`时不允许函数计算或格式化。

`FIF_DESIGN_TIME_EXPR_EVAL`\
帧信息应从托管应用域（而不是托管进程）获取。

## <a name="remarks"></a>备注
这些标志将传递给[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)和[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)方法，以指示要在[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构或结构中初始化哪些字段。

这些标志还用于指示在返回结构时使用[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构的哪些字段并有效。 这些值可以稍微结合`OR`。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
