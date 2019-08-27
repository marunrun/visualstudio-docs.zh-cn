---
title: DBG_ATTRIB_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DBG_ATTRIB_FLAGS
helpviewer_keywords:
- DBGPROP_ATTRIB_FLAGS enumerations
ms.assetid: 2f13e601-dadc-476e-a8ec-01c4515082e7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fde7ac384a6b2de293fc9baf0075438c9c609236
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346300"
---
# <a name="dbgattribflags"></a>DBG_ATTRIB_FLAGS
描述各种特性[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)或[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)接口。 成员[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构。

## <a name="syntax"></a>语法

```cpp
#define DBG_ATTRIB_NONE                 0x0000000000000000,
#define DBG_ATTRIB_ALL                  0x00000000ffffffff,

// Attributes about the object itself

#define DBG_ATTRIB_OBJ_IS_EXPANDABLE    0x0000000000000001,
#define DBG_ATTRIB_OBJ_HAS_ID           0x0000000000000002,
#define DBG_ATTRIB_OBJ_CAN_HAVE_ID      0x0000000000000004,

// Attributes about the value of the object

#define DBG_ATTRIB_VALUE_READONLY       0x0000000000000010,
#define DBG_ATTRIB_VALUE_ERROR          0x0000000000000020,
#define DBG_ATTRIB_VALUE_SIDE_EFFECT    0x0000000000000040,
#define DBG_ATTRIB_OVERLOADED_CONTAINER 0x0000000000000080,
#define DBG_ATTRIB_VALUE_BOOLEAN        0x0000000000000100,
#define DBG_ATTRIB_VALUE_BOOLEAN_TRUE   0x0000000000000200,
#define DBG_ATTRIB_VALUE_INVALID        0x0000000000000400,
#define DBG_ATTRIB_VALUE_NAT            0x0000000000000800,
#define DBG_ATTRIB_VALUE_AUTOEXPANDED   0x0000000000001000,
#define DBG_ATTRIB_VALUE_TIMEOUT        0x0000000000002000,
#define DBG_ATTRIB_VALUE_RAW_STRING     0x0000000000004000,
#define DBG_ATTRIB_VALUE_CUSTOM_VIEWER  0x0000000000008000,

// Attributes about field access types for the object

#define DBG_ATTRIB_ACCESS_NONE          0x0000000000010000,
#define DBG_ATTRIB_ACCESS_PUBLIC        0x0000000000020000,
#define DBG_ATTRIB_ACCESS_PRIVATE       0x0000000000040000,
#define DBG_ATTRIB_ACCESS_PROTECTED     0x0000000000080000,
#define DBG_ATTRIB_ACCESS_FINAL         0x0000000000100000,
#define DBG_ATTRIB_ACCESS_ALL           0x00000000001f0000,

// Attributes for the storage types of the object

#define DBG_ATTRIB_STORAGE_NONE         0x0000000001000000,
#define DBG_ATTRIB_STORAGE_GLOBAL       0x0000000002000000,
#define DBG_ATTRIB_STORAGE_STATIC       0x0000000004000000,
#define DBG_ATTRIB_STORAGE_REGISTER     0x0000000008000000,
#define DBG_ATTRIB_STORAGE_ALL          0x000000000f000000,

// Attributes for the type modifiers on the object

#define DBG_ATTRIB_TYPE_NONE            0x0000000100000000,
#define DBG_ATTRIB_TYPE_VIRTUAL         0x0000000200000000,
#define DBG_ATTRIB_TYPE_CONSTANT        0x0000000400000000,
#define DBG_ATTRIB_TYPE_SYNCHRONIZED    0x0000000800000000,
#define DBG_ATTRIB_TYPE_VOLATILE        0x0000001000000000,
#define DBG_ATTRIB_TYPE_ALL             0x0000001f00000000,

// Attributes that describe the type of object

#define DBG_ATTRIB_DATA                 0x0000010000000000,
#define DBG_ATTRIB_METHOD               0x0000020000000000,
#define DBG_ATTRIB_PROPERTY             0x0000040000000000,
#define DBG_ATTRIB_CLASS                0x0000080000000000,
#define DBG_ATTRIB_BASECLASS            0x0000100000000000,
#define DBG_ATTRIB_INTERFACE            0x0000200000000000,
#define DBG_ATTRIB_INNERCLASS           0x0000400000000000,
#define DBG_ATTRIB_MOSTDERIVED          0x0000800000000000,
#define DBG_ATTRIB_CHILD_ALL            0x0000ff0000000000,

// Miscellaneous attributes

#define DBG_ATTRIB_MULTI_CUSTOM_VIEWERS 0x0001000000000000

typedef UINT64 DBG_ATTRIB_FLAGS;
```

```csharp
public const int DBG_ATTRIB_NONE                 = 0x0000000000000000,
public const int DBG_ATTRIB_ALL                  = 0x00000000ffffffff,

// Attributes about the object itself

public const int DBG_ATTRIB_OBJ_IS_EXPANDABLE    = 0x0000000000000001,
public const int DBG_ATTRIB_OBJ_HAS_ID           = 0x0000000000000002,
public const int DBG_ATTRIB_OBJ_CAN_HAVE_ID      = 0x0000000000000004,

// Attributes about the value of the object

public const int DBG_ATTRIB_VALUE_READONLY       = 0x0000000000000010,
public const int DBG_ATTRIB_VALUE_ERROR          = 0x0000000000000020,
public const int DBG_ATTRIB_VALUE_SIDE_EFFECT    = 0x0000000000000040,
public const int DBG_ATTRIB_OVERLOADED_CONTAINER = 0x0000000000000080,
public const int DBG_ATTRIB_VALUE_BOOLEAN        = 0x0000000000000100,
public const int DBG_ATTRIB_VALUE_BOOLEAN_TRUE   = 0x0000000000000200,
public const int DBG_ATTRIB_VALUE_INVALID        = 0x0000000000000400,
public const int DBG_ATTRIB_VALUE_NAT            = 0x0000000000000800,
public const int DBG_ATTRIB_VALUE_AUTOEXPANDED   = 0x0000000000001000,
public const int DBG_ATTRIB_VALUE_TIMEOUT        = 0x0000000000002000,
public const int DBG_ATTRIB_VALUE_RAW_STRING     = 0x0000000000004000,
public const int DBG_ATTRIB_VALUE_CUSTOM_VIEWER  = 0x0000000000008000,

// Attributes about field access types for the object

public const int DBG_ATTRIB_ACCESS_NONE          = 0x0000000000010000,
public const int DBG_ATTRIB_ACCESS_PUBLIC        = 0x0000000000020000,
public const int DBG_ATTRIB_ACCESS_PRIVATE       = 0x0000000000040000,
public const int DBG_ATTRIB_ACCESS_PROTECTED     = 0x0000000000080000,
public const int DBG_ATTRIB_ACCESS_FINAL         = 0x0000000000100000,
public const int DBG_ATTRIB_ACCESS_ALL           = 0x00000000001f0000,

// Attributes for the storage types of the object

public const int DBG_ATTRIB_STORAGE_NONE         = 0x0000000001000000,
public const int DBG_ATTRIB_STORAGE_GLOBAL       = 0x0000000002000000,
public const int DBG_ATTRIB_STORAGE_STATIC       = 0x0000000004000000,
public const int DBG_ATTRIB_STORAGE_REGISTER     = 0x0000000008000000,
public const int DBG_ATTRIB_STORAGE_ALL          = 0x000000000f000000,

// Attributes for the type modifiers on the object

public const int DBG_ATTRIB_TYPE_NONE            = 0x0000000100000000,
public const int DBG_ATTRIB_TYPE_VIRTUAL         = 0x0000000200000000,
public const int DBG_ATTRIB_TYPE_CONSTANT        = 0x0000000400000000,
public const int DBG_ATTRIB_TYPE_SYNCHRONIZED    = 0x0000000800000000,
public const int DBG_ATTRIB_TYPE_VOLATILE        = 0x0000001000000000,
public const int DBG_ATTRIB_TYPE_ALL             = 0x0000001f00000000,

// Attributes that describe the type of object

public const int DBG_ATTRIB_DATA                 = 0x0000010000000000,
public const int DBG_ATTRIB_METHOD               = 0x0000020000000000,
public const int DBG_ATTRIB_PROPERTY             = 0x0000040000000000,
public const int DBG_ATTRIB_CLASS                = 0x0000080000000000,
public const int DBG_ATTRIB_BASECLASS            = 0x0000100000000000,
public const int DBG_ATTRIB_INTERFACE            = 0x0000200000000000,
public const int DBG_ATTRIB_INNERCLASS           = 0x0000400000000000,
public const int DBG_ATTRIB_MOSTDERIVED          = 0x0000800000000000,
public const int DBG_ATTRIB_CHILD_ALL            = 0x0000ff0000000000,

// Miscellaneous attributes

public const int DBG_ATTRIB_MULTI_CUSTOM_VIEWERS = 0x0001000000000000
```

## <a name="members"></a>成员
 `DBG_ATTRIB_NONE`\
 表示没有特性。

 `DBG_ATTRIB_ALL`\
 指示所有属性。

 `DBG_ATTRIB_OBJ_IS_EXPANDABLE`\
 表示引用或属性具有子级。

 `DBG_ATTRIB_OBJ_HAS_ID`\
 指示已创建此对象的 ID。

 `DBG_ATTRIB_OBJ_CAN_HAVE_ID`\
 指示可以创建此对象的 ID。

 `DBG_ATTRIB_VALUE_READONLY`\
 表示值是只读的。

 `DBG_ATTRIB_VALUE_ERROR`\
 指示值错误。

 `DBG_ATTRIB_VALUE_SIDE_EFFECT`\
 指示计算具有副作用。

 `DBG_ATTRIB_OVERLOADED_CONTAINER`\
 指示此属性实际上是重载的容器。

 `DBG_ATTRIB_VALUE_BOOLEAN`\
 指示在值`DEBUG_PROPERTY_INFO::bstrValue`是布尔值。

 `DBG_ATTRIB_VALUE_BOOLEAN_TRUE`\
 指示中的值`DEBUG_PROPERTY_INFO::bstrValue`是一个布尔值和`TRUE`。

 `DBG_ATTRIB_VALUE_INVALID`\
 表示 `DEBUG_PROPERTY_INFO::bstrValue` 中的值无效。

 `DBG_ATTRIB_VALUE_NAT`\
 指示中的值`DEBUG_PROPERTY_INFO::bstrValue`是"*不是一件事情*"(NAT)。 NAT 介绍 Intel 64 位处理器指示延迟推理异常的寄存器标志。

 `DBG_ATTRIB_VALUE_AUTOEXPANDED`\
 指示在值`DEBUG_PROPERTY_INFO::bstrValue`可能已自动扩展。

 `DBG_ATTRIB_VALUE_TIMEOUT`\
 指示，评估已超时。

 `DBG_ATTRIB_VALUE_RAW_STRING`\
 指示在值`DEBUG_PROPERTY_INFO::bstrValue`可以由原始字符串。

 `DBG_ATTRIB_VALUE_CUSTOM_VIEWER`\
 指示此属性具有与之关联的至少一个自定义查看器。

 `DBG_ATTRIB_ACCESS_NONE`\
 指示一个对象，既没有`public`， `private`，也不`protected`类型访问。

 `DBG_ATTRIB_ACCESS_PUBLIC`\
 表示对象具有公共访问。

 `DBG_ATTRIB_ACCESS_PRIVATE`\
 表示对象具有私有访问。

 `DBG_ATTRIB_ACCESS_PROTECTED`\
 表示对象具有受保护的访问。

 `DBG_ATTRIB_ACCESS_FINAL`\
 表示对象具有最终访问。

 `DBG_ATTRIB_ACCESS_ALL`\
 掩码中提取的访问特性从`DBG_ATTRIB_FLAGS`。

 `DBG_ATTRIB_STORAGE_NONE`\
 指示不存在指定的存储类型。

 `DBG_ATTRIB_STORAGE_GLOBAL`\
 表示全局存储。

 `DBG_ATTRIB_STORAGE_STATIC`\
 表示静态存储。

 `DBG_ATTRIB_STORAGE_REGISTER`\
 表示存储在寄存器中。

 `DBG_ATTRIB_STORAGE_ALL`\
 掩码中提取的存储属性`DBG_ATTRIB_FLAGS`。

 `DBG_ATTRIB_TYPE_NONE`\
 指示没有类型修饰符。

 `DBG_ATTRIB_TYPE_VIRTUAL`\
 指示对象的类型为虚拟。

 `DBG_ATTRIB_TYPE_CONSTANT`\
 表示对象的类型是常量。

 `DBG_ATTRIB_TYPE_SYNCHRONIZED`\
 指示同步的对象的类型。

 `DBG_ATTRIB_TYPE_VOLATILE`\
 指示对象的类型是易失性。

 `DBG_ATTRIB_TYPE_ALL`\
 掩码中提取的类型属性`DBG_ATTRIB_FLAGS`。

 `DBG_ATTRIB_DATA`\
 指示此对象为数据字段。

 `DBG_ATTRIB_METHOD`\
 指示此对象是一种方法。

 `DBG_ATTRIB_PROPERTY`\
 指示此对象是一个属性。

 `DBG_ATTRIB_CLASS`\
 指示此对象是一个类。

 `DBG_ATTRIB_BASECLASS`\
 指示此对象的基类。

 `DBG_ATTRIB_INTERFACE`\
 指示此对象是一个接口。

 `DBG_ATTRIB_INNERCLASS`\
 指示此对象是一个内部类。

 `DBG_ATTRIB_MOSTDERIVED`\
 指示此对象为*派生程度最高*。 术语"*派生程度最高*"意味着该对象的实际类型而非其引用的类型。

 `DBG_ATTRIB_CHILD_ALL`\
 指示的掩码`DBG_ATTRIB_DATA`通过`DBG_ATTRIB_MOSTDERIVED`。

 `DBG_ATTRIB_MULTI_CUSTOM_VIEWERS`\
 指示该对象具有与之关联的多个自定义查看器。

## <a name="remarks"></a>备注

> [!NOTE]
> 实际的程序集的 C# 中未定义此枚举中的值。 相反，您必须将定义复制到您的源文件。

 这些标志也用于筛选对象，例如的子级时作为参数传递[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)。 可能的按位组合值`OR`。

 `DBG_ATTRIB_VALUE_CUSTOM_VIEWER`标志，则为表示[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]来获取[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)从接口[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)接口并调用[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)有关自定义查看器的列表。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)