---
title: IDiaEnumSourceFiles::Item | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Item method
ms.assetid: 3c19d7ed-0232-4b0e-9b10-f33ed9e0c93b
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 62dce70d3ebf05694b453d13e1f11529dd21e8ce
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189783"
---
# <a name="idiaenumsourcefilesitem"></a>IDiaEnumSourceFiles::Item
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

通过索引检索源文件。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Item (   
   DWORD            index,  
   IDiaSourceFile** sourceFile  
);  
```  
  
#### <a name="parameters"></a>参数  
 索引  
 中要检索的 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) 对象的索引。 索引介于0到 `count` -1 之间，其中 `count` 由 [IDiaEnumSourceFiles：： get_Count](../../debugger/debug-interface-access/idiaenumsourcefiles-get-count.md) 方法返回。  
  
 sourceFile  
 弄返回一个 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) 对象，该对象表示所需的源文件。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)   
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
