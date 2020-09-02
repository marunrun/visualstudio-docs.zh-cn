---
title: IDiaStackWalkFrame：： readMemory |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150166"
---
# <a name="idiastackwalkframereadmemory"></a>IDiaStackWalkFrame::readMemory
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

从映像读取内存。  
  
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
  
#### <a name="parameters"></a>参数  
 `type`  
 中 [MemoryTypeEnum 枚举](../../debugger/debug-interface-access/memorytypeenum.md) 值之一，用于指定要访问的内存类型。  
  
 `va`  
 中要开始读取的映像中的虚拟地址位置。  
  
 `cbData`  
 中数据缓冲区的大小（以字节为单位）。  
  
 `pcbData`  
 弄返回返回的字节数。 如果 `data` 为 `NULL` ，则 `pcbData` 包含可用数据的总字节数。  
  
 `data`  
 弄要使用来自指定位置的数据进行填充的缓冲区。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
