---
title: CANSTOP_REASON | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CANSTOP_REASON
helpviewer_keywords:
- CANSTOP_REASON enumeration
ms.assetid: 6da944eb-36cd-4a8c-8d71-544c775cfcc1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 18861d7aa19281528e9a100f57399451194598a9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66327255"
---
# <a name="canstopreason"></a>CANSTOP_REASON
用于确定程序可以停止在到达执行的特定点后执行。

## <a name="syntax"></a>语法

```cpp
enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
typedef DWORD CANSTOP_REASON;
```

```csharp
public enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
```

## <a name="fields"></a>字段
`CANSTOP_ENTRYPOINT`\
指定给定的程序的入口点。

`CANSTOP_STEPIN`\
指定单步执行函数。

## <a name="remarks"></a>备注
作为参数传递[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)方法来确认与会话调试管理器 (SDM)，如果，则可以暂时停止或单步执行函数或方法后到达该程序的入口点。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
