---
title: IDiaSession::findSymbolByAddr | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByAddr method
ms.assetid: c130abc5-4d0a-4d2d-8286-94fde36ddd4a
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 40cddc1c4088ca51791a6778a436e2f1161444ba
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68165508"
---
# <a name="idiasessionfindsymbolbyaddr"></a>IDiaSession::findSymbolByAddr
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索指定地址中包含或最近的指定符号类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT findSymbolByAddr (   
   DWORD        isect,  
   DWORD        offset,  
   SymTagEnum   symtag,  
   IDiaSymbol** ppSymbol  
);  
```  
  
#### <a name="parameters"></a>参数  
 `isect`  
 中指定地址的部分组件。  
  
 `offset`  
 中指定地址的偏移量部分。  
  
 `symtag`  
 中要查找的符号类型。 值取自 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md) 枚举。  
  
 `ppSymbol`  
 弄返回一个 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象，该对象表示检索到的符号。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="example"></a>示例  
  
```cpp#  
IDiaSymbol* pFunc;  
pSession->findSymbolByAddr( isect, offset, SymTagFunction, &pFunc );  
```  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
