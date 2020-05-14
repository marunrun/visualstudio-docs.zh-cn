---
title: IDebug属性3：：创建对象ID |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721172"
---
# <a name="idebugproperty3createobjectid"></a>IDebugProperty3::CreateObjectID
为此属性创建唯一 ID，以确保它在所有其他属性中是唯一的。

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
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 当会话调试管理器希望确保此属性在所有其他属性之间唯一标识时，将调用此方法。 调试引擎 （DE） 支持此方法，除非它处理的属性已被唯一标识。 如果 DE 不支持此方法，它将返回`E_NOTIMPL`。

 调用[销毁ObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)方法`CreateObjectID`时，将销毁使用的任何唯一 ID;这也标志着唯一标识此属性的需要的结束。

> [!NOTE]
> 没有检索此唯一 ID 的方法，因此当调用`CreateObjectID`该方法时，DE 可以执行所需的任何唯一 ID 操作。

## <a name="see-also"></a>请参阅
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)
