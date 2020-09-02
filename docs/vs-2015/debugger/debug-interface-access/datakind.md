---
title: DataKind | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- DataKind enumeration
ms.assetid: b64be708-22d6-4360-99e7-8f4e6b196de7
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a6a72d1093bc8acd9aae788ff357aee2efeb9e52
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197639"
---
# <a name="datakind"></a>DataKind
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指示数据值的特定范围。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum DataKind {   
   DataIsUnknown,  
   DataIsLocal,  
   DataIsStaticLocal,  
   DataIsParam,  
   DataIsObjectPtr,  
   DataIsFileStatic,  
   DataIsGlobal,  
   DataIsMember,  
   DataIsStaticMember,  
   DataIsConstant  
};  
```  
  
## <a name="elements"></a>元素  
 DataIsUnknown  
 无法确定数据符号。  
  
 DataIsLocal  
 数据项是局部变量。  
  
 DataIsStaticLocal  
 数据项是一个静态局部变量。  
  
 DataIsParam  
 数据项是一个形参。  
  
 DataIsObjectPtr  
 数据项是 () 的对象指针 `this` 。  
  
 DataIsFileStatic  
 数据项是文件范围的变量。  
  
 DataIsGlobal  
 数据项是全局变量。  
  
 DataIsMember  
 数据项是一个对象成员变量。  
  
 DataIsStaticMember  
 数据项是类静态变量。  
  
 DataIsConstant  
 数据项是一个常数值。  
  
## <a name="remarks"></a>备注  
 此枚举中的值由 [IDiaSymbol：： get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md) 方法返回。  
  
## <a name="requirements"></a>要求  
 标头： cvconst  
  
## <a name="see-also"></a>另请参阅  
 [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)
