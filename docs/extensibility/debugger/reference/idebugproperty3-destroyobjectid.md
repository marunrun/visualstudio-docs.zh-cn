---
title: IDebugProperty3::DestroyObjectID | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::DestroyObjectID
helpviewer_keywords:
- IDebugProperty3::DestroyObjectID
ms.assetid: bd08f356-cc67-4717-98c9-c3d00cad2040
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c117cab17340f50a1ed580d081c3291308ec0d9d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66308888"
---
# <a name="idebugproperty3destroyobjectid"></a>IDebugProperty3::DestroyObjectID
销毁，该值指示调用方不再关注来标识唯一中所有其他属性的此属性与此属性相关联的唯一 ID。

## <a name="syntax"></a>语法

```cpp
HRESULT DestroyObjectID(
   void
);
```

```csharp
int DestroyObjectID();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 如果调试引擎不需要支持的属性的唯一 Id （因为它已跟踪它们唯一内部），则可以只返回`E_NOTIMPL`为此方法。

 通过调用创建唯一 Id [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)方法时调用方想要确保此属性唯一地标识在所有其他属性之间。

## <a name="see-also"></a>请参阅
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)