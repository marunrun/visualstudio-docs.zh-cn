---
title: IDiaSymbol::get_hasEHa | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasEHa method
ms.assetid: cb61dfd9-fe69-461c-8185-288440454864
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 87adaa2e43068784e5ec6488030f147891a027dd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840649"
---
# <a name="idiasymbolget_haseha"></a>IDiaSymbol::get_hasEHa
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指定该函数是否包含异步 (结构化) 异常处理。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_hasEHa(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pFlag`  
 弄 `TRUE` 如果函数具有任何异步异常处理，则返回; 否则返回 `FALSE` 。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值意味着该 `S_FALSE` 属性对符号不可用。  
  
## <a name="remarks"></a>备注  
 可以使用 c + + 样式的异常处理混合使用异步或结构化异常处理，但需要使用特定的编译器开关/EHa 来启用它。  
  
## <a name="requirements"></a>要求  
  
|要求|说明|  
|-----------------|-----------------|  
|标头：|dia2|  
|版本：|DIA SDK v8.0|  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
