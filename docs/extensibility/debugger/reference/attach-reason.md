---
title: ATTACH_REASON | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ATTACH_REASON
helpviewer_keywords:
- ATTACH_REASON enumeration
ms.assetid: 159fb70b-a344-4ba6-9115-b7eaa16e228f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8c132b507d679fd6cec5ce7fff04362159cbc848
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351844"
---
# <a name="attachreason"></a>ATTACH_REASON
指定调试引擎 (DE) 的原因，若要将附加到程序节点。

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
将附加，因为进程当前处于调试模式。

`ATTACH_REASON_LAUNCH`\
将附加，因为启动进程。

`ATTACH_REASON_USER`\
由于用户请求而将附加。

## <a name="remarks"></a>备注
这些值用作参数[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)并[附加](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)方法。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [附加](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)
