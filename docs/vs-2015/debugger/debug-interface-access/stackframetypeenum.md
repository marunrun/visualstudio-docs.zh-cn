---
title: StackFrameTypeEnum | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- StackFrameTypeEnum enumeration
ms.assetid: 61e40163-eee0-4c1f-af47-cef3771bdc41
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 655911bac1efbafe1838e24e2056282f9036479b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179190"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定堆栈帧类型。  
  
## <a name="syntax"></a>语法  
  
```cpp  
enum StackFrameTypeEnum {  
   FrameTypeFPO,  
   FrameTypeTrap,  
   FrameTypeTSS,  
   FrameTypeStandard,  
   FrameTypeFrameData,  
   FrameTypeUnknown = -1  
};  
```  
  
## <a name="elements"></a>元素  
 `FrameTypeFPO`  
 省略帧指针;可用的 FPO 信息。  
  
 `FrameTypeTrap`  
 内核捕获帧。  
  
 `FrameTypeTSS`  
 内核捕获帧。  
  
 `FrameTypeStandard`  
 标准 EBP 堆栈帧。  
  
 `FrameTypeFrameData`  
 省略帧指针;提供框架数据信息。  
  
 `FrameTypeUnknown`  
 不包含任何调试信息的帧。  
  
## <a name="remarks"></a>备注  
 此枚举中的值由对 [IDiaStackFrame：： get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md) 方法的调用返回。  
  
## <a name="requirements"></a>要求  
 标头： cvconst  
  
## <a name="see-also"></a>另请参阅  
 [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
