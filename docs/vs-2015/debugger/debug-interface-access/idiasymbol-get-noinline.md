---
title: 'Idiasymbol:: Get_noinline |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_noInline method
ms.assetid: 5c610b78-f1a3-494a-acf8-c42b97935be1
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e6ee1e21b46e1906b4872e9598e75ac283b013ac
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "65698460"
---
# <a name="idiasymbolgetnoinline"></a>IDiaSymbol::get_noInline
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，指定是否已标记为不被内联函数 (使用[noinline](https://msdn.microsoft.com/library/f259d55b-dec7-4bde-8cf9-14521e4fdc42)属性)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_noInline(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pFlag`  
 [out]返回`TRUE`如果函数具有`noinline`属性; 否则，返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="requirements"></a>要求  
  
|需求|描述|  
|-----------------|-----------------|  
|标头：|dia2.h|  
|版本：|DIA SDK v8.0|  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [noinline](https://msdn.microsoft.com/library/f259d55b-dec7-4bde-8cf9-14521e4fdc42)
