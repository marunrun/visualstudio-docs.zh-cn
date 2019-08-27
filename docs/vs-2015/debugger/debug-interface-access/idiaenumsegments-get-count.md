---
title: IDiaEnumSegments::get_Count | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::get_Count method
ms.assetid: c62a0fda-17b8-4cf6-b321-6014ce581096
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 445049452a91351ffff0cc18daa328777ed89dc9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189922"
---
# <a name="idiaenumsegmentsgetcount"></a>IDiaEnumSegments::get_Count
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索的段数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_Count (   
   LONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 pRetVal  
 [out，retval]返回的段数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)   
 [IDiaEnumSegments::Item](../../debugger/debug-interface-access/idiaenumsegments-item.md)
