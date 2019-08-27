---
title: IDiaSymbol::get_libraryName | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_libraryName method
ms.assetid: d04ddd9a-812d-46e4-bd39-28bdf3edfb70
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cdab8fdff421da751f3813789a6dee8b5b640771
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64810807"
---
# <a name="idiasymbolgetlibraryname"></a>IDiaSymbol::get_libraryName
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索加载该对象的库或对象文件的文件名称。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_libraryName (   
   BSTR* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回从中加载该对象的库或对象文件的文件名。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
