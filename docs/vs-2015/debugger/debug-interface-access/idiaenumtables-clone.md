---
title: IDiaEnumTables::Clone | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Clone method
ms.assetid: beb21109-b12c-44d8-8c1f-a332216b3713
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: feb4fdbdfe734263fee97fd0e71dfe0c132f26d6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194842"
---
# <a name="idiaenumtablesclone"></a>IDiaEnumTables::Clone
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建一个包含当前枚举数形式的相同枚举状态的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Clone (   
   IDiaEnumTables** ppenum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppenum`  
 [out]返回[IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)对象，其中包含重复的枚举器。 未复制表，仅枚举器。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
