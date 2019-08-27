---
title: IDebugProgram2::GetENCUpdate | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetENCUpdate
helpviewer_keywords:
- IDebugProgram2::GetENCUpdate
ms.assetid: 9832aac8-6320-4fd8-91dd-2a0852febb00
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: eb92e7076c308663ddf9ec760d1f2276affd0c87
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66320840"
---
# <a name="idebugprogram2getencupdate"></a>IDebugProgram2::GetENCUpdate
此方法获取此程序的编辑并继续 (ENC) 更新。 自定义调试引擎始终返回`E_NOTIMPL`。

## <a name="syntax"></a>语法

```cpp
HRESULT GetENCUpdate( 
   IUnknown** ppUpdate
);
```

```csharp
int GetENCUpdate(
   out object ppUpdate
);
```

## <a name="parameters"></a>参数
`ppUpdate`\
[out]返回可用于更新此程序的内部接口。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

> [!NOTE]
> 自定义调试引擎应始终返回`E_NOTIMPL`。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)