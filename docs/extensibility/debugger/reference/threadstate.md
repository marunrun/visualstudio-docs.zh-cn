---
title: THREADSTATE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADSTATE
helpviewer_keywords:
- THREADSTATE enumeration
ms.assetid: 62efdd7c-25b1-4fd3-9d06-ac1830a418a9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d86baeeab046a7e605979d3af2d6329998f796ba
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72727499"
---
# <a name="threadstate"></a>THREADSTATE
指定线程的状态。

## <a name="syntax"></a>语法

```cpp
enum enum_THREADSTATE { 
   THREADSTATE_RUNNING = 0x0001,
   THREADSTATE_STOPPED = 0x0002,
   THREADSTATE_FRESH   = 0x0003,
   THREADSTATE_DEAD    = 0x0004,
   THREADSTATE_FROZEN  = 0x0005
};
typedef DWORD THREADSTATE;
```

```csharp
public enum enum_THREADSTATE { 
   THREADSTATE_RUNNING = 0x0001,
   THREADSTATE_STOPPED = 0x0002,
   THREADSTATE_FRESH   = 0x0003,
   THREADSTATE_DEAD    = 0x0004,
   THREADSTATE_FROZEN  = 0x0005
};
```

## <a name="fields"></a>字段
 `THREADSTATE_RUNNING`\
 指示线程正在运行。

 `THREADSTATE_STOPPED`\
 指示由于断点而停止线程。

 `THREADSTATE_FRESH`\
 指示线程已创建但尚未运行代码。

 `THREADSTATE_DEAD`\
 指示线程已死。

 `THREADSTATE_FROZEN`\
 指示线程已冻结（无法执行任何执行）。

## <a name="remarks"></a>备注
 用于[THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)结构的 `dwThreadState` 字段。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： VisualStudio。

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)