---
title: BP_STATE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_STATE
helpviewer_keywords:
- BP_STATE enumeration
ms.assetid: 08aa6a3f-3e5f-4c83-8eca-7b7b5f8e208d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2721028c0635af274174574e4a264546c1909778
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737797"
---
# <a name="bp_state"></a>BP_STATE
指定绑定断点的存在，并指定是否启用了该断点。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
typedef DWORD BP_STATE;
```

```csharp
public enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
```

## <a name="fields"></a>字段
`BPS_NONE`\
指定不存在断点。

`BPS_DELETED`\
指定断点已被删除。

`BPS_DISABLED`\
指定断点已禁用。

`BPS_ENABLED`\
指定启用断点。

## <a name="remarks"></a>备注
从[GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)方法返回。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [获取状态](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)
