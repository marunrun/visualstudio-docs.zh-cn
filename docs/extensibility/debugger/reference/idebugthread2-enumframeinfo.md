---
title: IDebugThread2::EnumFrameInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::EnumFrameInfo
helpviewer_keywords:
- IDebugThread2::EnumFrameInfo
ms.assetid: 17914a71-10ea-4b6f-8982-e364f87dca53
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fad77ca1d649e7ffdda02c7145dc11666619f232
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66320318"
---
# <a name="idebugthread2enumframeinfo"></a>IDebugThread2::EnumFrameInfo
检索此线程的堆栈帧的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumFrameInfo ( 
   FRAMEINFO_FLAGS        dwFieldSpec,
   UINT                   nRadix,
   IEnumDebugFrameInfo2** ppEnum
);
```

```csharp
int EnumFrameInfo ( 
   enum_FRAMEINFO_FLAGS     dwFieldSpec,
   uint                     nRadix,
   out IEnumDebugFrameInfo2 ppEnum
);
```

## <a name="parameters"></a>参数
`dwFieldSpec`\
[in]中的标志的组合[FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)枚举，用于指定的哪些字段[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构是要填写。指定`FIF_FUNCNAME_FORMAT`标志设置为一个字符串的格式的函数名称。

`nRadix`\
[in]设置格式的枚举数中的数字信息时使用的基数。

`ppEnum`\
[out]返回[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)对象，其中包含一系列[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构描述的堆栈帧。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 使用第一次枚举的当前帧和上一次枚举的最早帧中顺序，列举了线程的帧。

## <a name="see-also"></a>请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)