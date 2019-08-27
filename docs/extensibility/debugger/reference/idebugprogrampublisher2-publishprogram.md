---
title: IDebugProgramPublisher2::PublishProgram | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgram
ms.assetid: 92ff63f0-e869-4040-b3ae-b2c899e708ff
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5d4f0b279bafe5291679237efdaada7907ddc515
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343374"
---
# <a name="idebugprogrampublisher2publishprogram"></a>IDebugProgramPublisher2::PublishProgram
此方法将可用于调试引擎 (DEs) 的程序和会话调试管理器。

## <a name="syntax"></a>语法

```cpp
HRESULT PublishProgram(
   CONST_GUID_ARRAY Engines,
   LPCOLESTR        szFriendlyName,
   IUnknown*        pDebuggeeInterface
);
```

```csharp
int PublishProgram(
   CONST_GUID_ARRAY Engines,
   string           szFriendlyName,
   object           pDebuggeeInterface
);
```

## <a name="parameters"></a>参数
`Engines`\
[in]针对 DEs 的可启动或附加到此程序的 Guid 的数组。

`szFriendlyName`\
[in]（这会显示在菜单或对话框向用户显示） 的程序的友好名称。

`pDebuggeeInterface`\
[in]`IUnknown`程序接口 （此值用作一个 cookie 以唯一标识程序; 此相同的值用于"取消发布"程序）

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 若要使程序不再可用于调试，请调用[UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)。

## <a name="see-also"></a>请参阅
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)