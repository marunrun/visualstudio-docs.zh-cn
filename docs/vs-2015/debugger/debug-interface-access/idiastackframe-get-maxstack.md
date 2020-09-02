---
title: IDiaStackFrame::get_maxStack | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_maxStack method
ms.assetid: 6352e972-7105-4d0e-aeba-b8fc16d62dec
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f7e860830b5169a71d7757e1ee39b223559456de
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62575991"
---
# <a name="idiastackframeget_maxstack"></a>IDiaStackFrame::get_maxStack
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索堆栈中堆栈上推送的最大字节数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_maxStack (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄返回在堆栈上推送的最大字节数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果该属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
