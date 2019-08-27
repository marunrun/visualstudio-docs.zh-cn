---
title: IDiaEnumTables::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::get__NewEnum method
ms.assetid: 7b1159c7-a5f0-4baa-861a-dc11437d8b93
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c47b552d2d9246fcf7f0982a84d8c301238cf65d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832682"
---
# <a name="idiaenumtablesgetnewenum"></a>IDiaEnumTables::get__NewEnum
检索<xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT>此枚举器的版本。

## <a name="syntax"></a>语法

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`IUnknown`接口，表示<xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT>此枚举器的版本。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)