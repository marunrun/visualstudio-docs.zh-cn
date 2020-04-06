---
title: IDebugEvent2：：获取属性 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2::GetAttributes
helpviewer_keywords:
- IDebugEvent2::GetAttributes
ms.assetid: 2ac5b5fb-da17-43f7-811a-313f677e60d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ffc3fc1b7988401611190fdf09e8041bf0dc5b1a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729953"
---
# <a name="idebugevent2getattributes"></a>IDebugEvent2::GetAttributes
获取此调试事件的属性。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAttribute( 
   DWORD* pdwAttrib
);
```

```csharp
int GetAttribute( 
   out uint pdwAttrib
);
```

## <a name="parameters"></a>参数
`pdwAttrib`\
[出][事件属性](../../../extensibility/debugger/reference/eventattributes.md)枚举中标志的组合。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口是所有事件所共有的。 此方法描述事件的类型;例如，事件是同步事件或异步事件，它是停止事件。

## <a name="see-also"></a>请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
