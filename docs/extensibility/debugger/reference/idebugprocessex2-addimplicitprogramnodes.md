---
title: IDebugProcessEx2：： AddImplicitProgramNodes |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723394"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
此方法为 (DE) 指定的每个调试引擎添加一个程序节点。

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
中 `GUID` 用于启动 (的程序的 DE 的，假定将其自己的程序节点添加) 。

`rgguidSpecificEngines`\
中要 `GUID` 为其添加程序节点的 DEs 的数组。

`celtSpecificEngines`\
中数组中的的数目 `GUID` `rgguidSpecificEngines` 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
- 将为中列出的每个 DE 添加[程序节点](../../../extensibility/debugger/program-nodes.md) `rgguidSpecificEngines` （不包括启动引擎 (在) 中指定） `guidLaunchingEngine` ，这在启动程序时假定添加自己的程序节点。

## <a name="see-also"></a>另请参阅
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
- [程序节点](../../../extensibility/debugger/program-nodes.md)
