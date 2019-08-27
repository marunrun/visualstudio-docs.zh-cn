---
title: IDebugEngine2::RemoveAllSetExceptions | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::RemoveAllSetExceptions
helpviewer_keywords:
- IDebugEngine2::RemoveAllSetExceptions
ms.assetid: 165fbe89-802d-4d99-85ca-c10fd6cccc09
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 17063a2c503535bc20b61ba8d9914fc54005cccc
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352614"
---
# <a name="idebugengine2removeallsetexceptions"></a>IDebugEngine2::RemoveAllSetExceptions
删除的异常 IDE 已设置为特定的运行时体系结构或语言的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT RemoveAllSetExceptions( 
   REFGUID guidType
);
```

```csharp
int RemoveAllSetExceptions( 
   ref Guid guidType
);
```

## <a name="parameters"></a>参数
`guidType`\
[in]语言 GUID 或特定于运行时体系结构的调试引擎的 GUID。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 通过此方法移除异常设置的早期调用[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)方法。

 若要删除的特定异常，请调用[RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)