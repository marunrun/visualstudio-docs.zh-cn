---
title: COMPUTER_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- COMPUTER_INFO structure
ms.assetid: 943085b2-f165-462d-9a4e-2086f0cdfff4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 55d3eb6c321875b479d8df597b963fc3ac30db12
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346575"
---
# <a name="computerinfo"></a>COMPUTER_INFO
描述在其运行调试器的计算机。

## <a name="syntax"></a>语法

```cpp
typedef struct tagCOMPUTER_INFO
{
    WORD wProcessorArchitecture;
    WORD wSuiteMask;
    DWORD dwOperatingSystemVersion;
} COMPUTER_INFO;
```

```csharp
public struct COMPUTER_INFO
{
    public ushort wProcessorArchitecture;
    public ushort wSuiteMask;
    public uint dwOperatingSystemVersion;
}
```

## <a name="members"></a>成员
`wProcessorArchitecture`\
标识微处理器体系的结构。

`wSuiteMask`\
标识套件掩码。

`dwOperatingSystemVersion`\
操作系统版本号。

## <a name="remarks"></a>备注
返回此结构[GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)方法。

## <a name="requirements"></a>要求
标头：Msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)
