---
title: PENDING_BP_STATE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PENDING_BP_STATE
helpviewer_keywords:
- PENDING_BP_STATE enumeration
ms.assetid: ac04ad72-fa92-4a15-ade2-0d0bbbadfc7f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6707c09e409e2a04d7afec0322b575a70cea33cf
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349875"
---
# <a name="pendingbpstate"></a>PENDING_BP_STATE
指定挂起断点 （尚未绑定的断点） 的状态。

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
 零占位符。 永远不会返回此值。

 `PBPS_DELETED`\
 指示挂起断点已被删除。

 `PBPS_DISABLED`\
 指示挂起断点已禁用。

 `PBPS_ENABLED`\
 指示启用了挂起断点。

## <a name="remarks"></a>备注
 使用作为`state`的成员[PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)结构。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)