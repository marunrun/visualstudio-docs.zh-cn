---
title: IDiaEnumLineNumbers::get_Count | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::get_Count method
ms.assetid: dbb55936-b754-4a27-8b82-9537a7adb664
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: aaa39e806e8482ac989c643470261403647212d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62431662"
---
# <a name="idiaenumlinenumbersget_count"></a>IDiaEnumLineNumbers::get_Count
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索行号的数目。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_Count (   
   LONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 pRetVal  
 弄返回行号的数目。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)   
 [IDiaEnumLineNumbers::Item](../../debugger/debug-interface-access/idiaenumlinenumbers-item.md)
