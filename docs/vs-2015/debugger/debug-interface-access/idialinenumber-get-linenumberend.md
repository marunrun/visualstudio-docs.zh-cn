---
title: IDiaLineNumber::get_lineNumberEnd | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_lineNumberEnd method
ms.assetid: b101853e-2bcf-47c1-acef-e13984c7ea9d
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 21e5213e1940726c5863f0f5cfc306ae0c16e9eb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152041"
---
# <a name="idialinenumberget_linenumberend"></a>IDiaLineNumber::get_lineNumberEnd
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索语句或表达式结束处的源行号（从1开始）。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_lineNumberEnd (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄返回语句或表达式结束处的行号。 如果值为零，则不存在最终信息。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
