---
title: IDiaSymbol：： get_access |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_access method
ms.assetid: 908976ae-95c4-4020-89c9-de137f727f98
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 806e9fd06611e2cb30829b294222870b9252c35b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840577"
---
# <a name="idiasymbolget_access"></a>IDiaSymbol::get_access
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索类成员的访问修饰符。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_access (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pRetVal`  
 弄从 [CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md) 枚举返回一个值，该值指定类成员的访问修饰符。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值意味着该 `S_FALSE` 属性对符号不可用。  
  
## <a name="requirements"></a>要求  
  
|要求|说明|  
|-----------------|-----------------|  
|标头：|dia2|  
|版本：|DIA SDK v7.0|  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)
