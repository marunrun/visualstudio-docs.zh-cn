---
title: IEnum调试过程2 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715749"
---
# <a name="ienumdebugprocesses2"></a>IEnumDebugProcesses2
此接口枚举在调试端口上运行的进程。

## <a name="syntax"></a>语法

```
IEnumDebugProcesses : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 自定义端口供应商实现此接口以提供在端口上运行的进程的列表。

## <a name="notes-for-callers"></a>呼叫者备注
 可视化工作室调用[Enum 进程](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugProcesses2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)|检索枚举序列中指定数量的进程。|
|[跳](../../../extensibility/debugger/reference/ienumdebugprocesses2-skip.md)|在枚举序列中跳过指定数量的进程。|
|[重置](../../../extensibility/debugger/reference/ienumdebugprocesses2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugprocesses2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprocesses2-getcount.md)|获取枚举器中的进程数。|

## <a name="remarks"></a>备注
 Visual Studio 使用此界面填充 **"进程"** 窗口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)
