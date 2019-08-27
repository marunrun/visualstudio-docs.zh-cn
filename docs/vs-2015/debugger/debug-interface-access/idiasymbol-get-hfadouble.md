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
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64810633"
---
# <a name="idiasymbolgethfadouble"></a>IDiaSymbol::get_hfaDouble
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索指定用户定义类型 (UDT) 是否包含同构浮点聚合 (HFA) 数据类型为 double 的标志。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_hfaDouble(   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回`TRUE`UDT 包含 HFA 数据类型的双精度; 否则为如果返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="remarks"></a>备注  
  
## <a name="requirements"></a>要求  
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia100.dll  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)
