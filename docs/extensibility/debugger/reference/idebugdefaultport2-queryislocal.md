---
title: IDebug默认端口2：：查询本地 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::QueryIsLocal
helpviewer_keywords:
- IDebugDefaultPort2::QueryIsLocal
ms.assetid: 1a42e774-c6ed-419a-a0e3-cab5778652ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c06230f7bbd1825fe73a22f9b1fdc35aea35c499
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732325"
---
# <a name="idebugdefaultport2queryislocal"></a>IDebugDefaultPort2::QueryIsLocal
此方法确定此端口是否位于本地计算机上。

## <a name="syntax"></a>语法

```cpp
HRESULT QueryIsLocal(
   void
);
```

```csharp
int QueryIsLocal();
```

## <a name="return-value"></a>返回值
 如果`S_OK`此端口是本地的（与调用方在同一台计算机上），或者`S_FALSE`该端口位于另一台计算机上，则返回。

## <a name="see-also"></a>请参阅
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
