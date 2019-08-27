---
title: IDiaAddressMap::set_addressMap | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_addressMap method
ms.assetid: 81e82073-089b-43d5-af39-49d7a4907c7a
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 693ecf6e8fd4f0b55936bde371b7baa6975b8f2c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198650"
---
# <a name="idiaaddressmapsetaddressmap"></a>IDiaAddressMap::set_addressMap
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

提供映射的地址以支持图像布局翻译。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT set_addressMap (   
   DWORD                     cbData,  
   struct DiaAddressMapEntry data[],  
   BOOL                      imagetoSymbols  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `cbData`  
 [in]中的元素数`data`参数。  
  
 `data[]`  
 [in]一个数组[DiaAddressMapEntry 结构](../../debugger/debug-interface-access/diaaddressmapentry.md)用于定义转换映射的结构。  
  
 `imagetoSymbols`  
 [in]`TRUE`如果`data`参数定义新的图像布局从映射到原始布局 （如所述的调试符号）。 `FALSE` 如果`data`是映射到来自原始布局的新图像布局。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 通常情况下，DIA 从程序数据库 (.pdb) 文件检索地址转换映射。 如果这些值缺失， [idiaaddressmap:: Set_imageheaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)方法调用两次，一次用于`imagetoSymbols`参数设置为`TRUE`和一次与`imagetoSymbols`参数设置为`FALSE`。 不能使用启用了地址映射转换[idiaaddressmap:: Put_addressmapenabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)方法除非提供了两个转换映射。  
  
## <a name="see-also"></a>请参阅  
 [DiaAddressMapEntry 结构](../../debugger/debug-interface-access/diaaddressmapentry.md)   
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)   
 [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)
