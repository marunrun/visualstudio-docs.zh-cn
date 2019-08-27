---
title: 'Idiasymbol:: Get_types |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_types method
ms.assetid: 5f056e0c-e15b-4e00-8f78-aadc8574f7ea
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 813dcd692669d823548e52ce6bb7eccc9546de61
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64832255"
---
# <a name="idiasymbolgettypes"></a>IDiaSymbol::get_types
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索此符号的特定于编译器的类型的数组。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_types (   
   DWORD       cTypes,  
   DWORD*      pcTypes,  
   IDiaSymbol* types[]  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cTypes`  
 [in]若要保存的数据缓冲区的大小。  
  
 `pcTypes`  
 [out]返回的类型编写的或者，如果`types`参数是`NULL`，然后可用类型的总数。  
  
 `types[]`  
 [out]数组，它是在用来填充[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)表示此符号的所有类型的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
