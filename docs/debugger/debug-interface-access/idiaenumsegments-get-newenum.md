---
title: IDiaEnumSegments::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::get__NewEnum method
ms.assetid: 504505fa-b35c-402f-a440-8972c589cc5b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c5c021e74c758b6409d42deae6a7e6831368367e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829805"
---
# <a name="idiaenumsegmentsgetnewenum"></a>IDiaEnumSegments::get__NewEnum
检索<xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT>此枚举器的版本。

## <a name="syntax"></a>语法

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

[out]返回`IUnknown`接口，表示<xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT>此枚举器的版本。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)