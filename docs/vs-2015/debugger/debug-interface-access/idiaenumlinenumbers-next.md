---
title: IDiaEnumLineNumbers：： Next |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Next method
ms.assetid: 363d5b40-1316-4ab8-836f-63637f619e0a
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ebf4016b3bff52a74607fe01918655c0587f51d9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190103"
---
# <a name="idiaenumlinenumbersnext"></a>IDiaEnumLineNumbers::Next
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索枚举序列中指定数目的行号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Next (   
   ULONG            celt,  
   IDiaLineNumber** rgelt,  
   ULONG*           pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 celt  
 中要检索的枚举器中的行号数目。  
  
 rgelt  
 弄返回 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) 对象的数组，这些对象表示所需的行号。  
  
 pceltFetched  
 弄返回提取的枚举器中的行号数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果没有更多的行号，则返回。 否则，返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)   
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)   
 [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)
