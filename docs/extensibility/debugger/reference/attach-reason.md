---
title: ATTACH_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ATTACH_REASON
helpviewer_keywords:
- ATTACH_REASON enumeration
ms.assetid: 159fb70b-a344-4ba6-9115-b7eaa16e228f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ca871d9dac2b6f37018af925eece5c1a6f3d1585
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738125"
---
# <a name="attach_reason"></a>ATTACH_REASON
指定调试引擎 (DE) 附加到程序节点的原因。

## <a name="syntax"></a>语法

```cpp
enum enum_ATTACH_REASON {
    ATTACH_REASON_LAUNCH = 0x0001,
    ATTACH_REASON_USER   = 0x0002,
    ATTACH_REASON_AUTO   = 0x0003
};
typedef DWORD ATTACH_REASON;
```

```csharp
public enum enum_ATTACH_REASON {
    ATTACH_REASON_LAUNCH = 0x0001,
    ATTACH_REASON_USER   = 0x0002,
    ATTACH_REASON_AUTO   = 0x0003
};
```

## <a name="fields"></a>字段
`ATTACH_REASON_AUTO`\
附加，因为进程当前处于调试模式。

`ATTACH_REASON_LAUNCH`\
附加，因为进程已启动。

`ATTACH_REASON_USER`\
由于用户请求而附加。

## <a name="remarks"></a>备注
这些值用作 [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法和 [附加](../../../extensibility/debugger/reference/idebugprogramex2-attach.md) 方法的参数。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [附加](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)
