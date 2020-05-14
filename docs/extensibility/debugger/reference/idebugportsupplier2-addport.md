---
title: IDebugPort供应商2：：添加端口 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::AddPort
helpviewer_keywords:
- IDebugPortSupplier2::AddPort
ms.assetid: df491161-6bf3-4fcc-b478-b9ec88ec995f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 00954ceaa0ddd750a3d08e372d1edaa1905f01c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724735"
---
# <a name="idebugportsupplier2addport"></a>IDebugPortSupplier2::AddPort
添加端口。

## <a name="syntax"></a>语法

```cpp
HRESULT AddPort( 
   IDebugPortRequest2* pRequest,
   IDebugPort2**       ppPort
);
```

```csharp
int AddPort( 
   IDebugPortRequest2 pRequest,
   out IDebugPort2    ppPort
);
```

## <a name="parameters"></a>参数
`pRequest`\
[在]描述要添加的端口的[IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)对象。

`ppPort`\
[出]返回表示端口的[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法实际上创建请求的端口，并将其添加到端口供应商的活动端口的内部列表中。 可以首先调用[CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)方法，以避免可能耗时的延迟。

## <a name="see-also"></a>请参阅
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)
