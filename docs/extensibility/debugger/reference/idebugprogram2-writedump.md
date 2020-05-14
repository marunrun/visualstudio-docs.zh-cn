---
title: IDebugProgram2：：写入转储 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::WriteDump
helpviewer_keywords:
- IDebugProgram2::WriteDump
ms.assetid: 375afb8c-882d-44db-bfa7-e2c9eb555122
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 333535a727d88f66346ba4c94cb08b4917b8acfd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722735"
---
# <a name="idebugprogram2writedump"></a>IDebugProgram2::WriteDump
将转储写入文件。

## <a name="syntax"></a>语法

```cpp
HRESULT WriteDump( 
   DUMPTYPE  DumpType,
   LPCOLESTR pszDumpUrl
);
```

```csharp
int WriteDump( 
   enum_DUMPTYPE  DumpType,
   string         pszDumpUrl
);
```

## <a name="parameters"></a>参数
`DumpType`\
[在][DUMPTYPE](../../../extensibility/debugger/reference/dumptype.md)枚举中指定转储类型的值，例如，短转储或长转储类型。

`pszDumpUrl`\
[在]要将转储写入的 URL。 通常，这是以 的形式`file://c:\path\filename.ext`，但可以是任何有效的 URL。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 程序转储通常包括当前堆栈帧、堆栈本身、程序中正在运行的线程的列表，以及程序拥有的任何内存。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
