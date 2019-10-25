---
title: 符号类型的类层次结构 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], class hierarchies
ms.assetid: 0ccd6990-4654-44cd-a6f3-bdd82fe90f6c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3c42ea4bb2d5c2ad91538bec8b31774a5a41aa4d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745460"
---
# <a name="class-hierarchy-of-symbol-types"></a>符号类型的类层次结构
下表描述了类层次结构中的符号类型。

## <a name="symbol-types"></a>符号类型

|符号类型|描述|
|-----------------|-----------------|
|[UDT](../../debugger/debug-interface-access/udt.md)|用于表示每个类、结构和联合的符号。|
|[枚举（调试接口访问 SDK）](../../debugger/debug-interface-access/enum-debug-interface-access-sdk.md)|枚举类型的符号。|
|[PointerType](../../debugger/debug-interface-access/pointertype.md)|指针类型的符号。|
|[ArrayType](../../debugger/debug-interface-access/arraytype.md)|数组类型的符号。|
|[BaseType](../../debugger/debug-interface-access/basetype.md)|基类型符号|
|[Typedef（调试接口访问 SDK）](../../debugger/debug-interface-access/typedef-debug-interface-access-sdk.md)|为其他类型引入名称的符号。|
|[BaseClass](../../debugger/debug-interface-access/baseclass.md)|用于用户定义类型（UDT）的每个基类的符号。|
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

## <a name="see-also"></a>请参阅
- [CV_access_e 枚举](../../debugger/debug-interface-access/cv-access-e.md)
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [符号和符号标记](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)