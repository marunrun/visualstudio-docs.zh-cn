---
title: IDiaEnumFrameData::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::get__NewEnum method
ms.assetid: f5fe0279-0549-4af5-8f89-bcb535fc5809
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bc6e5d42d2a9f360b3899b2922bda879d4293d4d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838371"
---
# <a name="idiaenumframedatagetnewenum"></a>IDiaEnumFrameData::get__NewEnum
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
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)