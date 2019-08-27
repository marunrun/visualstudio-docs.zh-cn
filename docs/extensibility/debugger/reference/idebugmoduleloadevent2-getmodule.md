---
title: IDebugModuleLoadEvent2::GetModule | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModuleLoadEvent2::GetModule
helpviewer_keywords:
- IDebugModuleLoadEvent2::GetModule
ms.assetid: c86482bb-9ce5-4e63-bbe0-969b50169424
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6ee91686051440fe44efd1f4e4f9ba933f3e0c99
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323704"
---
# <a name="idebugmoduleloadevent2getmodule"></a>IDebugModuleLoadEvent2::GetModule
获取正在的模块加载或卸载。

## <a name="syntax"></a>语法

```cpp
HRESULT GetModule( 
   IDebugModule2** pModule,
   BSTR*           pbstrDebugMessage,
   BOOL*           pbLoad
);
```

```csharp
int GetModule( 
   out IDebugModule2 pModule,
   ref string        pbstrDebugMessage,
   ref int           pbLoad
);
```

## <a name="parameters"></a>参数
`pModule`\
[out]返回[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)对象，表示加载或卸载的模块。

`pbstrDebugMessage`\
[in、 out]返回描述此事件的可选消息。 如果此参数为 null 值，被不请求的任何消息。

`pbLoad`\
[in、 out]非零值 (`TRUE`) 如果模块加载和零 (`FALSE`) 如果正在卸载模块。 如果此参数为 null 值，无状态请求。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)