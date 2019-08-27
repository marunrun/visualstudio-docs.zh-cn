---
title: IDiaFrameData::get_lengthParams | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthParams method
ms.assetid: a9177ed6-9ba8-4384-b411-24cad07d031b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 712f7ee9eaf497fc5dd176f3f254d5af73ebcf3b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829040"
---
# <a name="idiaframedatagetlengthparams"></a>IDiaFrameData::get_lengthParams
检索的参数推送到堆栈上的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthParams ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回参数的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 中的计划字符串解释通常使用此方法返回的值 (请参阅[idiaframedata:: Get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)程序字符串的定义的方法)。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)