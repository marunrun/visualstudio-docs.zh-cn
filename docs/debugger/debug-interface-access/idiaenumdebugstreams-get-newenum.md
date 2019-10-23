---
title: IDiaEnumDebugStreams::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::get__NewEnum method
ms.assetid: 972372ff-abfc-4987-a302-7788fab90348
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd6497464e5ec3251bd32fe96cfe65621ded5359
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744752"
---
# <a name="idiaenumdebugstreamsget__newenum"></a>IDiaEnumDebugStreams::get__NewEnum
检索此枚举器的 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> 版本。

## <a name="syntax"></a>语法

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

弄返回表示此枚举器的 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> 版本的 `IUnknown` 接口。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)