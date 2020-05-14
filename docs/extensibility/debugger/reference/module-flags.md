---
title: MODULE_FLAGS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_FLAGS
helpviewer_keywords:
- MODULE_FLAGS enumeration
ms.assetid: 0e555b42-b846-4dbb-812e-8e3d11c85b2d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 78c7f24d64ffca667706c3b2fcebeffad16a9d85
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714252"
---
# <a name="module_flags"></a>MODULE_FLAGS
用于描述模块。

## <a name="syntax"></a>语法

```cpp
enum enum_MODULE_FLAGS { 
   MODULE_FLAG_NONE        = 0x0000,
   MODULE_FLAG_SYSTEM      = 0x0001,
   MODULE_FLAG_SYMBOLS     = 0x0002,
   MODULE_FLAG_64BIT       = 0x0004,
   MODULE_FLAG_OPTIMIZED   = 0x0008,
   MODULE_FLAG_UNOPTIMIZED = 0x0010
};
typedef DWORD MODULE_FLAGS;
```

```csharp
public enum enum_MODULE_FLAGS { 
   MODULE_FLAG_NONE        = 0x0000,
   MODULE_FLAG_SYSTEM      = 0x0001,
   MODULE_FLAG_SYMBOLS     = 0x0002,
   MODULE_FLAG_64BIT       = 0x0004,
   MODULE_FLAG_OPTIMIZED   = 0x0008,
   MODULE_FLAG_UNOPTIMIZED = 0x0010
};
```

## <a name="fields"></a>字段
 `MODULE_FLAG_NONE`\
 未指定任何模块。

 `MODULE_FLAG_SYSTEM`\
 指定系统模块。

 `MODULE_FLAG_SYMBOLS`\
 指定符号模块。

 `MODULE_FLAG_64BIT`\
 指定 64 位模块。

 `MODULE_FLAG_OPTIMIZED`\
 指定模块已优化。 此状态反映在 **"模块"** 窗口中。

 `MODULE_FLAG_UNOPTIMIZED`\
 指定模块尚未优化。 此状态反映在 **"模块"** 窗口中。 这是默认状态。

## <a name="remarks"></a>备注
 用于[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)结构`m_dwModuleFlags`的成员。

 这些标志可以稍微结合`OR`。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
