---
title: IDiaEnumFrameData::frameByVA | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::frameByVA method
ms.assetid: 0b1e441b-710a-46d8-8060-bed39071c834
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d0560965858bd6d9ee823a6056332bdd9a7b654a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68146506"
---
# <a name="idiaenumframedataframebyva"></a>IDiaEnumFrameData::frameByVA
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

按虚拟地址 (VA) 返回一个帧。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT frameByVA(   
   ULONGLONG       virtualAddress,  
   IDiaFrameData** frame  
);  
```  
  
#### <a name="parameters"></a>参数  
 virtualAddress  
 [in]弗吉尼亚州的感兴趣的帧。  
  
 框架  
 [out]返回[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象，表示包含提供的地址的帧。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果任何帧数据与指定的地址相不匹配。 否则，返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)   
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
