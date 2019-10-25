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
ms.openlocfilehash: fe8155d14b3a568b8c59ec7c013c4260118ebaf2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744624"
---
# <a name="idiaenumframedataget__newenum"></a>IDiaEnumFrameData::get__NewEnum
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
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)