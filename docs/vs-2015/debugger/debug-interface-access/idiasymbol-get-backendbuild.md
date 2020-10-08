---
title: IDiaSymbol：： get_backEndBuild |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_backEndBuild method
ms.assetid: 423af497-9294-438e-92b4-456c6f56dc56
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1bd7a0bc75907d60a3ac3cbb8a571908631777e3
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "91838452"
---
# <a name="idiasymbolget_backendbuild"></a>IDiaSymbol::get_backEndBuild
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索编译器的后端内部版本号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_backEndBuild (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄返回后端内部版本号。 请参阅“备注”。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值意味着该 `S_FALSE` 属性对符号不可用。  
  
## <a name="remarks"></a>注解  
 编译器通常包含两个主要元素：前端 (分析器) ，它处理将源代码分析成中间窗体，并将中间窗体转换为程序集) 后端 (代码生成器。 前端的版本不同于后端，这种情况并不常见。  
  
 前端或后端版本号由三个部分组成： .. \<major> \<minor> \<build> ，其中 \<major> 是主版本号， \<minor> 是次版本号， \<build> 是内部版本号。 例如，13.10.3077。  
  
## <a name="requirements"></a>要求  
  
|要求|说明|  
|-----------------|-----------------|  
|标头：|dia2|  
|版本：|DIA SDK v7.0|  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
