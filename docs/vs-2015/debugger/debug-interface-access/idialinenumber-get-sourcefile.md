---
title: IDiaLineNumber::get_sourceFile | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_sourceFile method
ms.assetid: 86fc4411-375e-4b99-8f96-4da2c3f68190
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 32cbf0fb37eedb29c1498224aff28140d2e09d0d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150628"
---
# <a name="idialinenumberget_sourcefile"></a>IDiaLineNumber::get_sourceFile
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索对源文件的引用。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_sourceFile (   
   IDiaSourceFile** pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄返回一个 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) 对象，该对象表示源文件。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)   
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
