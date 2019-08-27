---
title: IDiaEnumSourceFiles::Next | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Next method
ms.assetid: 83bf6317-ff39-4c5c-8987-cba34e7a6983
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fe965043ad854c31c933447452f1039ba40cd04a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189824"
---
# <a name="idiaenumsourcefilesnext"></a>IDiaEnumSourceFiles::Next
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索指定的数目的枚举序列中的源文件。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Next (   
   ULONG            celt,  
   IDiaSourceFile** rgelt,  
   ULONG*           pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 celt  
 [in]要检索的枚举器中的源文件数。  
  
 rgelt  
 [out]数组，它是在用来填充[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象表示所需的源文件。  
  
 pceltFetched  
 [out]返回在提取枚举器中的源文件数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果没有更多的源文件。 否则，返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)   
 [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)   
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
