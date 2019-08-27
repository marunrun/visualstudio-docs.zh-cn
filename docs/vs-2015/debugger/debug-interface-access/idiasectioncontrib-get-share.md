---
title: IDiaSectionContrib::get_share | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_share method
ms.assetid: 05c4c896-4419-4166-8bb2-8d0934dc14b5
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ce9e75e16aaed3b2d7386f977894bde3c17029f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150530"
---
# <a name="idiasectioncontribgetshare"></a>IDiaSectionContrib::get_share
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，指示是否可以在内存中共享部分。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_share (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pRetVal`  
 [out]返回`TRUE`的部分是可共享在内存中; 否则，返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
