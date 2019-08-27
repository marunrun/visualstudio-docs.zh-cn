---
title: IDebugPortNotify2::AddProgramNode | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortNotify2::AddProgramNode
helpviewer_keywords:
- IDebugPortNotify2::AddProgramNode
ms.assetid: 34c0e949-1eb9-4108-9cb8-a3eb87fcf190
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f0afd0b2ae50555e29a75159edb8f52635730a56
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319469"
---
# <a name="idebugportnotify2addprogramnode"></a>IDebugPortNotify2::AddProgramNode
可调试的程序注册到的端口运行。

## <a name="syntax"></a>语法

```cpp
HRESULT AddProgramNode( 
   IDebugProgramNode2* pProgramNode
);
```

```csharp
int AddProgramNode( 
   IDebugProgramNode2 pProgramNode
);
```

## <a name="parameters"></a>参数
`pProgramNode`\
[in][IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象，表示要注册的程序。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 程序节点可以注销从端口通过调用[RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)