---
title: OBJECT_TYPE | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- OBJECT_TYPE
helpviewer_keywords:
- OBJECT_TYPE enumeration
ms.assetid: c4d246f9-8a98-44ec-b2bb-ff5c684f668e
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc23045fa70554133eba3a7f1326681bf31ea379
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205145"
---
# <a name="objecttype"></a>OBJECT_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定的表达式计算器中的对象的类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_OBJECT_TYPE {   
   OBJECT_TYPE_BOOLEAN = 0x0,  
   OBJECT_TYPE_CHAR    = 0x1,  
   OBJECT_TYPE_I1      = 0x2,  
   OBJECT_TYPE_U1      = 0x3,  
   OBJECT_TYPE_I2      = 0x4,  
   OBJECT_TYPE_U2      = 0x5,  
   OBJECT_TYPE_I4      = 0x6,  
   OBJECT_TYPE_U4      = 0x7,  
   OBJECT_TYPE_I8      = 0x8,  
   OBJECT_TYPE_U8      = 0x9,  
   OBJECT_TYPE_R4      = 0xa,  
   OBJECT_TYPE_R8      = 0xb,  
   OBJECT_TYPE_OBJECT  = 0xc,  
   OBJECT_TYPE_NULL    = 0xd,  
   OBJECT_TYPE_CLASS   = 0xe  
};  
typedef DWORD OBJECT_TYPE;  
```  
  
```csharp  
public enum enum_OBJECT_TYPE {   
   OBJECT_TYPE_BOOLEAN = 0x0,  
   OBJECT_TYPE_CHAR    = 0x1,  
   OBJECT_TYPE_I1      = 0x2,  
   OBJECT_TYPE_U1      = 0x3,  
   OBJECT_TYPE_I2      = 0x4,  
   OBJECT_TYPE_U2      = 0x5,  
   OBJECT_TYPE_I4      = 0x6,  
   OBJECT_TYPE_U4      = 0x7,  
   OBJECT_TYPE_I8      = 0x8,  
   OBJECT_TYPE_U8      = 0x9,  
   OBJECT_TYPE_R4      = 0xa,  
   OBJECT_TYPE_R8      = 0xb,  
   OBJECT_TYPE_OBJECT  = 0xc,  
   OBJECT_TYPE_NULL    = 0xd,  
   OBJECT_TYPE_CLASS   = 0xe  
};  
```  
  
## <a name="members"></a>成员  
 OBJECT_TYPE_BOOLEAN  
 指示对象是一个布尔值。  
  
 OBJECT_TYPE_CHAR  
 指示对象是一个字符。  
  
 OBJECT_TYPE_I1  
 指示对象是单字节有符号的整数。  
  
 OBJECT_TYPE_U1  
 指示对象是单字节无符号的整数。  
  
 OBJECT_TYPE_I2  
 指示对象是双字节有符号的整数。  
  
 OBJECT_TYPE_U2  
 指示对象是双字节无符号的整数。  
  
 OBJECT_TYPE_I4  
 指示对象是一个四字节有符号的整数。  
  
 OBJECT_TYPE_U4  
 指示对象是一个四字节无符号的整数。  
  
 OBJECT_TYPE_I8  
 指示对象是一个 8 字节有符号的整数。  
  
 OBJECT_TYPE_U8  
 指示对象是一个 8 字节无符号的整数。  
  
 OBJECT_TYPE_R4  
 指示对象是一个 4 字节浮点数。  
  
 OBJECT_TYPE_R8  
 指示对象是 8 字节浮点数。  
  
 OBJECT_TYPE_OBJECT  
 指示对象是一个对象。  
  
 OBJECT_TYPE_NULL  
 指示对象为 NULL。  
  
 OBJECT_TYPE_CLASS  
 指示对象是一个类。  
  
## <a name="remarks"></a>备注  
 作为参数传递[CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)并[CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)方法。  
  
## <a name="requirements"></a>要求  
 标头： ee.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)   
 [CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)
