---
title: IDebugProcessEx2：：添加隐式程序节点 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 113c81e95e7384be04b7e02a5c58cd2cad7c9c6b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723394"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
此方法为指定的每个调试引擎 （DE） 添加一个程序节点。

## <a name="syntax"></a>语法

```cpp
HRESULT AddImplicitProgramNodes(
   REFGUID guidLaunchingEngine,
   GUID*   rgguidSpecificEngines,
   DWORD   celtSpecificEngines
);
```

```csharp
int AddImplicitProgramNodes(
   ref Guid guidLaunchingEngine,
   Guid[]   rgguidSpecificEngines,
   uint     celtSpecificEngines
);
```

## <a name="parameters"></a>参数
`guidLaunchingEngine`\
[在]`GUID`用于启动程序的 DE 的 DE（假定用于添加其自己的程序节点）。

`rgguidSpecificEngines`\
[在]`GUID`要为其添加程序节点的 D 数组。

`celtSpecificEngines`\
[在]数组中的`rgguidSpecificEngines` `GUID`s 数。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
- [Program Nodes](../../../extensibility/debugger/program-nodes.md)将添加在`rgguidSpecificEngines`中列出的每个 DE 的程序节点 - 不包括启动引擎（如`guidLaunchingEngine`中给出的），假定在启动程序时添加自己的程序节点。

## <a name="see-also"></a>请参阅
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
- [程序节点](../../../extensibility/debugger/program-nodes.md)
