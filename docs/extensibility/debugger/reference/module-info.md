---
title: MODULE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO
helpviewer_keywords:
- MODULE_INFO structure
ms.assetid: f2e06180-1ab3-4eb5-a428-7994cceb61b6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db67710fd7ee71cddf1e7dbee030cb208a1de86c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339113"
---
# <a name="moduleinfo"></a>MODULE_INFO
描述为特定模块 （DLL、 exe 文件或程序集）。

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
 中的标志的组合[MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)枚举，用于指定哪些字段填写。

 `m_bstrName`\
 模块名。

 `m_bstrUrl`\
 模块的 URL。

 `m_bstrVersion`\
 模块版本。

 `m_bstrDebugMessage`\
 可选的消息有关该模块，例如，"无法加载符号。"

 `m_addrLoadAddress`\
 模块加载地址。

 `m_addrPreferredLoadAddress`\
 模块的首选的加载地址。

 `m_dwSize`\
 模块大小。

 `m_dwLoadOrder`\
 模块加载顺序。

 `m_TimeStamp`\
 上次修改符号文件的时间。

 `m_bstrUrlSymbolLocation`\
 符号文件的位置 (例如，"。\\") 指定模块中。 用作起始位置到查找符号的模块。

 `m_dwModuleFlags`\
 中的标志的组合[MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md)枚举，用于描述该模块。

## <a name="remarks"></a>备注
 此结构传递给[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)填写其中的方法。

 此结构对应于中列出的每个模块**模块**窗口。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)
- [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
