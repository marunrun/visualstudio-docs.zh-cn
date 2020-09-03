---
title: IDebugPort2：： GetPortRequest |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2::GetPortRequest
helpviewer_keywords:
- IDebugPort2::GetPortRequest
ms.assetid: 14abf847-0675-4fa8-872e-971e00c84224
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d48d39ea10e8425d5449444514489ac4b73c0a3f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80725333"
---
# <a name="idebugport2getportrequest"></a>IDebugPort2::GetPortRequest
获取以前用于创建端口 (（如果可用）) 的端口的说明。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPortRequest( 
   IDebugPortRequest2** ppRequest
);
```

```csharp
int GetPortRequest( 
   out IDebugPortRequest2 ppRequest
);
```

## <a name="parameters"></a>参数
`ppRequest`\
弄返回一个 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) 对象，该对象表示用于创建端口的请求。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。  `E_PORT_NO_REQUEST`如果未使用[IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)端口请求创建端口，则返回。

## <a name="see-also"></a>另请参阅
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
