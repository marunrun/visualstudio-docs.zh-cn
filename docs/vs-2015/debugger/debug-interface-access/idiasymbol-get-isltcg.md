---
title: IDiaSymbol::get_isLTCG | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isLTCG method
ms.assetid: 5f7f05b8-6b71-4958-9e1e-e4924ef9c59b
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d355a05ba2d805349a84a842a00b699d6c1ef272
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "65696286"
---
# <a name="idiasymbolgetisltcg"></a>IDiaSymbol::get_isLTCG
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，指定是否[编译单位](../../debugger/debug-interface-access/compiland.md)已链接使用链接器开关[/LTCG （链接时间代码生成）](https://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2)，这样有助于全程序优化。 此开关仅适用于托管代码。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_iSLTCG(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>参数  
 pFlag  
 [out]返回`TRUE`如果`compiland`已与 /LTCG 链接器开关进行链接; 否则，返回`FALSE`。  
  
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
