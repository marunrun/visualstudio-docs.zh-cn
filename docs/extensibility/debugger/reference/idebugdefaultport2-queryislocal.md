---
title: IDebugDefaultPort2::QueryIsLocal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::QueryIsLocal
helpviewer_keywords:
- IDebugDefaultPort2::QueryIsLocal
ms.assetid: 1a42e774-c6ed-419a-a0e3-cab5778652ca
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 42a21419af9be56647a835ee1d8ddab62e20f842
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351752"
---
# <a name="idebugdefaultport2queryislocal"></a>IDebugDefaultPort2::QueryIsLocal
此方法确定此端口是否在本地计算机上。

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
 返回`S_OK`此端口是在本地 （在调用方所在的计算机） 或`S_FALSE`如果端口是在另一台计算机上。

## <a name="see-also"></a>请参阅
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)