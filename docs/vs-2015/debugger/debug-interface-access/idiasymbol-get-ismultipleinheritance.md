---
title: IDiaSymbol::get_isMultipleInheritance |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: 0aa356a1-5c5c-4ee4-8b48-bae0a2610013
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a0505703c7fb109182e261910760516e4e9225b0
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "68163968"
---
# <a name="idiasymbolgetismultipleinheritance"></a>IDiaSymbol::get_isMultipleInheritance
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定是否`this`指针指向一个具有多个继承数据成员。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_isMultipleInheritance(   
   BOOL* pRetVal);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pRetVal`  
 [out]一个指向`BOOL`，它指定是否`this`指针指向一个具有多个继承数据成员。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
