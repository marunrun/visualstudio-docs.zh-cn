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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68179190"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定的堆栈帧类型。  
  
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
 帧指针省略;FPO 信息可用。  
  
 `FrameTypeTrap`  
 内核陷阱帧。  
  
 `FrameTypeTSS`  
 内核陷阱帧。  
  
 `FrameTypeStandard`  
 标准 EBP 堆栈帧。  
  
 `FrameTypeFrameData`  
 帧指针省略;帧数据信息可用。  
  
 `FrameTypeUnknown`  
 不具有任何调试信息的帧。  
  
## <a name="remarks"></a>备注  
 此枚举中的值返回通过调用[idiastackframe:: Get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)方法。  
  
## <a name="requirements"></a>要求  
 标头： cvconst.h  
  
## <a name="see-also"></a>请参阅  
 [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
