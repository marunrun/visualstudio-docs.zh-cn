---
title: IDiaAddressMap::get_relativeVirtualAddressEnabled | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::get_relativeVirtualAddressEnabled method
ms.assetid: 4c48af81-7148-4d9a-818e-dbe62cbfc638
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fc04b50e718720ee13997b32cc7b102e8d96d0bf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198690"
---
# <a name="idiaaddressmapgetrelativevirtualaddressenabled"></a>IDiaAddressMap::get_relativeVirtualAddressEnabled
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指示是否启用的计算和使用的相对虚拟地址 (RVA)。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_relativeVirtualAddressEnabled (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 pRetVal  
 [out]返回`TRUE`如果启用的 Rva 计算。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果段最初加载从 PDB 文件，则启用 Rva。 可以通过调用暂时禁用使用的 Rva [idiaaddressmap:: Put_relativevirtualaddressenabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)方法。  
  
 此外，新映像标头可以通过调用来建立[idiaaddressmap:: Set_imageheaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)方法后调用`put_relativeVirtualAddressEnabled`方法可用来启用的 rva 也使用新映像标头。  
  
## <a name="see-also"></a>请参阅  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)   
 [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)
