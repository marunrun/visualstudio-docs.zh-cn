---
title: IDiaStackWalkHelper：： readMemory |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::readMemory method
ms.assetid: e1eb90aa-49b7-476c-9e70-7e8f08994cbe
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8bef01cd29bb2312bd682f2f1f1150ee78da293e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150060"
---
# <a name="idiastackwalkhelperreadmemory"></a>IDiaStackWalkHelper::readMemory
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

从可执行文件的图像的内存中读取数据块。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT readMemory(   
   enum MemoryTypeEnum type,  
   ULONGLONG           va,  
   DWORD               cbData,  
   DWORD*              pcbData,  
   BYTE*               pbData  
);  
```  
  
#### <a name="parameters"></a>参数  
 `type`  
 中 [MemoryTypeEnum 枚举](../../debugger/debug-interface-access/memorytypeenum.md) 枚举中的一个值，该值指定要读取的内存类型。  
  
 va  
 中要从其开始读取的映像中的虚拟地址。  
  
 `cbData`  
 中数据缓冲区的大小（以字节为单位）。  
  
 `pcbData`  
 弄返回实际读取的字节数。 如果 `pbData` 为 `NULL` ，则这是可用数据的总字节数。  
  
 `pbData`  
 [in，out]填充内存读取的缓冲区。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)   
 [MemoryTypeEnum 枚举](../../debugger/debug-interface-access/memorytypeenum.md)
