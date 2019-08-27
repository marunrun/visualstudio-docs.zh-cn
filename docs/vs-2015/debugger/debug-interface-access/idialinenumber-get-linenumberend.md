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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152041"
---
# <a name="idialinenumbergetlinenumberend"></a>IDiaLineNumber::get_lineNumberEnd
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索的语句或表达式的结束位置的基于 1 的源行号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_lineNumberEnd (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回的行号的语句或表达式的结束位置。 如果值为零，然后结束信息不存在。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
