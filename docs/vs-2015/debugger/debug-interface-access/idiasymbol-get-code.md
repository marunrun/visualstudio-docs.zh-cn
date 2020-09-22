---
title: IDiaSymbol::get_code | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_code method
ms.assetid: 5f425fa3-7ba6-4979-8b3e-0fcd06cbba73
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 13fe5511c5bb95e32ec2ded10420073a9818e11f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840695"
---
# <a name="idiasymbolget_code"></a>IDiaSymbol::get_code
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指定符号是否引用代码地址。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_code (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pRetVal`  
 弄 `TRUE` 如果符号引用代码地址，则返回，否则返回 `FALSE` 。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 或错误代码。  
  
> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。  
  
## <a name="requirements"></a>要求  
  
|要求|说明|  
|-----------------|-----------------|  
|标头：|dia2|  
|版本：|DIA SDK v7.0|  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
