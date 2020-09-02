---
title: IDiaLoadCallback::RestrictSymbolServerAccess | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::RestrictSymbolServerAccess method
ms.assetid: db37ad9f-f75e-4f0c-83bf-21a6e66ba859
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fddf9812810e7d184859f60d98f51000b824092a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150599"
---
# <a name="idialoadcallbackrestrictsymbolserveraccess"></a>IDiaLoadCallback::RestrictSymbolServerAccess
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

确定是否允许访问符号服务器来解析符号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT RestrictSymbolServerAccess();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 除以外的任何返回代码 `S_OK` 都禁止使用符号服务器解析符号。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
