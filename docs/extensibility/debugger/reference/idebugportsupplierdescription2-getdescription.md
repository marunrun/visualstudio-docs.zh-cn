---
title: IDebugPortSupplierDescription2::GetDescription | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2::GetDescription
ms.assetid: bff5f536-1cd1-4313-8856-db7b05818305
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7619421e66b8f6e68c252fd2c2885272003bb6e8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339943"
---
# <a name="idebugportsupplierdescription2getdescription"></a>IDebugPortSupplierDescription2::GetDescription
检索端口提供程序的说明和描述性元数据。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDescription(
   PORT_SUPPLIER_DESCRIPTION_FLAGS *pdwFlags,
   BSTR *pbstrText
);
```

```csharp
public int GetDescription(
   out enum_PORT_SUPPLIER_DESCRIPTION_FLAGS pdwFlags,
   out string pbstrText
);
```

## <a name="parameters"></a>参数
`pdwFlags`\
[out]说明的元数据标记。

`pbstrText`\
[out]端口提供程序的说明。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md)