---
title: IEnumDebugProcesses2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugProcesses2
helpviewer_keywords:
- IEnumDebugProcesses2
ms.assetid: 06a1368f-10f0-44eb-af61-e388c2327111
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8b9fe0e96ade081e8da11b5e1c06c5b45279b10b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80715749"
---
# <a name="ienumdebugprocesses2"></a>IEnumDebugProcesses2
此接口枚举调试端口上运行的进程。

## <a name="syntax"></a>语法

```
IEnumDebugProcesses : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 自定义端口供应商实现此接口，以提供在端口上运行的进程的列表。

## <a name="notes-for-callers"></a>调用方说明
 Visual Studio 将调用 [EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md) 来获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IEnumDebugProcesses2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)|检索枚举序列中指定数目的进程。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugprocesses2-skip.md)|跳过枚举序列中指定数目的进程。|
|[重置](../../../extensibility/debugger/reference/ienumdebugprocesses2-reset.md)|将枚举序列重置到开始处。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugprocesses2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprocesses2-getcount.md)|获取枚举器中的进程数。|

## <a name="remarks"></a>备注
 Visual Studio 使用此接口来填充 " **进程** " 窗口。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)
