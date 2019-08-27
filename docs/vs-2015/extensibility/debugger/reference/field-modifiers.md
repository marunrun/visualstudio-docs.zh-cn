---
title: FIELD_MODIFIERS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- FIELD_MODIFIERS
helpviewer_keywords:
- FIELD_MODIFIERS enumeration
ms.assetid: 1e44681c-1f03-41a9-9c04-b79f231b0822
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bd25a3cb5b2d074e989b47f33513e05538868759
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203037"
---
# <a name="fieldmodifiers"></a>FIELD_MODIFIERS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定字段类型修饰符。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_FIELD_MODIFIERS {   
   FIELD_MOD_NONE             = 0x00000000,  
  
   // Modifier of the field  
   FIELD_MOD_ACCESS_NONE      = 0x00000001,  
   FIELD_MOD_ACCESS_PUBLIC    = 0x00000002,  
   FIELD_MOD_ACCESS_PROTECTED = 0x00000004,  
   FIELD_MOD_ACCESS_PRIVATE   = 0x00000008,  
  
   // Storage modifier of the field  
   FIELD_MOD_NOMODIFIERS      = 0x00000010,  
   FIELD_MOD_STATIC           = 0x00000020,  
   FIELD_MOD_CONSTANT         = 0x00000040,  
   FIELD_MOD_TRANSIENT        = 0x00000080,  
   FIELD_MOD_VOLATILE         = 0x00000100,  
   FIELD_MOD_ABSTRACT         = 0x00000200,  
   FIELD_MOD_NATIVE           = 0x00000400,  
   FIELD_MOD_SYNCHRONIZED     = 0x00000800,  
   FIELD_MOD_VIRTUAL          = 0x00001000,  
   FIELD_MOD_INTERFACE        = 0x00002000,  
   FIELD_MOD_FINAL            = 0x00004000,  
   FIELD_MOD_SENTINEL         = 0x00008000,  
   FIELD_MOD_INNERCLASS       = 0x00010000,  
   FIELD_TYPE_OPTIONAL        = 0x00020000,  
   FIELD_MOD_BYREF            = 0x00040000,  
   FIELD_MOD_HIDDEN           = 0x00080000,  
   FIELD_MOD_MARSHALASOBJECT  = 0x00100000,  
   FIELD_MOD_SPECIAL_NAME     = 0x00200000,  
   FIELD_MOD_HIDEBYSIG        = 0x00400000,  
  
   FIELD_MOD_WRITEONLY        = 0x80000000,  
   FIELD_MOD_ACCESS_MASK      = 0x000000ff,  
   FIELD_MOD_MASK             = 0xffffff00,  
   FIELD_MOD_ALL              = 0x7fffffff  
};  
typedef DWORD FIELD_MODIFIERS;  
```  
  
```csharp  
public enum enum_FIELD_MODIFIERS {  
   FIELD_MOD_NONE             = 0x00000000,  
  
   // Modifier of the field  
   FIELD_MOD_ACCESS_NONE      = 0x00000001,  
   FIELD_MOD_ACCESS_PUBLIC    = 0x00000002,  
   FIELD_MOD_ACCESS_PROTECTED = 0x00000004,  
   FIELD_MOD_ACCESS_PRIVATE   = 0x00000008,  
  
   // Storage modifier of the field  
   FIELD_MOD_NOMODIFIERS      = 0x00000010,  
   FIELD_MOD_STATIC           = 0x00000020,  
   FIELD_MOD_CONSTANT         = 0x00000040,  
   FIELD_MOD_TRANSIENT        = 0x00000080,  
   FIELD_MOD_VOLATILE         = 0x00000100,  
   FIELD_MOD_ABSTRACT         = 0x00000200,  
   FIELD_MOD_NATIVE           = 0x00000400,  
   FIELD_MOD_SYNCHRONIZED     = 0x00000800,  
   FIELD_MOD_VIRTUAL          = 0x00001000,  
   FIELD_MOD_INTERFACE        = 0x00002000,  
   FIELD_MOD_FINAL            = 0x00004000,  
   FIELD_MOD_SENTINEL         = 0x00008000,  
   FIELD_MOD_INNERCLASS       = 0x00010000,  
   FIELD_TYPE_OPTIONAL        = 0x00020000,  
   FIELD_MOD_BYREF            = 0x00040000,  
   FIELD_MOD_HIDDEN           = 0x00080000,  
   FIELD_MOD_MARSHALASOBJECT  = 0x00100000,  
   FIELD_MOD_SPECIAL_NAME     = 0x00200000,  
   FIELD_MOD_HIDEBYSIG        = 0x00400000,  
  
