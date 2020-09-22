---
title: IDiaSymbol::get_addressSection | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_addressSection method
ms.assetid: fe80d479-3bb5-4f55-9b62-1bd58d0a60ce
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 85e6ffac13f25e79f51af13ac134cf538e6af5af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840359"
---
# <a name="idiasymbolget_addresssection"></a>IDiaSymbol::get_addressSection
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索地址位置部分。 当 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md) 设置为时使用 `LocIsStatic` 。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_addressSection (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pRetVal`  
 弄返回地址位置部分。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值意味着该 `S_FALSE` 属性对符号不可用。  
  
## <a name="remarks"></a>备注  
 对于位于外部 DLL 中的静态成员，此方法返回的部分可能为0，因为此方法依赖于获取成员的虚拟地址。 仅当使用指定 DLL 的加载地址的非零参数调用了[IDiaSession](../../debugger/debug-interface-access/idiasession.md)接口中的[IDiaSession：:p ut_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)方法时，虚拟地址才有效。  
  
 若要获取地址的偏移量部分，请调用 [IDiaSymbol：： get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md) 方法。  
  
## <a name="requirements"></a>要求  
  
|要求|说明|  
|-----------------|-----------------|  
|标头：|dia2|  
|版本：|DIA SDK v7.0|  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
