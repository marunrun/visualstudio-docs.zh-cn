---
title: IDiaSymbol::get_unmodifiedTypeId | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: 4f7fc73c-f524-4d7a-b378-a9ab99a96104
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 731c0aa1ba12572e396f512eecbcc4d5e7cd9eab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150354"
---
# <a name="idiasymbolget_unmodifiedtypeid"></a>IDiaSymbol::get_unmodifiedTypeId
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索) 类型未修改的原始 (的 ID。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_unmodifiedTypeId(   
   DWORD* pRetVal);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄指向包含 ID 的的指针 `DWORD` 。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
