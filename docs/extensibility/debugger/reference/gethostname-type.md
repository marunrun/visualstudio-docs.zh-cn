---
title: GETHOSTNAME_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- GETHOSTNAME_TYPE
helpviewer_keywords:
- GETHOSTNAME_TYPE enumeration
ms.assetid: 2be92bea-8133-412b-9015-1833baf16e1b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 799b7e67248759987a3e3f9595978fb1a7bbf87d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317598"
---
# <a name="gethostnametype"></a>GETHOSTNAME_TYPE
指定主机名的类型。

## <a name="syntax"></a>语法

```cpp
enum enum_GETHOSTNAME_TYPE {
    GHN_FRIENDLY_NAME = 0,
    GHN_FILE_NAME     = 1
};
typedef DWORD GETHOSTNAME_TYPE;
```

```csharp
public enum enum_GETHOSTNAME_TYPE {
    GHN_FRIENDLY_NAME = 0,
    GHN_FILE_NAME     = 1
};
```

## <a name="fields"></a>字段
`GHN_FRIENDLY_NAME`\
指定的主机的友好名称。

`GHN_FILE_NAME`\
指定主机的文件名称。

## <a name="remarks"></a>备注
这些值会作为参数传递[GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)方法来检索主机名以不同的格式。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
