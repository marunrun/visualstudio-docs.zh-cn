---
title: DEBUGPROP_INFO_FLAGS |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68143001"
---
# <a name="debugprop_info_flags"></a>DEBUGPROP_INFO_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要检索的有关调试属性对象的信息。  
  
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
 初始化/使用 `bstrFullName` 字段。  
  
 DEBUGPROP_INFO_NAME  
 初始化/使用 `bstrName` 字段。  
  
 DEBUGPROP_INFO_TYPE  
 初始化/使用 `bstrType` 字段。  
  
 DEBUGPROP_INFO_VALUE  
 初始化/使用 `bstrValue` 字段。  
  
 DEBUGPROP_INFO_ATTRIB  
 初始化/使用 `dwAttrib` 字段。  
  
 DEBUGPROP_INFO_PROP，  
 初始化/使用 `pProperty` 包含 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 接口的字段。  
  
 DEBUGPROP_INFO_VALUE_AUTOEXPAND  
 指定值字段应包含此类型的对象的自动扩展值（如果可用）。  
  
 DEBUGPROP_INFO_VALUE_NOFUNCEVAL  
 已否决。  
  
 DEBUGPROP_INFO_VALUE_RAW  
 不要返回任何 beautified 值或成员 (即，不要) 设置值的格式。  
  
 DEBUGPROP_INFO_VALUE_NO_TOSTRING  
 不要返回任何特殊的合成值 (例如，不要对对象调用 `ToString()` 以生成值) 。  
  
 DEBUGPROP_INFO_NONE  
 指定不设置任何标志。  
  
 DEBUGPROP_INFO_STANDARD  
 初始化/使用 `dwAttrib` 、 `bstrName` 、 `bstrType` 和 `bstrValue` 字段。  
  
 DEBUGPROP_INFO_All  
 指示所有标志的掩码。  
  
## <a name="remarks"></a>备注  
 这些值将传递到 [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)、 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)和 [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md) 方法，以指示要 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构初始化哪些字段。  
  
 这些值还用于 `dwFields` 结构的成员 `DEBUG_PROPERTY_INFO` ，以指示在返回结构时使用的结构字段和有效字段。  
  
 这些值可以与按位组合 `OR` 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)   
 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)   
 [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)   
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
