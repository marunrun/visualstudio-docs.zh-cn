---
title: IDiaSectionContrib::get_remove | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_remove method
ms.assetid: fd30ab7b-022b-4402-a42a-2d38e274c1b1
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 603602fd6606721ea9ec198c17741f4dc7d79646
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151839"
---
# <a name="idiasectioncontribget_remove"></a>IDiaSectionContrib::get_remove
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指示是否在部分成为内存中映像的一部分之前删除该部分。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_remove (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄 `TRUE` 如果该节未添加到内存中的映像，则返回; 否则返回 `FALSE` 。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
