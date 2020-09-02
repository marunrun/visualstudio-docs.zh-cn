---
title: IDiaFrameData::execute | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::execute method
ms.assetid: 7a6c7d03-1ff1-4059-bd54-5f407eeebc26
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4042cf58ee34b5f49df601b94e1110f03e0b6f5b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197554"
---
# <a name="idiaframedataexecute"></a>IDiaFrameData::execute
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

执行堆栈展开并返回堆栈审核帧接口中的结果。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT execute (   
   IDiaStackWalkFrame* frame  
);  
```  
  
#### <a name="parameters"></a>参数  
 `frame`  
 中保存框架寄存器状态的 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md) 对象。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。 下表显示了此方法的可能的返回值。  
  
|值|说明|  
|-----------|-----------------|  
|E_DIA_INPROLOG|无法在序言代码中执行堆栈帧。|  
|E_DIA_SYNTAX|帧程序中出现分析错误。|  
|E_DIA_FRAME_ACCESS|无法访问寄存器或内存。|  
|E_DIA_VALUE|计算值时出错 (例如，被零除) 。|  
  
## <a name="remarks"></a>备注  
 在调试过程中调用此方法展开堆栈。 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)对象由客户端应用程序实现，以接收对寄存器的更新并提供方法使用的方法 `execute` 。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
