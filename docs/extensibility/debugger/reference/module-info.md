---
title: MODULE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO
helpviewer_keywords:
- MODULE_INFO structure
ms.assetid: f2e06180-1ab3-4eb5-a428-7994cceb61b6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59ab4d0bb2a7aaa4b08f616ea0a99be85b521bb0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80714312"
---
# <a name="module_info"></a>MODULE_INFO
描述特定模块 (DLL、EXE 或程序集) 。

## <a name="syntax"></a>语法

```cpp
typedef struct tagMODULE_INFO { 
   MODULE_INFO_FIELDS dwValidFields;
   BSTR               m_bstrName;
   BSTR               m_bstrUrl;
   BSTR               m_bstrVersion;
   BSTR               m_bstrDebugMessage;
   UINT64             m_addrLoadAddress;
   UINT64             m_addrPreferredLoadAddress;
   DWORD              m_dwSize;
   DWORD              m_dwLoadOrder;
   FILETIME           m_TimeStamp;
   BSTR               m_bstrUrlSymbolLocation;
   MODULE_FLAGS       m_dwModuleFlags;
} MODULE_INFO;
```

```csharp
public struct MODULE_INFO { 
   public uint     dwValidFields;
   public string   m_bstrName;
   public string   m_bstrUrl;
   public string   m_bstrVersion;
   public string   m_bstrDebugMessage;
   public ulong    m_addrLoadAddress;
   public ulong    m_addrPreferredLoadAddress;
   public uint     m_dwSize;
   public uint     m_dwLoadOrder;
   public FILETIME m_TimeStamp;
   public string   m_bstrUrlSymbolLocation;
   public uint     m_dwModuleFlags;
};
```

## <a name="members"></a>成员
 `dwValidFields`\
 [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)枚举中的标志的组合，用于指定要填写的字段。

 `m_bstrName`\
 模块名。

 `m_bstrUrl`\
 模块 URL。

 `m_bstrVersion`\
 模块版本。

 `m_bstrDebugMessage`\
 有关模块的可选消息，例如 "无法加载符号"。

 `m_addrLoadAddress`\
 模块加载地址。

 `m_addrPreferredLoadAddress`\
 模块的首选加载地址。

 `m_dwSize`\
 模块大小。

 `m_dwLoadOrder`\
 模块加载顺序。

 `m_TimeStamp`\
 上次修改符号文件的时间。

 `m_bstrUrlSymbolLocation`\
 符号文件的位置 (例如，". \\ "模块中指定 ) 。 用作查找模块符号的起始位置。

 `m_dwModuleFlags`\
 描述模块的 [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md) 枚举中的标志的组合。

## <a name="remarks"></a>备注
 此结构被传递给 [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md) 方法，其中填充了此结构。

 此结构对应于 " **模块** " 窗口中列出的每个模块。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)
- [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
