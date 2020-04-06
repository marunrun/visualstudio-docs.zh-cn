---
title: IDebugProgram3：：执行线程 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 201c08352bc5b616298349c52197529ef3f1a7d2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722659"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
执行调试器程序。 返回线程以向调试器提供有关用户在执行程序时正在查看的线程的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT ExecuteOnThread(
   [in] IDebugThread2* pThread)
```

```csharp
int ExecuteOnThread(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>参数
`pThread`\
[在][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 调试器在停止后可以恢复执行的三种不同方式：

- 执行：取消任何上一步，并一直运行到下一个断点等。

- 步骤：取消任何旧步骤，并一直运行到新步骤完成。

- 继续：再次运行，并保留任何旧步骤处于活动状态。

  在决定要取消`ExecuteOnThread`哪个步骤时，传递给的线程非常有用。 如果不知道线程，运行执行将取消所有步骤。 了解线程后，只需取消活动线程上的步骤。

## <a name="see-also"></a>请参阅
- [执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)
- [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)
