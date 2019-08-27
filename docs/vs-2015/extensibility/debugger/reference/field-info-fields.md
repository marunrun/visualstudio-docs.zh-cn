---
title: FIELD_INFO_FIELDS | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- FIELD_INFO_FIELDS
helpviewer_keywords:
- FIELD_INFO_FIELDS enumeration
ms.assetid: a69487d2-e701-4165-804a-8a011df9a3bd
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e3f947db7606d6f7495cb1d88591aafa9e9933b6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62423707"
---
# <a name="fieldinfofields"></a>FIELD_INFO_FIELDS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要检索相关信息[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_FIELD_INFO_FIELDS {   
   FIF_FULLNAME  = 0x0001,  
   FIF_NAME      = 0x0002,  
   FIF_TYPE      = 0x0004,  
   FIF_MODIFIERS = 0x0008,  
   FIF_ALL       = 0xffffffff,  
   FIF_NONE      = 0x0000  
};  
typedef DWORD FIELD_INFO_FIELDS;  
```  
  
```csharp  
public enum enum_FIELD_INFO_FIELDS {  
   FIF_FULLNAME  = 0x0001,  
   FIF_NAME      = 0x0002,  
   FIF_TYPE      = 0x0004,  
   FIF_MODIFIERS = 0x0008,  
   FIF_ALL       = 0xffffffff,  
   FIF_NONE      = 0x0000  
};  
```  
  
## <a name="members"></a>成员  
 FIF_FULLNAME  
 初始化/用`bstrFullName`字段中[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)结构。  
  
 FIF_NAME  
 初始化/用`bstrName`字段中`FIELD_INFO`结构。  
  
 FIF_TYPE  
 初始化/用`bstrType`字段中`FIELD_INFO`结构。  
  
 FIF_MODIFIERS  
 初始化/用`bstrModifiers`字段中`FIELD_INFO`结构。  
  
## <a name="remarks"></a>备注  
 这些值也会作为参数传递[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)方法，以指定的哪些字段[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)结构是进行初始化。  
  
 中还使用这些值`dwFields`的成员`FIELD_INFO`结构，用于指示哪些字段是使用，有效。  
  
 可能的按位组合这些标志`OR`。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
