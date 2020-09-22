---
title: IDiaSymbol：： get_packed |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_packed method
ms.assetid: e42ff368-56c4-49a2-8676-f80e349efa21
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 90351c3319f8354685ae0d907379b8446f76cb7f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840711"
---
# <a name="idiasymbolget_packed"></a>IDiaSymbol::get_packed
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指定是否打包 (UDT) 的用户定义数据类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_packed (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pRetVal`  
 弄 `TRUE` 如果 UDT 已打包，则返回; 否则返回 `FALSE` 。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值意味着该 `S_FALSE` 属性对符号不可用。  
  
## <a name="remarks"></a>备注  
 "打包" 表示 UDT 的所有成员尽可能靠近，无干预填充以与内存边界对齐。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
