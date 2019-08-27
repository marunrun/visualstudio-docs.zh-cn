---
title: IDebugPortEx2::GetProgram | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::GetProgram
helpviewer_keywords:
- IDebugPortEx2::GetProgram
ms.assetid: cd83a111-bfd5-4eae-b576-526466c6b6ec
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 505823a6399cc605d8784a4dba88f2fa27ad6d72
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311201"
---
# <a name="idebugportex2getprogram"></a>IDebugPortEx2::GetProgram
获取与程序节点相关联的程序。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProgram( 
   IDebugProgramNode2* pProgramNode,
   IDebugProgram2**    ppProgram
);
```

```csharp
int GetProgram( 
   IDebugProgramNode2 pProgramNode,
   out IDebugProgram2 ppProgram
);
```

## <a name="parameters"></a>参数
`pProgramNode` [in][IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象，表示程序节点。

`ppProgram` [out]返回[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示与程序节点相关联的程序。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)