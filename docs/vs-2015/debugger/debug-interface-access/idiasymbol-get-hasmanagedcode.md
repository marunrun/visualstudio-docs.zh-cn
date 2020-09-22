---
title: IDiaSymbol::get_hasManagedCode | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasManagedCode method
ms.assetid: e40f82f5-88fe-4a9b-b594-3605f42773ec
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 49e78c062ba92bf93edfce9aa7dac215a96faeb1
ms.sourcegitcommit: fb8babf5cd72f1fc2f97ffe4ad7b62d91f325f61
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2020
ms.locfileid: "90840565"
---
# <a name="idiasymbolget_hasmanagedcode"></a>IDiaSymbol::get_hasManagedCode
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指示该模块是否包含托管代码。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_hasManagedCode(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pFlag`  
 弄 `TRUE` 如果模块包含托管代码，则返回; 否则返回 `FALSE` ，则代码为非托管代码。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值意味着该 `S_FALSE` 属性对符号不可用。  
  
## <a name="remarks"></a>备注  
 此属性可从 " `SymTagCompilandDetails` 符号类型" (参阅 [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)) 。  
  
## <a name="requirements"></a>要求  
  
|要求|说明|  
|-----------------|-----------------|  
|标头：|dia2|  
|版本：|DIA SDK v8.0|  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)
