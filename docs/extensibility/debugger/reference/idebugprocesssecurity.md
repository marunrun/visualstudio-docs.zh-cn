---
title: IDebugProcessSecurity | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity interface
ms.assetid: 8a52ddca-bd99-49c0-9778-469dce7abd44
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 74202c4342ae5880f277299b6bb94dcdadff26f5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311423"
---
# <a name="idebugprocesssecurity"></a>IDebugProcessSecurity
`IDebugProcessSecurity` 被实现端口提供程序来警告用户，附加到进程是不安全的。

## <a name="syntax"></a>语法

```
IDebugProcessSecurity : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugProcessSecurity`。

|方法|描述|
|------------|-----------------|
|[GetUserName](../../../extensibility/debugger/reference/idebugprocesssecurity-getusername.md)|从端口提供程序获取用户名称。|
|[QueryCanSafelyAttach](../../../extensibility/debugger/reference/idebugprocesssecurity-querycansafelyattach.md)|警告用户将附加到调试过程是不安全。|

## <a name="remarks"></a>备注
 实现此接口可显示一条警告，并允许用户取消如果要附加的过程可被视为不安全。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [端口](../../../extensibility/debugger/ports.md)
- [端口提供程序](../../../extensibility/debugger/port-suppliers.md)
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)