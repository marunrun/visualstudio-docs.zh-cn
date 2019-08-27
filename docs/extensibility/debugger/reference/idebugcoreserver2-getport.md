---
title: IDebugCoreServer2::GetPort | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetPort
helpviewer_keywords:
- IDebugCoreServer2::GetPort
ms.assetid: 3f5ea4a8-6085-4600-980a-9e48f8b5be56
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59f4507f631887f8ffda37abec8b597087a0e57f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317798"
---
# <a name="idebugcoreserver2getport"></a>IDebugCoreServer2::GetPort
检索特定端口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPort( 
   REFGUID       guidPort,
   IDebugPort2** ppPort
);
```

```csharp
int GetPort( 
   ref Guid        guidPort,
   out IDebugPort2 ppPort
);
```

## <a name="parameters"></a>参数
`guidPort`\
[in]要检索的端口的 GUID。

`ppPort`\
[out]返回[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)对象，表示所需的端口。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 返回`E_PORTSUPPLIER_NO_PORT`是否存在具有给定标识符的任何端口。

## <a name="see-also"></a>请参阅
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)