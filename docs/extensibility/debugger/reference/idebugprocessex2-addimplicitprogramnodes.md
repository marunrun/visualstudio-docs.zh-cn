---
title: IDebugProcessEx2::AddImplicitProgramNodes | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b75ef50107b44de8de6f65c5c4c9c6827e13426e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309492"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
此方法将添加指定每种调试引擎 (DE) 的程序节点。

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
[in]`GUID`的 DE 是要用来启动程序 （并且假定添加其自身程序节点）。

`rgguidSpecificEngines`\
[in]数组`GUID`的 DEs 将节点添加的程序。

`celtSpecificEngines`\
[in]数`GUID`中的 s`rgguidSpecificEngines`数组。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
- [程序节点](../../../extensibility/debugger/program-nodes.md)中列出的每个 DE 将添加`rgguidSpecificEngines`— 不包括启动引擎 (中给出`guidLaunchingEngine`)，这假定它启动程序时添加其自己的程序节点。

## <a name="see-also"></a>请参阅
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
- [程序节点](../../../extensibility/debugger/program-nodes.md)