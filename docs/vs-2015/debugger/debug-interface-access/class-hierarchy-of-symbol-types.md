---
title: 符号类型的类层次结构 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], class hierarchies
ms.assetid: 0ccd6990-4654-44cd-a6f3-bdd82fe90f6c
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3a7b3edb0262e3e2b4f0cde51b499e25b04aba51
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840754"
---
# <a name="class-hierarchy-of-symbol-types"></a>符号类型的类层次结构
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

下表描述了类层次结构中的符号类型。  
  
## <a name="symbol-types"></a>符号类型  
  
|符号类型|说明|  
|-----------------|-----------------|  
|[UDT](../../debugger/debug-interface-access/udt.md)|用于表示每个类、结构和联合的符号。|  
|[枚举（调试接口访问 SDK）](../../debugger/debug-interface-access/enum-debug-interface-access-sdk.md)|枚举类型的符号。|  
|[PointerType](../../debugger/debug-interface-access/pointertype.md)|指针类型的符号。|  
|[ArrayType](../../debugger/debug-interface-access/arraytype.md)|数组类型的符号。|  
|[BaseType](../../debugger/debug-interface-access/basetype.md)|基类型符号|  
|[Typedef（调试接口访问 SDK）](../../debugger/debug-interface-access/typedef-debug-interface-access-sdk.md)|为其他类型引入名称的符号。|  
|[BaseClass](../../debugger/debug-interface-access/baseclass.md)|用于用户定义类型的每个基类的符号 (UDT) 。|  
|[友元（调试接口访问 SDK）](../../debugger/debug-interface-access/friend-debug-interface-access-sdk.md)|友元类和友元函数的符号。|  
|[FunctionType](../../debugger/debug-interface-access/functiontype.md)|每个唯一函数签名的符号。|  
|[FunctionArgType](../../debugger/debug-interface-access/functionargtype.md)|函数的每个参数的符号。|  
|[VTableShape](../../debugger/debug-interface-access/vtableshape.md)|虚拟表大小的符号。|  
|[VTable](../../debugger/debug-interface-access/vtable.md)|用于虚拟表的符号。|  
|[CustomType](../../debugger/debug-interface-access/customtype.md)|供应商定义的类型的符号。|  
|[ManagedType](../../debugger/debug-interface-access/managedtype.md)|在元数据中定义的类型的符号。|  
|[维度](../../debugger/debug-interface-access/dimension.md)|数组维度的符号。|  
  
> [!NOTE]
> 每个符号可以具有保存有关符号的信息以及对其他符号的引用的属性。 各个符号主题中列出了这些属性。  
  
## <a name="see-also"></a>另请参阅  
 [CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)   
 [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [符号和符号标记](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)
