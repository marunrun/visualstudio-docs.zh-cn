---
title: EXCEPTION_STATE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EXCEPTION_STATE
helpviewer_keywords:
- EXCEPTION_STATE enumeration
ms.assetid: 597f4f4c-9b70-485c-b5dc-3c2e3aecc664
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cd2e280cd03ae413e0853950d13fbfefb69bc15f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736956"
---
# <a name="exception_state"></a>EXCEPTION_STATE
指定异常状态。

## <a name="syntax"></a>语法

```cpp
enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
typedef DWORD EXCEPTION_STATE;
```

```csharp
public enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
```

## <a name="fields"></a>字段
`EXCEPTION_NONE`\
不要停止在异常。

`EXCEPTION_STOP_FIRST_CHANCE`\
在首先触发异常时停止。 描述异常事件时，此标志指示异常事件是第一次异常事件。

`EXCEPTION_STOP_SECOND_CHANCE`\
在异常的第二次触发时停止。 描述异常事件时，指示异常事件是第二个异常事件。

`EXCEPTION_STOP_USER_FIRST_CHANCE`\
首先触发用户模式异常时停止。 描述异常事件时，指示异常事件是第一次用户异常事件。

`EXCEPTION_STOP_USER_UNCAUGHT`\
未捕获用户模式异常时停止。 描述异常事件时，指示异常事件是未捕获的用户模式异常事件。

`EXCEPTION_STOP_ALL`\
停止任何异常。 描述异常事件时未使用。

`EXCEPTION_CANNOT_BE_CONTINUED`\
描述异常事件时，指示无法继续从 中继续异常。

`EXCEPTION_CODE_SUPPORTED`\
指示异常具有支持它的代码。 用于显示异常

`EXCEPTION_CODE_DISPLAY_IN_HEX`\
指示异常代码应显示在十六进制中。 用于显示异常。

`EXCEPTION_JUST_MY_CODE_SUPPORTED`\
指示异常代码支持 JustMyCode。 用于显示异常。

`EXCEPTION_MANAGED_DEBUG_ASSISTANT`\
指示托管代码调试器应处理异常。 如果未设置，则默认调试器处理异常。 这将传递给[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)方法，并且未在[EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)结构中使用。

`EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT`\
过时，请勿使用。

`EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT`\
过时，请勿使用。

`EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT`\
过时，请勿使用。

`EXCEPTION_STOP_USER_SECOND_CHANCE_USE_PARENT`\
过时，请勿使用。

## <a name="remarks"></a>备注
用作EXCEPTION_INFO结构`dwState`的成员，用于[EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)指示异常的状态以及可以对此执行哪些措施。

这些值也会传递给[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)方法，以设置所有异常的状态。

这些标志可以与位或组合。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)
