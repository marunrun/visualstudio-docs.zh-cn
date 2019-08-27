---
title: IDiaTable::get_name | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::get_name method
ms.assetid: f6e9cd07-63cd-48a6-9835-e69c2d0859c5
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d4865bff057165405cac89f169348576f8b4c0fc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68145720"
---
# <a name="idiatablegetname"></a>IDiaTable::get_name
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索表的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_name (   
   BSTR* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pRetVal`  
 [out]返回的表的名称。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
