---
title: IDiaSymbol：： get_intrinsic |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_intrinsic method
ms.assetid: f969f595-d9f9-48b9-adaa-63a6e4e09575
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 318a0867b256b4127e6ca16298dfed225cd27d57
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840746"
---
# <a name="idiasymbolget_intrinsic"></a>IDiaSymbol::get_intrinsic
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指定类是否为内部类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_intrinsic(   
   BOOL* pRetVal)  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pRetVal`  
 弄 `TRUE` 如果类是内部类型，则返回; 否则返回 `FALSE` 。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。  
  
## <a name="remarks"></a>备注  
  
## <a name="requirements"></a>要求  
 标头： Dia2  
  
 库： diaguids  
  
 DLL： msdia100.dll  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
