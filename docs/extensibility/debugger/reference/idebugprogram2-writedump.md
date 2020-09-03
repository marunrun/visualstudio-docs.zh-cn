---
title: IDebugProgram2：： WriteDump |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722735"
---
# <a name="idebugprogram2writedump"></a>IDebugProgram2::WriteDump
向文件写入转储。

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
中 [DUMPTYPE](../../../extensibility/debugger/reference/dumptype.md) 枚举中的一个值，该值指定转储的类型，例如，short 或 long。

`pszDumpUrl`\
中要将转储写入到的 URL。 通常，此格式为 `file://c:\path\filename.ext` ，但可以是任何有效的 URL。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 程序转储通常包括当前堆栈帧、堆栈本身、在程序中运行的线程列表，以及程序拥有的任何内存。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
