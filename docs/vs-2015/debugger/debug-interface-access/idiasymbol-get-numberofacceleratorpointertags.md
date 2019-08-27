---
title: IDiaSymbol::get_numberOfAcceleratorPointerTags | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: 1886e3ec-b227-4187-8d93-c5144b4b77ae
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b25cd941b8f06909ca1bf777d0e3251c78732706
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "68183186"
---
# <a name="idiasymbolgetnumberofacceleratorpointertags"></a>IDiaSymbol::get_numberOfAcceleratorPointerTags
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

返回 accelerator 指针中的标记数C++AMP 存根 （stub） 函数。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_numberOfAcceleratorPointerTags(   
   DWORD* count);  
```  
  
#### <a name="parameters"></a>参数  
 `count`  
 [out]一个指向`DWORD`，它持有的加速器数量中的指针标记C++AMP 存根 （stub） 函数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
## <a name="remarks"></a>备注  
 在调用此方法`IDiaSymbol`接口对应于C++AMP 快捷键存根 （stub） 函数。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
