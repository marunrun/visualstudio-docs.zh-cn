---
title: IDiaSymbol::get_hfaDouble | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hfaDouble method
ms.assetid: efc247b9-c16e-4fa3-89b0-901caf7b74c3
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: db12f9dfb0a5a5594c08ab0cd58446cac100f7ae
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840595"
---
# <a name="idiasymbolget_hfadouble"></a>IDiaSymbol::get_hfaDouble
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指定 (UDT) 的用户定义类型是否包含同类浮点聚合 (HFA) 数据类型为 double。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_hfaDouble(   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pRetVal`  
 弄 `TRUE` 如果 UDT 包含 double 类型的 HFA 数据，则返回; 否则返回 `FALSE` 。  
  
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
 [IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)
