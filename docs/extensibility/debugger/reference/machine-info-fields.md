---
title: MACHINE_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO_FIELDS
helpviewer_keywords:
- MACHINE_INFO_FIELDS enumeration
ms.assetid: 2d61d206-7d40-4df1-8c88-1b3c9c78821e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 79bd733d987511a624235c06b5dbe83206e0c5bd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339349"
---
# <a name="machineinfofields"></a>MACHINE_INFO_FIELDS
指定要检索特定计算机的信息种类。

## <a name="syntax"></a>语法

```cpp
enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
typedef DWORD MACHINE_INFO_FIELDS;
```

```csharp
public enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
```

## <a name="fields"></a>字段
 `MCIF_NAME`\
 初始化/使用`bstrName`结构中的字段。

 `MCIF_FLAGS`\
 初始化/使用`Flags`结构中的字段。

 `MIF_ALL`\
 初始化/使用所有结构中的字段。

## <a name="remarks"></a>备注
 这些值传递给[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)方法，以指示的哪些成员[MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)结构是进行初始化。

 中也使用`Fields`的成员`MACHINE_INFO`结构，用于指示哪些字段是使用，有效。

 可能的按位组合这些标志`OR`。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)