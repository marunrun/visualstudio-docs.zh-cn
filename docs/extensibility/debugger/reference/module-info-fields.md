---
title: MODULE_INFO_FIELDS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO_FIELDS
helpviewer_keywords:
- MODULE_INFO_FIELDS enumeration
ms.assetid: 8bed85f4-235f-4192-b58f-5fad7a4d7a78
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa64147738a916d44b6924f193860f74bd10a855
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714320"
---
# <a name="module_info_fields"></a>MODULE_INFO_FIELDS
指定调试模块信息的标志。

## <a name="syntax"></a>语法

```cpp
enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
typedef DWORD MODULE_INFO_FIELDS;
```

```csharp
public enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
```

## <a name="fields"></a>字段
 `MIF_NONE`\
 初始化/使用结构中没有任何字段。

 `MIF_NAME`\
 初始化/使用`m_bstrName`[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)结构中的字段。

 `MIF_URL`\
 初始化/使用结构`m_bstrUrl`中的`MODULE_INFO`字段。

 `MIF_VERSION`\
 初始化/使用结构`m_bstrVersion`中的`MODULE_INFO`字段。

 `MIF_DEBUGMESSAGE`\
 初始化/使用结构`m_bstrDebugMessage`中的`MODULE_INFO`字段。

 `MIF_LOADADDRESS`\
 初始化/使用结构`m_addrLoadAddress`中的`MODULE_INFO`字段。

 `MIF_PREFFEREDADDRESS`\
 初始化/使用结构`m_addrPreferredLoadAddress`中的`MODULE_INFO`字段。

 `MIF_SIZE`\
 初始化/使用结构`m_dwSize`中的`MODULE_INFO`字段。

 `MIF_LOADORDER`\
 初始化/使用结构`m_dwLoadOrder`中的`MODULE_INFO`字段。

 `MIF_TIMESTAMP`\
 初始化/使用结构`m_TimeStamp`中的`MODULE_INFO`字段。

 `MIF_URLSYMBOLLOCATION`\
 初始化/使用结构`m_bstrUrlSymbolLocation`中的`MODULE_INFO`字段。

 `MIF_FLAGS`\
 初始化/使用结构`m_dwModuleFlags`中的`MODULE_INFO`字段。

 `MIF_ALLFIELDS`\
 初始化/使用`MODULE_INFO`结构中的所有字段。

## <a name="remarks"></a>备注
 这些值作为参数传递给[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)方法，以指示要初始化[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)结构的字段。

 这些值还用于结构中`MODULE_INFO`，以指示使用哪些字段有效。

 这些标志可以稍微结合`OR`。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
