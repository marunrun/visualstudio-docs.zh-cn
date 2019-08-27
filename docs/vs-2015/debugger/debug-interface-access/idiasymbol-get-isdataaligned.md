---
title: 'Idiasymbol:: Get_isdataaligned |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isDataAligned method
ms.assetid: ddd11a41-6c00-4829-acf4-aa1ace8c21a7
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 86c701765f9c8a67f7b95368d02febc1d254c696
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64810726"
---
# <a name="idiasymbolgetisdataaligned"></a>IDiaSymbol::get_isDataAligned
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，指定是否已为某些特定的内存边界对齐用户定义类型 (UDT)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_isDataAligned(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pFlag`  
 [out]返回`TRUE`UDT 符合某些内存边界; 否则，返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="remarks"></a>备注  
 使用非默认数据对齐方式编译可执行文件时，通常设置此属性。 例如，Microsoft c + + 编译器可以更改使用命令行选项时，数据对齐 /Zp<em>#</em>，其中 *#* 是一个字节值。  
  
## <a name="requirements"></a>要求  
  
|需求|描述|  
|-----------------|-----------------|  
|标头：|dia2.h|  
|版本：|DIA SDK v8.0|  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
