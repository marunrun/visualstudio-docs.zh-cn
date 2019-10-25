---
title: IDiaFrameData::get_cplusplusExceptionHandling | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_cplusplusExceptionHandling method
ms.assetid: 54ee9cde-ce8e-45f1-809c-6fbad800d850
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d6d1e66cc7358bd086088199bf07a7320a0c8d07
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743637"
---
# <a name="idiaframedataget_cplusplusexceptionhandling"></a>IDiaFrameData::get_cplusplusExceptionHandling
检索一个标志，该标志C++指示异常处理是否有效。

## <a name="syntax"></a>语法

```C++
HRESULT get_cplusplusExceptionHandling ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果C++异常处理有效，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 若要确定结构化异常处理是否有效（与C++异常处理并不完全相同），请调用[IDiaFrameData：： get_systemExceptionHandling](../../debugger/debug-interface-access/idiaframedata-get-systemexceptionhandling.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_systemExceptionHandling](../../debugger/debug-interface-access/idiaframedata-get-systemexceptionhandling.md)