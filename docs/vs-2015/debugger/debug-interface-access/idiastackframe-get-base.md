---
title: IDiaStackFrame::get_base | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_base method
ms.assetid: f27477d7-26fe-4c1c-a08a-c52cb20c8293
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3ad1647c31dba9b313d67a55d9435bcd5843a5a2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190607"
---
# <a name="idiastackframegetbase"></a>IDiaStackFrame::get_base
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索在帧的基址。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_base (   
   ULONGLONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回的基址。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果不支持的属性。 否则，返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
