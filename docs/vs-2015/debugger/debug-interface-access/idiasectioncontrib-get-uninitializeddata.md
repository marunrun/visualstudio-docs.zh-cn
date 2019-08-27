---
title: IDiaSectionContrib::get_uninitializedData | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_uninitializedData method
ms.assetid: 39736f35-6c73-4f54-a092-517192e417ff
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2ee0f9dd959d22d064ef2a1f86bae7789179ed3c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68151852"
---
# <a name="idiasectioncontribgetuninitializeddata"></a>IDiaSectionContrib::get_uninitializedData
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，指示的部分是否包含未初始化的数据。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_uninitializedData (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回`TRUE`的部分包含未初始化的数据; 否则，返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
