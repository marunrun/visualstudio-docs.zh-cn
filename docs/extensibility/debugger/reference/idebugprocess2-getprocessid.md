---
title: IDebugProcess2::GetProcessId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetProcessId
helpviewer_keywords:
- IDebugProcess2::GetProcessId
ms.assetid: d5b6f03c-d49d-4b83-b072-016ac3124f5f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b1759563f9f379a878f987662df2cd380ec0532c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309507"
---
# <a name="idebugprocess2getprocessid"></a>IDebugProcess2::GetProcessId
此过程中获取的 GUID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProcessId(
   GUID* pguidProcessId
);
```

```csharp
int GetProcessId(
   out Guid pguidProcessId
);
```

## <a name="parameters"></a>参数
`pguidProcessId`\
[out]返回此进程的 GUID。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 全局唯一标识符 (GUID) 标识此过程从系统中运行的所有其他进程。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)