---
title: IDebugExceptionEvent2::GetExceptionDescription | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::GetExceptionDescription
helpviewer_keywords:
- IDebugExceptionEvent2::GetExceptionDescription
ms.assetid: d07d458f-5729-47e4-9b77-1bd59c61a75a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cc13184328ce3a7cf09e6df20ee62162cb108b5b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310544"
---
# <a name="idebugexceptionevent2getexceptiondescription"></a>IDebugExceptionEvent2::GetExceptionDescription
获取可显示异常的说明。

## <a name="syntax"></a>语法

```cpp
HRESULT GetExceptionDescription( 
   BSTR* pbstrDescription
);
```

```csharp
int GetExceptionDescription( 
   out string pbstrDescription
);
```

## <a name="parameters"></a>参数
`pbstrDescription`\
[out]返回可显示异常的说明。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的字符串通常是异常的名称和中所示**输出**窗口时出现异常。

## <a name="see-also"></a>请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)