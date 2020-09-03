---
title: IDiaAddressMap：： set_imageHeaders |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_imageHeaders method
ms.assetid: a46b9d0e-43e6-433f-b2c7-aa203981e4e4
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 18fa69929f78d5ae661169a09db97697d98f4d94
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198642"
---
# <a name="idiaaddressmapset_imageheaders"></a>IDiaAddressMap::set_imageHeaders
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设置图像标头以启用相对虚拟地址转换。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT set_imageHeaders (   
   DWORD cbData,  
   BYTE  data[],  
   BOOL  originalHeaders  
);  
```  
  
#### <a name="parameters"></a>参数  
 cbData  
 中标头数据的字节数。 必须是 `n*sizeof(IMAGE_SECTION_HEADER)` `n` 可执行文件中的节标头数。  
  
 data[]  
 中  `IMAGE_SECTION_HEADER` 要用作图像标头的结构的数组。  
  
 originalHeaders  
 中如果 `FALSE` 图像标题来自新图像，则设置为; `TRUE` 如果在升级之前反映原始图像，则设置为。 通常，这只会设置为 `TRUE` 与调用 [IDiaAddressMap：： set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) 方法结合。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 `IMAGE_SECTION_HEADER`结构在 Winnt 中声明，表示可执行文件的图像节标头格式。  
  
 相对虚拟地址的计算取决于 `IMAGE_SECTION_HEADER` 值。 通常，DIA 从程序数据库 () 文件中检索这些文件。 如果缺少这些值，DIA 将无法计算相对虚拟地址， [IDiaAddressMap：： get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md) 方法返回 `FALSE` 。 然后，客户端必须调用 [IDiaAddressMap：:p ut_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md) 方法，以便在提供图像本身缺少的图像标头后启用相对虚拟地址计算。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap：： set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)   
 [IDiaAddressMap：： get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)   
 [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)
