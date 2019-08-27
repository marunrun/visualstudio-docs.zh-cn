---
title: IDiaSession::findSymbolsByRVAForAcceleratorPointerTag |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: a073cc45-0c7b-417e-b5fc-a3b08beccdbc
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0711c95310d4d3613d8b82bccbecab122bf19ef8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196364"
---
# <a name="idiasessionfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSession::findSymbolsByRVAForAcceleratorPointerTag
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

提供相应的标记值，则此方法将返回在指定的父 Accelerator 存根 （stub） 函数在指定的相对虚拟地址中包含的符号的枚举。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT findSymbolsByRVAForAcceleratorPointerTag (   
   IDiaSymbol*           parent,  
   DWORD                 tagValue,  
   DWORD                 rva,  
   IDiaEnumSymbols**     ppResult  
);  
```  
  
#### <a name="parameters"></a>参数  
 `parent`  
 [in]`IDiaSymbol` ，对应于要搜索的加速器存根 （stub） 函数。  
  
 `tagValue`  
 [in]指针标记值。  
  
 `rva`  
 [in]相对虚拟地址。  
  
 `ppResult`  
 [out]一个指向`IDiaEnumSymbols`使用结果初始化的接口指针。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 调用此方法仅对`IDiaSymbol`对应于加速器存根 （stub） 函数的接口。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
