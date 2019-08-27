---
title: 'Idiasymbol:: Get_intro |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_intro method
ms.assetid: 101afe4a-4c57-45de-87b4-330394c6de10
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: df8930d620f6199ecde4d6d921d5b969204f92e6
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64830315"
---
# <a name="idiasymbolgetintro"></a>IDiaSymbol::get_intro
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索用于指定函数是否是引入的虚拟函数的标志。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_intro (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回`TRUE`如果函数为简介虚拟; 否则，返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="example"></a>示例  
  
```cpp#  
class A {  
   virtual int f1();  
}  
class B : public A {  
   int f1();  
}  
```  
  
 这两`A::f1`并`B::f1`是虚拟函数，但`A::f1`是虚拟的简介。  
  
## <a name="requirements"></a>要求  
  
|需求|描述|  
|-----------------|-----------------|  
|标头：|dia2.h|  
|版本：|DIA SDK v7.0|  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
