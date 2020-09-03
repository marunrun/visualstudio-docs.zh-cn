---
title: IDiaLineNumber::get_compilandId | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_compilandId method
ms.assetid: 2cd6f551-8091-47c7-803f-3f79a766a211
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1210276728e40e43f8ae40eef78de4d53cf6262d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152075"
---
# <a name="idialinenumberget_compilandid"></a>IDiaLineNumber::get_compilandId
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索提供此行的编译单位的唯一标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_compilandId (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄返回 `DWORD` ，它包含提供此行的编译单位的唯一标识符。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
