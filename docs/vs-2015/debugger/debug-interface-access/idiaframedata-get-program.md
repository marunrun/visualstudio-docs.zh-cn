---
title: IDiaFrameData::get_program | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_program method
ms.assetid: 9201409e-b4b1-4e2e-a9f8-d17678ac538b
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d87f5c7fda25a901d44b9f511b9a92eb4471f845
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180001"
---
# <a name="idiaframedataget_program"></a>IDiaFrameData::get_program
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索用于在调用当前函数之前计算注册集的程序字符串。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_program (   
   BSTR* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄返回程序字符串。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 程序字符串是一系列用于建立序言的宏。 例如，典型的堆栈帧可能使用程序字符串 `"$T0 $ebp = $eip $T0 4 + ^ = $ebp $T0 ^ = $esp $T0 8 + ="` 。 格式为反转波兰表示法，其中运算符遵循操作数。 `T0` 表示堆栈上的临时变量。 此示例执行以下步骤：  
  
1. 将注册的内容移动 `ebp` 到 `T0` 。  
  
2. 将添加 `4` 到中的值 `T0` 以生成地址，从该地址获取该值，并将该值存储在 register 中 `eip` 。  
  
3. 获取中存储的地址的值 `T0` ，并将该值存储在 register 中 `ebp` 。  
  
4. 将添加 `8` 到中的值 `T0` ，并将该值存储在 register 中 `esp` 。  
  
   请注意，程序字符串特定于 CPU，并且针对当前堆栈帧所表示的函数设置的调用约定。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
