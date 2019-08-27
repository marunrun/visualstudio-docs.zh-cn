---
title: IDebugProcess2::GetAttachedSessionName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetAttachedSessionName
helpviewer_keywords:
- IDebugProcess2::GetAttachedSessionName
ms.assetid: 7e5e116f-2c0c-4bc8-ad3f-e9fd2318a7e4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1d14e76e576aaf3e467ab24083d445c9d9fc5214
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353154"
---
# <a name="idebugprocess2getattachedsessionname"></a>IDebugProcess2::GetAttachedSessionName
获取正在调试此进程的会话的名称。 IDE 可以调试特定计算机上的特定进程的用户显示此信息。

> [!NOTE]
> 此方法已弃用，并且它的实现应始终返回`E_NOTIMPL`。

## <a name="syntax"></a>语法

```
HRESULT GetAttachedSessionName(
   BSTR* pbstrSessionName
);
```

## <a name="parameters"></a>参数
`pbstrSessionName`\

## <a name="return-value"></a>返回值
 此方法应始终返回`E_NOTIMPL`。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)