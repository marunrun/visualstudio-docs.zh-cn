---
title: IDiaLineNumber::get_columnNumber | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_columnNumber method
ms.assetid: e317f29a-6525-46a7-8421-33985392f8fd
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 51763dea01039ce084804bfa007fd8f0577cb9e2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192380"
---
# <a name="idialinenumberget_columnnumber"></a>IDiaLineNumber::get_columnNumber
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索表达式或语句开始的列号。  
  
## <a name="syntax"></a>语法  
  
```  
[C++]  
HRESULT get_columnNumber (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄返回表达式或语句开始的列号。 如果值为零，则不存在列信息。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法返回的列值是行中语句的第一个字符到行中的字节偏移量。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
