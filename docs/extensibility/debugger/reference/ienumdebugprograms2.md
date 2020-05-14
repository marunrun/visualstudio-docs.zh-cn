---
title: IEnum调试程序2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2
helpviewer_keywords:
- IEnumDebugPrograms2
ms.assetid: 7fbb8fb7-db64-4546-a364-dc668430c8af
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1717397d9ff073642c7b6bc25ad85babe76d684c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715573"
---
# <a name="ienumdebugprograms2"></a>IEnumDebugPrograms2
此接口枚举在当前调试会话中运行的程序。

## <a name="syntax"></a>语法

```
IEnumDebugPrograms2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口，以提供 DE 正在调试的程序的列表。

## <a name="notes-for-callers"></a>呼叫者备注
 Visual Studio 调用[枚举程序](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)以获取此接口。 [视觉工作室不使用枚举程序](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugPrograms2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)|在枚举序列中检索指定数量的程序。|
|[跳](../../../extensibility/debugger/reference/ienumdebugprograms2-skip.md)|在枚举序列中跳过指定数量的程序。|
|[重置](../../../extensibility/debugger/reference/ienumdebugprograms2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugprograms2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprograms2-getcount.md)|获取枚举器中的程序数。|

## <a name="remarks"></a>备注
 Visual Studio 使用此界面：

- 填充**模块**窗口（通过调用[EnumProgram，](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)然后在每个程序上调用[EnumModule）。](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)

- 填充**附加到进程**列表（通过调用`IDebugProcess2::EnumPrograms`，然后调用每个[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) [接口上的查询接口](/cpp/atl/queryinterface)以获取[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)接口）。

- 生成可以调试过程中每个程序的 D 的 D 列表（使用[GetEngineInfo）。](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)

- 对每个程序应用编辑和继续 （ENC） 更新（通过调用 IDebugProcess2：：：枚举程序，然后调用[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)）。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)
