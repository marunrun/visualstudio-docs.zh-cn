---
title: JS_NATIVE_FRAME 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- JS_NATIVE_FRAME
apilocation:
- jscript9diag.dll
ms.assetid: 5afa2ee1-b3e2-47cb-b304-84f96e6fbb14
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9a0777cf42b9ed9412602cb34ed2d521deca1fb9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62968667"
---
# <a name="jsnativeframe-structure"></a>JS_NATIVE_FRAME 结构
表示堆栈帧。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct {  
    UINT64 InstructionOffset;    UINT64 ReturnOffset;    UINT64 FrameOffset;    UINT64 StackOffset;  
} JS_NATIVE_FRAME;  
```  
  
## <a name="members"></a>成员  
 `InstructionOffset`  
 指令指针中。  
  
 `ReturnOffset`  
 寄信人地址。  
  
 `FrameOffset`  
 帧指针。  
  
 `StackOffset`  
 堆栈指针。  
  
## <a name="remarks"></a>备注  
 `JS_NATIVE_FRAME`结构由`IJsStackFrameEnumerator`。  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)