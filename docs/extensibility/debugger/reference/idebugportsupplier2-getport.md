---
title: IDebugPortSupplier2::GetPort | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::GetPort
helpviewer_keywords:
- IDebugPortSupplier2::GetPort
ms.assetid: d55d5055-7386-4037-bf22-4c3e434a99ca
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3b27c810ec6cb71cacb54e39ad97a95b53480232
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66340150"
---
# <a name="idebugportsupplier2getport"></a>IDebugPortSupplier2::GetPort
获取一个端口从端口提供程序。

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
[in]该端口的全局唯一标识符 (GUID)。

`ppPort`\
[out]返回[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)对象表示的端口。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 返回`E_PORTSUPPLIER_NO_PORT`如果任何端口不存在具有给定的标识符。

## <a name="see-also"></a>请参阅
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)