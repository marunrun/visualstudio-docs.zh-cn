---
title: IDiaStackWalkHelper：： imageForVA |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper::imageForVA method
ms.assetid: 8d4edabf-3c01-4fef-8b61-4779f3371067
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 36ad6529f28701d0e6d83550636382be773f0ec1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150100"
---
# <a name="idiastackwalkhelperimageforva"></a>IDiaStackWalkHelper::imageForVA
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

如果可执行文件的内存空间中某个位置有一个虚拟地址，则返回该可执行文件的图像在内存中的起始位置。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT imageForVA(  
   ULONGLONG  vaContext,  
   ULONGLONG *pvaImageStart  
);  
```  
  
#### <a name="parameters"></a>参数  
 `vaContext`  
 中位于可执行空间中某个位置的虚拟地址。  
  
 `pvaImageStart`  
 弄返回可执行文件的映像的起始虚拟地址。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