   FIELD_MOD_WRITEONLY        = 0x80000000,  
   FIELD_MOD_ACCESS_MASK      = 0x000000ff,  
   FIELD_MOD_MASK             = 0xffffff00,  
   FIELD_MOD_ALL              = 0x7fffffff  
};  
```  
  
## <a name="members"></a>成员  
 FIELD_MOD_ACCESS_TYPE  
 指示不能访问该字段。  
  
 FIELD_MOD_ACCESS_PUBLIC  
 指示该字段具有公共访问权限。  
  
 FIELD_MOD_ACCESS_PROTECTED  
 指示该字段具有受保护的访问。  
  
 FIELD_MOD_ACCESS_PRIVATE  
 指示该字段具有私有访问权限。  
  
 FIELD_MOD_NOMODIFIERS  
 指示该字段具有没有修饰符。  
  
 FIELD_MOD_STATIC  
 指示该字段是静态的。  
  
 FIELD_MOD_CONSTANT  
 指示字段是一个常量。  
  
 FIELD_MOD_TRANSIENT  
 指示该字段为暂时性。  
  
 FIELD_MOD_VOLATILE  
 指示该字段是易失性。  
  
 FIELD_MOD_ABSTRACT  
 指示该字段为抽象。  
  
 FIELD_MOD_NATIVE  
 指示该字段是本机。  
  
 FIELD_MOD_SYNCHRONIZED  
 指示该字段保持同步。  
  
 FIELD_MOD_VIRTUAL  
 指示该字段是虚拟。  
  
 FIELD_MOD_INTERFACE  
 指示该字段是一个接口。  
  
 FIELD_MOD_FINAL  
 指示该字段是最后一个。  
  
 FIELD_MOD_SENTINEL  
 指示该字段是 sentinel。  
  
 FIELD_MOD_INNERCLASS  
 指示该字段是一个内部类。  
  
 FIELD_TYPE_OPTIONAL  
 指示字段是可选的。  
  
 FIELD_MOD_BYREF  
 指示该字段是引用自变量。 这是专门为方法参数。  
  
 FIELD_MOD_HIDDEN  
 指示字段必须是隐藏或显示在另一个上下文中;例如，[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]静态局部变量。  
  
 FIELD_MOD_MARSHALASOBJECT  
 指示此字段表示的对象`IUnknown`接口。  
  
 FIELD_MOD_SPECIAL_NAME  
 指示该字段具有特殊名称，例如，`.ctor`的构造函数 ([!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]仅)。  
  
 FIELD_MOD_HIDEBYSIG  
 指示该字段具有`Overloads`关键字应用于它 ([!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]仅)。  
  
 FIELD_MOD_WRITEONLY  
 指示该字段是只写。 此值不包括在`FIELD_MOD_ALL`，因为此类只写字段的唯一用途是函数求值。 用户必须明确地要求提供`FIELD_MOD_WRITEONLY`字段。  
  
 FIELD_MOD_ACCESS_MASK  
 指示字段访问掩码。  
  
 FIELD_MOD_MASK  
 指示字段修饰符的掩码。  
  
## <a name="remarks"></a>备注  
 用于`dwModifiers`的成员[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)结构。  
  
 这些值也将传递给[EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)方法来筛选特定字段。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)   
 [EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)
