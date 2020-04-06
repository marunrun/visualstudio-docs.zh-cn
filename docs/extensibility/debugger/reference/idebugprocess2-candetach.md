---
title: IDebugProcess2：：可以分离 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::CanDetach
helpviewer_keywords:
- IDebugProcess2::CanDetach
ms.assetid: 2830f7c3-69fb-474a-97b8-5b869e38d546
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2bfb7b7b586f9c8b86e75d453389525c61a63bc4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724174"
---
# <a name="idebugprocess2candetach"></a>IDebugProcess2::CanDetach
确定会话调试管理器 （SDM） 是否可以分离进程。

## <a name="syntax"></a>语法

```cpp
HRESULT CanDetach(
   void
);
```

```csharp
int CanDetach();
```

## <a name="return-value"></a>返回值
 如果成功，如果`S_OK.`调试`S_FALSE`器无法从进程分离，则返回。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
