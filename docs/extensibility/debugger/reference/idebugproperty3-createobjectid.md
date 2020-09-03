---
title: IDebugProperty3：： CreateObjectID |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::CreateObjectID
helpviewer_keywords:
- IDebugProperty3::CreateObjectID
ms.assetid: f2fa81e7-822f-456e-8729-a96a18eea771
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1d3993d674f029260dbe32d16c576cb239ff8d6d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80721172"
---
# <a name="idebugproperty3createobjectid"></a>IDebugProperty3::CreateObjectID
为此属性创建一个唯一的 ID，以确保它在所有其他属性中是唯一的。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateObjectID(
   void
);
```

```csharp
int CreateObjectID();
```

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 当会话调试管理器需要确保在所有其他属性中唯一标识该属性时，将调用此方法。 调试引擎 (DE) 支持此方法，除非它处理的属性已唯一标识。 如果 DE 不支持此方法，则返回 `E_NOTIMPL` 。

 在 `CreateObjectID` 调用 [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md) 方法时，将销毁用创建的任何唯一 ID; 这还会发出信号，以唯一标识此属性。

> [!NOTE]
> 没有方法可以检索此唯一 ID，因此，在调用方法时，DE 可以为唯一 Id 执行任何所需的操作 `CreateObjectID` 。

## <a name="see-also"></a>另请参阅
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)
