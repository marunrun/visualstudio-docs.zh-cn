---
title: IDiaSymbol::getSrcLineOnTypeDefn | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: ad554d18-9988-4b64-ad71-e7594c266e94
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a3a70cec3ab9e03dd97a1df5f0ccf8713a79cc28
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "68180474"
---
# <a name="idiasymbolgetsrclineontypedefn"></a>IDiaSymbol::getSrcLineOnTypeDefn
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索表示指定的用户定义类型定义位置的源代码文件和行号。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT getSrcLineOnTypeDefn(  
   IDiaLineNumber **ppResult);  
```  
  
#### <a name="parameters"></a>参数  
 `ppResult`  
 [out]一个`IDiaLineNumber`对象，其中包含源文件和行号的用户定义。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
