---
title: IDebugProgram3::ExecuteOnThread | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 798a0caca394a21d6ee12a99efeacb2f27f6969c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343607"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
执行调试程序。 线程将返回以授予用户查看哪个线程执行程序时的调试程序信息。

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
[in][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 有三种不同方法，调试器可以恢复后停止执行：

- 执行：取消任何上一步骤中，并运行到下一个断点，依此类推。

- 步骤：取消任何旧的步骤，并运行，直到新的步骤完成。

- 继续：再次运行，并保留任何旧步骤活动。

  在线程传递给`ExecuteOnThread`决定哪个步骤取消时很有用。 如果不知道运行的线程，执行将取消所有步骤。 线程的信息后，只需取消对活动线程的步骤。

## <a name="see-also"></a>请参阅
- [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)
- [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)