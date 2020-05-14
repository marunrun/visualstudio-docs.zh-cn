---
title: IDebugPort供应商2：：获取端口 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::GetPort
helpviewer_keywords:
- IDebugPortSupplier2::GetPort
ms.assetid: d55d5055-7386-4037-bf22-4c3e434a99ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: be3f53c12b5562377cd79267d6e216a1435859a5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724664"
---
# <a name="idebugportsupplier2getport"></a>IDebugPortSupplier2::GetPort
从端口供应商获取端口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPort( 
   REFGUID       guidPort,
   IDebugPort2** ppPort
);
```

```csharp
int GetPort( 
   ref Guid        guidPort,
   out IDebugPort2 ppPort
);
```

## <a name="parameters"></a>参数
`guidPort`\
[在]端口的全局唯一标识符 （GUID）。

`ppPort`\
[出]返回表示端口的[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 如果`E_PORTSUPPLIER_NO_PORT`给定标识符不存在端口，则返回。

## <a name="see-also"></a>请参阅
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
