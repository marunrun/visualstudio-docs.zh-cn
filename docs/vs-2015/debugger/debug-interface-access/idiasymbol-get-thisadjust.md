---
title: IDiaSymbol：： get_thisAdjust |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_thisAdjust method
ms.assetid: 56b9a147-e8c0-4d4b-a42a-398214dd5f86
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 979f79658834f9bdcf50f0af51597515eaab2991
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840616"
---
# <a name="idiasymbolget_thisadjust"></a>IDiaSymbol::get_thisAdjust
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索方法的逻辑 `this` adjustor。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_thisAdjust (   
   LONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pRetVal`  
 弄返回方法的逻辑 `this` adjustor。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。  
  
## <a name="remarks"></a>备注  
 在某些多重继承情况下，方法本身必须 `this` 通过将偏移量添加到来计算 true 值 `this` 。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
