---
title: IDiaStackWalkHelper::pdataForVA | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::pdataByVA method
ms.assetid: fafc38fe-74dc-4726-9a51-eebf3a673d7f
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5af921caa989d7279bb9f52751c452d91045cf3e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150093"
---
# <a name="idiastackwalkhelperpdataforva"></a>IDiaStackWalkHelper::pdataForVA
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

返回与虚拟地址相关联的 PDATA 数据块。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT pdataForVA(   
   ULONGLONG  va,  
   DWORD      cbData,  
   DWORD*     pcbData,  
   BYTE*      pbData  
);  
```  
  
#### <a name="parameters"></a>参数  
 `va`  
 中指定要获取的数据的虚拟地址。  
  
 `cbData`  
 中要获取的数据的大小（以字节为单位）。  
  
 `pcbData`  
 弄返回获取的数据的实际大小（以字节为单位）。  
  
 `pbData`  
 [in，out]使用请求的数据填充的缓冲区。 不能为 `NULL`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果指定地址没有 PDATA，则返回。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 PDATA (名为 "PDATA" 的节 ) 编译单位包含有关函数的异常处理的信息。  
  
 调用方知道要返回多少数据，以便调用方无需询问可用数据量。 因此，如果参数为，则此方法的实现可以返回错误 `pbData` `NULL` 。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
