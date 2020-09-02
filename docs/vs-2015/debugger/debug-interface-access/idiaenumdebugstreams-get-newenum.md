---
title: IDiaEnumDebugStreams::get__NewEnum | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::get__NewEnum method
ms.assetid: 972372ff-abfc-4987-a302-7788fab90348
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d94b7f082c4e748c745d90160912acdf8e7daa6e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187335"
---
# <a name="idiaenumdebugstreamsget__newenum"></a>IDiaEnumDebugStreams::get__NewEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> 此枚举器的版本。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get__NewEnum (   
   IUnknown** pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 pRetVal  
 弄返回 `IUnknown` 一个接口，该接口表示 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> 此枚举器的版本。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)
