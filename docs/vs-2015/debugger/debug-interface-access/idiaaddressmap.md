---
title: IDiaAddressMap | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap interface
ms.assetid: e6467529-508c-4328-85d7-89444ae4d1c1
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 012d6b1ca06b06f56239048fee712d898a79efa9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62547502"
---
# <a name="idiaaddressmap"></a>IDiaAddressMap
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

提供了控制 DIA SDK 如何计算的调试对象的虚拟和相对虚拟地址。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaAddressMap : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDiaAddressMap`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)|指示是否已为特定会话建立映射的地址。|  
|[IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)|指定是否应使用映射地址将符号地址转换。|  
|[IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)|指示是否启用的计算和使用的相对虚拟地址。|  
|[IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)|允许客户端启用或禁用相对虚拟地址的计算。|  
|[IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)|检索当前的图像对齐方式。|  
|[IDiaAddressMap::put_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-put-imagealign.md)|设置的图像对齐方式。|  
|[IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)|设置映像标头，以便启用的相对虚拟地址转换。|  
|[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)|提供映射的地址以支持图像布局翻译。|  
  
## <a name="remarks"></a>备注  
 此接口由提供的控件封装在您提供的数据的两个集： 映像标头和地址映射。 大多数客户端使用[idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)方法来查找正确的调试信息的映像和方法可以通常发现的所有必要的标头和映射数据本身。 不过，某些客户端实现专用的处理和搜索数据。 此类客户端使用的方法`IDiaAddressMap`DIA SDK 提供搜索结果的接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口是可从 DIA 会话对象。 客户端调用`QueryInterface`DIA 会话对象接口方法，通常[IDiaSession](../../debugger/debug-interface-access/idiasession.md)来检索`IDiaAddressMap`接口。  
  
## <a name="requirements"></a>要求  
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
