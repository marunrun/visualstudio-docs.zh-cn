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
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "68150354"
---
# <a name="idiasymbolgetunmodifiedtypeid"></a>IDiaSymbol::get_unmodifiedTypeId
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索原始 （未修改） 类型的 ID。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_unmodifiedTypeId(   
   DWORD* pRetVal);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]一个指向`DWORD`保存此 id。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
