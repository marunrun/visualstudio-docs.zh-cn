---
title: IDebug自定义属性查询2：：获取按名称获取自定义属性 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
helpviewer_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
ms.assetid: 7428dfeb-8929-41b2-9b99-cb343a86c02d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 47471f2743e705b06fb9a1bda6752b24a7836d1b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732561"
---
# <a name="idebugcustomattributequery2getcustomattributebyname"></a>IDebugCustomAttributeQuery2::GetCustomAttributeByName
获取给定自定义属性名称的自定义属性字节。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCustomAttributeByName( 
   LPCOLESTR pszCustomAttributeName,
   BYTE*     ppBlob,
   DWORD*    pdwLen
);
```

```csharp
int GetCustomAttributeByName(
   [In] string        pszCustomAttributeName,
   [In, Out] byte[]   ppBlob,
   [In, Out] ref uint pdwLen
);
```

## <a name="parameters"></a>参数
`pszCustomAttributeName`\
[在]包含要查找的自定义属性的名称的字符串。

`ppBlob`\
[进出]使用自定义属性字节填充的数组。

`pdwLen`\
[进出]指定要在`ppBlob`数组中返回的最大字节数，并返回实际写入数组的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK或返回S_FALSE自定义属性不存在。 否则，返回错误代码。

## <a name="remarks"></a>备注
 将`ppBlob`参数设置为空值以返回可用属性字节数。 然后分配一个数组，并将该数组传递给该`ppBlob`参数。

 属性字节表示自定义属性的原始数据。

 如果`ppBlob`和`pdwLen`参数设置为 null 值，则此方法可用于确定自定义属性是否仅存在。 但是，一个更简单的替代方法是调用[IsCustom属性定义](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)
