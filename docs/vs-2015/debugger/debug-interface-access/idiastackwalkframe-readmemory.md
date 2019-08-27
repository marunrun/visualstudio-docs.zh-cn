---
title: 'Idiastackwalkframe:: Readmemory |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::readMemory method
ms.assetid: 7ab0b525-a5a7-4692-acad-e8c00fa9ab9a
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 97a868973d2a514150b8d728e685523e918f88f4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150166"
---
# <a name="idiastackwalkframereadmemory"></a>IDiaStackWalkFrame::readMemory
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

从图像中读取内存。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT readMemory (   
   MemoryTypeEnum type,  
   ULONGLONG va,  
   DWORD     cbData,  
   DWORD*    pcbData,  
   BYTE      data[]  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `type`  
 [in]之一[MemoryTypeEnum 枚举](../../debugger/debug-interface-access/memorytypeenum.md)枚举值，指定要访问的内存的类型。  
  
 `va`  
 [in]要开始读取图像中的虚拟地址位置。  
  
 `cbData`  
 [in]数据缓冲区，以字节为单位的大小。  
  
 `pcbData`  
 [out]返回返回的字节数。 如果`data`是`NULL`，然后`pcbData`包含可用数据的字节总数。  
  
 `data`  
 [out]若要使用从指定的位置的数据填充缓冲区。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
