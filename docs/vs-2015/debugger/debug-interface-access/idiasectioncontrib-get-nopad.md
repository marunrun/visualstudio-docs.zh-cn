---
title: IDiaSectionContrib::get_nopad | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_nopad method
ms.assetid: f5c08603-0b3e-4e81-acf1-1b95a6a83bed
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3044deb31214aae9c37ef7bb1f84324857ffb7d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151891"
---
# <a name="idiasectioncontribget_nopad"></a>IDiaSectionContrib::get_nopad
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指示是否不应将节填充到下一个内存边界。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_nopad(  
   BOOL* pRetVal  
};  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄 `TRUE` 如果不应将节填充到下一个内存边界，则返回; 否则返回 `FALSE` 。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此属性通常仅在旧文件上出现。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
