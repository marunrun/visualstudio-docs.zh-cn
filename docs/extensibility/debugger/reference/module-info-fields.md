---
title: MODULE_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO_FIELDS
helpviewer_keywords:
- MODULE_INFO_FIELDS enumeration
ms.assetid: 8bed85f4-235f-4192-b58f-5fad7a4d7a78
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2ba419d0b10174e375cd15313fbc0770bf9d8cc0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311380"
---
# <a name="moduleinfofields"></a>MODULE_INFO_FIELDS
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
 初始化/使用无结构中的字段。

 `MIF_NAME`\
 初始化/用`m_bstrName`字段中[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)结构。

 `MIF_URL`\
 初始化/用`m_bstrUrl`字段中`MODULE_INFO`结构。

 `MIF_VERSION`\
 初始化/用`m_bstrVersion`字段中`MODULE_INFO`结构。

 `MIF_DEBUGMESSAGE`\
 初始化/用`m_bstrDebugMessage`字段中`MODULE_INFO`结构。

 `MIF_LOADADDRESS`\
 初始化/用`m_addrLoadAddress`字段中`MODULE_INFO`结构。

 `MIF_PREFFEREDADDRESS`\
 初始化/用`m_addrPreferredLoadAddress`字段中`MODULE_INFO`结构。

 `MIF_SIZE`\
 初始化/用`m_dwSize`字段中`MODULE_INFO`结构。

 `MIF_LOADORDER`\
 初始化/用`m_dwLoadOrder`字段中`MODULE_INFO`结构。

 `MIF_TIMESTAMP`\
 初始化/用`m_TimeStamp`字段中`MODULE_INFO`结构。

 `MIF_URLSYMBOLLOCATION`\
 初始化/用`m_bstrUrlSymbolLocation`字段中`MODULE_INFO`结构。

 `MIF_FLAGS`\
 初始化/用`m_dwModuleFlags`字段中`MODULE_INFO`结构。

 `MIF_ALLFIELDS`\
 中的字段的所有初始化/使用`MODULE_INFO`结构。

## <a name="remarks"></a>备注
 这些值会作为参数传递[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)方法，以指示的哪些字段[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)结构是进行初始化。

 中还使用这些值`MODULE_INFO`结构，用于指示哪些字段是使用，有效。

 可能的按位组合这些标志`OR`。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)