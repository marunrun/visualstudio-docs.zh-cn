---
title: PENDING_BP_STATE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PENDING_BP_STATE
helpviewer_keywords:
- PENDING_BP_STATE enumeration
ms.assetid: ac04ad72-fa92-4a15-ade2-0d0bbbadfc7f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 69c8dbe1022ee0b1b2ff034d2b83b947c8fb3df6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713998"
---
# <a name="pending_bp_state"></a>PENDING_BP_STATE
指定挂起断点的状态（尚未绑定的断点）。

## <a name="syntax"></a>语法

```cpp
enum enum_PENDING_BP_STATE { 
   PBPS_NONE     = 0x0000,
   PBPS_DELETED  = 0x0001,
   PBPS_DISABLED = 0x0002,
   PBPS_ENABLED  = 0x0003
};
typedef DWORD PENDING_BP_STATE;
```

```csharp
public enum enum_PENDING_BP_STATE { 
   PBPS_NONE     = 0x0000,
   PBPS_DELETED  = 0x0001,
   PBPS_DISABLED = 0x0002,
   PBPS_ENABLED  = 0x0003
};
```

## <a name="fields"></a>字段
 `PBPS_NONE`\
 占位符为零。 此值永远不会返回。

 `PBPS_DELETED`\
 指示挂起的断点已被删除。

 `PBPS_DISABLED`\
 指示挂起的断点已禁用。

 `PBPS_ENABLED`\
 指示已启用挂起的断点。

## <a name="remarks"></a>备注
 用作[PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)结构`state`的成员。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)
