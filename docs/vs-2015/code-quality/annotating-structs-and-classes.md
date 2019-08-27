---
title: 批注结构和类 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _Field_size_bytes_part_
- _Field_size_bytes_full_opt_
- _Field_size_bytes_
- _Field_size_opt_
- _Field_size_part_
- _Field_size_bytes_part_opt_
- _Field_range_
- _Field_size_part_opt_
- _Field_size_
- _Field_size_bytes_opt_
- _Struct_size_bytes_
- _Field_size_bytes_full_
- _Field_size_full_
- _Field_size_full_opt_
ms.assetid: b8278a4a-c86e-4845-aa2a-70da21a1dd52
caps.latest.revision: 11
author: mikeblome
ms.author: mblome
manager: jillfra
ms.openlocfilehash: df2e75bb3dd01d051d8fed29748e499f8f620128
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157081"
---
# <a name="annotating-structs-and-classes"></a>批注结构和类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以通过使用类似于固定条件注释批注结构和类成员，它们都假定为满足的任何函数调用或进入/退出函数涉及封闭结构作为参数或结果值。  
  
## <a name="struct-and-class-annotations"></a>结构和类批注  
  
- `_Field_range_(low, high)`  
  
     该字段是从 （含） 范围内`low`到`high`。  等效于`_Satisfies_(_Curr_ >= low && _Curr_ <= high)`通过使用适当的前置或后置条件应用于带批注的对象。  
  
- `_Field_size_(size)`, `_Field_size_opt_(size)`, `_Field_size_bytes_(size)`, `_Field_size_bytes_opt_(size)`  
  
     具有可写大小以元素 （或字节数） 为指定的字段`size`。  
  
- `_Field_size_part_(size, count)`, `_Field_size_part_opt_(size, count)`,         `_Field_size_bytes_part_(size, count)`, `_Field_size_bytes_part_opt_(size, count)`  
  
     具有可写大小以元素 （或字节数） 为指定的字段`size`，和`count`这些元素 （字节） 的可读。  
  
- `_Field_size_full_(size)`, `_Field_size_full_opt_(size)`, `_Field_size_bytes_full_(size)`, `_Field_size_bytes_full_opt_(size)`  
  
     具有可读和可写大小元素 （或字节数） 为指定的字段`size`。  
  
- `_Struct_size_bytes_(size)`  
  
     具有可读和可写大小元素 （或字节数） 为指定的字段`size`。  
  
     适用于结构或类声明。  指示该类型的有效对象，可能与指定的字节数会大于声明的类型， `size`。  例如：  
  
    ```cpp  
  
    typedef _Struct_size_bytes_(nSize)  
    struct MyStruct {  
        size_t nSize;  
        …  
    };  
  
    ```  
  
     以字节为单位的参数的缓冲区大小`pM`类型的`MyStruct *`然后将其视为：  
  
    ```cpp  
    min(pM->nSize, sizeof(MyStruct))  
    ```  
  
## <a name="see-also"></a>请参阅  
 [使用 SAL 注释减少 C /C++代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [了解 SAL](../code-quality/understanding-sal.md)   
 [对函数参数和返回值进行批注](../code-quality/annotating-function-parameters-and-return-values.md)   
 [对函数行为进行批注](../code-quality/annotating-function-behavior.md)   
 [对锁定行为进行批注](../code-quality/annotating-locking-behavior.md)   
 [指定何时以及在何处应用批注](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [内部函数](../code-quality/intrinsic-functions.md)   
 [最佳做法和示例](../code-quality/best-practices-and-examples-sal.md)
