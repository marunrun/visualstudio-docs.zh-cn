---
title: IDebugCoreServer2::GetMachineName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetName
helpviewer_keywords:
- IDebugCoreServer2::GetName
ms.assetid: 693bd794-7215-4f07-8651-b57366d39953
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cff51d5cf394c7ff93cc0b0310a69d78a2a6a045
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332345"
---
# <a name="idebugcoreserver2getmachinename"></a>IDebugCoreServer2::GetMachineName
获取核心服务器运行的计算机的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetName( 
   BSTR* pbstrName
);
```

```csharp
int GetName( 
   out string pbstrName
);
```

## <a name="parameters"></a>参数
`pbstrName`\
[out]返回包含计算机的名称的字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)