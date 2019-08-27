---
title: IDebugMemoryContext2::GetInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::GetInfo
helpviewer_keywords:
- GetInfo method
- IDebugMemoryContext2::GetInfo method
ms.assetid: 08c7f091-1816-4d64-8834-f9ecaac5c58d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f349ef2f923dd18feeb2a201ef59e9d3489271ab
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347051"
---
# <a name="idebugmemorycontext2getinfo"></a>IDebugMemoryContext2::GetInfo
检索[CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)结构，它描述的上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT GetInfo( 
   CONTEXT_INFO_FIELDS dwFields,
   CONTEXT_INFO*       pInfo
);
```

```csharp
int GetInfo(
   enum_CONTEXT_INFO_FIELDS dwFields,
   CONTEXT_INFO[]           pinfo
);
```

## <a name="parameters"></a>参数
`dwFields`\
[in]中的标志的组合[CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)枚举，用于指示哪些字段[CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)结构，则为填写。

`pInfo`\
[in、 out]`CONTEXT_INFO`中填充的结构。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)
- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)