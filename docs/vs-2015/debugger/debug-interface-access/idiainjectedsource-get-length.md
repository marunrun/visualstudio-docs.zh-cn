---
title: 'Idiainjectedsource:: Get_length |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_length method
ms.assetid: 38b88b8b-c2e0-4b2d-8b8b-9ff373733e78
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7ce9a927f8e2e732bd5b74d0f58afa40a7cf8efa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192448"
---
# <a name="idiainjectedsourcegetlength"></a>IDiaInjectedSource::get_length
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索的代码的字节数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_length (   
   ULONGLONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回代码的字节数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法返回的值是对源代码的长度并与相同的值返回的[idiainjectedsource:: Get_source](../../debugger/debug-interface-access/idiainjectedsource-get-source.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)   
 [IDiaInjectedSource::get_source](../../debugger/debug-interface-access/idiainjectedsource-get-source.md)
