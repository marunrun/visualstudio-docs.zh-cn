---
title: DEBUGPROP_INFO_FLAGS | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DEBUGPROP_INFO_FLAGS
helpviewer_keywords:
- DBGPROP_INFO_FLAGS enumeration
ms.assetid: 1c7fe777-615e-4929-9ed4-970d9fe0eb81
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 764d28972575e8da9ef499e6d33a4a4a1deb3b07
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68143001"
---
# <a name="debugpropinfoflags"></a>DEBUGPROP_INFO_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要检索有关调试属性对象的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_DEBUGPROP_INFO_FLAGS {   
   DEBUGPROP_INFO_FULLNAME          = 0x00000001,  
   DEBUGPROP_INFO_NAME              = 0x00000002,  
   DEBUGPROP_INFO_TYPE              = 0x00000004,  
   DEBUGPROP_INFO_VALUE             = 0x00000008,  
   DEBUGPROP_INFO_ATTRIB            = 0x00000010,  
   DEBUGPROP_INFO_PROP              = 0x00000020,  
   DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,  
   DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,  
   DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,  
   DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000  
   DEBUGPROP_INFO_NONE              = 0x00000000,  
   DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |  
                                      DEBUGPROP_INFO_NAME |  
                                      DEBUGPROP_INFO_TYPE |  
                                      DEBUGPROP_INFO_VALUE,  
   DEBUGPROP_INFO_ALL               = 0xffffffff  
};  
typedef DWORD DEBUGPROP_INFO_FLAGS;  
```  
  
```csharp  
public enum enum_DEBUGPROP_INFO_FLAGS {   
   DEBUGPROP_INFO_FULLNAME          = 0x00000001,  
   DEBUGPROP_INFO_NAME              = 0x00000002,  
   DEBUGPROP_INFO_TYPE              = 0x00000004,  
   DEBUGPROP_INFO_VALUE             = 0x00000008,  
   DEBUGPROP_INFO_ATTRIB            = 0x00000010,  
   DEBUGPROP_INFO_PROP              = 0x00000020,  
   DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,  
   DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,  
   DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,  
   DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000  
   DEBUGPROP_INFO_NONE              = 0x00000000,  
   DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |  
                                      DEBUGPROP_INFO_NAME |  
                                      DEBUGPROP_INFO_TYPE |  
                                      DEBUGPROP_INFO_VALUE,  
   DEBUGPROP_INFO_ALL               = 0xffffffff  
};  
```  
  
## <a name="members"></a>成员  
 DEBUGPROP_INFO_FULLNAME  
 初始化/使用`bstrFullName`字段。  
  
 DEBUGPROP_INFO_NAME  
 初始化/使用`bstrName`字段。  
  
 DEBUGPROP_INFO_TYPE  
 初始化/使用`bstrType`字段。  
  
 DEBUGPROP_INFO_VALUE  
 初始化/使用`bstrValue`字段。  
  
 DEBUGPROP_INFO_ATTRIB  
 初始化/使用`dwAttrib`字段。  
  
 DEBUGPROP_INFO_PROP，  
 初始化/用`pProperty`包含的字段[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)接口。  
  
 DEBUGPROP_INFO_VALUE_AUTOEXPAND  
 指定的值字段应包含自动扩展值中，是否可用，此类型的对象。  
  
 DEBUGPROP_INFO_VALUE_NOFUNCEVAL  
 已否决。  
  
 DEBUGPROP_INFO_VALUE_RAW  
 不返回任何非常值或成员 （即，不应格式化值）。  
  
 DEBUGPROP_INFO_VALUE_NO_TOSTRING  
 不返回任何特殊的合成的值 (例如，不要调用`ToString()`某个对象以生成值)。  
  
 DEBUGPROP_INFO_NONE  
 指定未设置任何标志。  
  
 DEBUGPROP_INFO_STANDARD  
 初始化/用`dwAttrib`， `bstrName`， `bstrType`，和`bstrValue`字段。  
  
 DEBUGPROP_INFO_All  
 指示所有标志的掩码。  
  
## <a name="remarks"></a>备注  
 这些值传递给[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)， [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)，并[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)方法，以指示哪些字段是要初始化[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构。  
  
 这些值还可用于`dwFields`的成员`DEBUG_PROPERTY_INFO`结构，用于指示结构的哪些字段是使用，有效时返回该结构。  
  
 可能的按位组合这些值`OR`。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)   
 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)   
 [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)   
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
