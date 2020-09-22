---
title: IDiaAddressMap::put_imageAlign | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_imageAlign method
ms.assetid: f9ce875d-c263-43e5-a534-f34c37f9866f
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5e0fa57c38c8451bde84d96ab32bc7980c5e2d8b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840494"
---
# <a name="idiaaddressmapput_imagealign"></a>IDiaAddressMap::put_imageAlign
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设置图像的对齐方式。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT put_imageAlign (   
   DWORD NewVal  
);  
```  
  
#### <a name="parameters"></a>parameters  
 NewVal  
 中可执行文件的新图像对齐值。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
  (加载的可执行文件) 的图像与指定的内存边界对齐。 此对齐方式可能受到当前系统体系结构以及编译和链接时间选项的影响。 图像对齐始终在字节边界上。 以下图像对齐值有效：1、2、4、8、16、32和64字节边界。  
  
 可以通过调用 [IDiaAddressMap：： get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md) 方法检索当前图像对齐方式。  
  
> [!NOTE]
> 此方法可被调用时已加载。 此 `put_imageAlign` 方法通常在图像已移动或更改并且需要新对齐时使用。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)
