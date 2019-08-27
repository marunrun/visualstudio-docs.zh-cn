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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442221"
---
# <a name="idiaaddressmapputimagealign"></a>IDiaAddressMap::put_imageAlign
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设置的图像对齐方式。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT put_imageAlign (   
   DWORD NewVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 NewVal  
 [in]新的图像对齐方式可执行文件有值。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 指定的内存边界对齐图像 （加载可执行文件）。 由当前的系统体系结构以及编译和链接时间选项，可能会影响此对齐方式。 图像对齐方式是始终在字节边界上。 下面的图像对齐方式值是有效的：1、 2、 4、 8、 16、 32 和 64 字节边界。  
  
 可以通过调用检索当前的图像对齐方式[idiaaddressmap:: Get_imagealign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)方法。  
  
> [!NOTE]
> 可以调用此方法时已加载图像。 `put_imageAlign`图像已被移动或更改和新的对齐方式是所需时通常使用方法。  
  
## <a name="see-also"></a>请参阅  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)
