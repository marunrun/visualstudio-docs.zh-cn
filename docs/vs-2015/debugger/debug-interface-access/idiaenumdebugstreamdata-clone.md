---
title: 'Idiaenumdebugstreamdata:: Clone |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Clone method
ms.assetid: e7f17750-0694-4634-bf34-c821cd265c2f
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0c97018adad246674c672fc1b081944f05e5913c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198569"
---
# <a name="idiaenumdebugstreamdataclone"></a>IDiaEnumDebugStreamData::Clone
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建一个包含当前枚举数相同的枚举的序列的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Clone (   
   IDiaEnumDebugStreamData** ppenum  
);  
```  
  
#### <a name="parameters"></a>参数  
 ppenum  
 [out]返回[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)包含调试数据流记录的重复的序列的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
