---
title: CV_call_e | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_call_e enumeration
ms.assetid: f230560b-4243-432d-8f19-46df112043b9
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cd1ee4c024894e5752277a5000d37745c88c4ac6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442106"
---
# <a name="cvcalle"></a>CV_call_e
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定的函数的调用约定。  
  
> [!NOTE]
> 此处介绍了仅是最常见的枚举值。 完整的枚举是 cvconst.h 标头文件中。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef enum CV_call_e {   
   CV_CALL_NEAR_C    = 0x00,  
   CV_CALL_NEAR_FAST = 0x04,  
   CV_CALL_NEAR_STD  = 0x07,  
   CV_CALL_NEAR_SYS  = 0x09,  
   CV_CALL_THISCALL  = 0x0b,  
   CV_CALL_CLRCALL   = 0x16  
} CV_call_e;  
```  
  
## <a name="elements"></a>元素  
 CV_CALL_NEAR_C  
 指定使用近右到左推送的函数调用约定。 调用函数清除堆栈。  
  
 CV_CALL_NEAR_FAST  
 指定使用寄存器使用几乎从左到右推式函数调用约定。 被调用的函数使用参数的字节数之和来清除堆栈。  
  
 CV_CALL_NEAR_STD  
 指定使用近乎标准调用 （从右到左推送） 的函数调用约定。  
  
 CV_CALL_NEAR_SYS  
 指定通过近乎系统调用的函数调用约定。  
  
 CV_CALL_THISCALL  
 函数调用约定使用指定`this`调用 (`this`在寄存器中传递的指针)。  
  
 CV_CALL_CLRCALL  
 指定使用由公共语言运行时 (CLR) （也称为托管代码调用约定） 的函数调用约定。  
  
## <a name="remarks"></a>备注  
 此枚举中的值返回通过调用[idiasymbol:: Get_callingconvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)方法。  
  
## <a name="requirements"></a>要求  
 标头： cvconst.h  
  
## <a name="see-also"></a>请参阅  
 [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)
