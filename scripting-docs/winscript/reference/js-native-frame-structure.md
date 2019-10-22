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
ms.openlocfilehash: a0b624229a96cfc2a2d2044a926f45fa91a1c76c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571762"
---
# <a name="js_native_frame-structure"></a>JS_NATIVE_FRAME 结构
表示堆栈帧。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct {  
    UINT64 InstructionOffset;    UINT64 ReturnOffset;    UINT64 FrameOffset;    UINT64 StackOffset;  
} JS_NATIVE_FRAME;  
```  
  
## <a name="members"></a>Members  
 `InstructionOffset`  
 指令指针。  
  
 `ReturnOffset`  
 寄信人地址。  
  
 `FrameOffset`  
 帧指针。  
  
 `StackOffset`  
 堆栈指针。  
  
## <a name="remarks"></a>备注  
 @No__t_1 使用 `JS_NATIVE_FRAME` 结构。  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)