---
title: AD_PROCESS_ID_TYPE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AD_PROCESS_ID_TYPE
helpviewer_keywords:
- AD_PROCESS_ID_TYPE enumeration
ms.assetid: 0aab80e9-285a-4697-94ac-c864d42a6aaa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a88fbe97cede8d343f1a96bc1917a69b8905b02b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738189"
---
# <a name="ad_process_id_type"></a>AD_PROCESS_ID_TYPE
指定如何在[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构中解释进程 ID。

## <a name="syntax"></a>语法

```cpp
enum enum_AD_PROCESS_ID {
    AD_PROCESS_ID_SYSTEM = 0,
    AD_PROCESS_ID_GUID   = 1
};
typedef DWORD AD_PROCESS_ID_TYPE;
```

```csharp
public enum enum_AD_PROCESS_ID {
    AD_PROCESS_ID_SYSTEM = 0,
    AD_PROCESS_ID_GUID   = 1
};
```

## <a name="fields"></a>字段
`AD_PROCESS_ID_SYSTEM`\
进程 ID 是系统标识符。 使用AD_PROCESS_ID`ProcessId.dwProcessId`结构的字段[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)。

`AD_PROCESS_ID_GUID`\
进程 ID 是 GUID。 `ProcessId.guidProcessId`使用结构字段`AD_PROCESS_ID`。

## <a name="remarks"></a>备注
用于AD_PROCESS_ID结构`ProcessIdType`的成员，用于[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)标识结构中包含的进程 ID 的类型。 确定如何解释结构中的`ProcessId`联合。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
