---
title: IDebugCustomAttributeQuery2::GetCustomAttributeByName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
helpviewer_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
ms.assetid: 7428dfeb-8929-41b2-9b99-cb343a86c02d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7d874a00c3c82108c224f18922f2b4853279beaa
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322206"
---
# <a name="idebugcustomattributequery2getcustomattributebyname"></a>IDebugCustomAttributeQuery2::GetCustomAttributeByName
获取给定名称的自定义特性的自定义特性字节。

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
[in]包含要查找的自定义特性的名称的字符串。

`ppBlob`\
[in、 out]使用自定义特性字节填充的数组。

`pdwLen`\
[in、 out]指定要在中返回的字节的最大数`ppBlob`数组并返回实际写入到的数组的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK 或如果自定义特性不存在，则返回 S_FALSE。 否则，返回错误代码。

## <a name="remarks"></a>备注
 设置`ppBlob`参数为 null 值，以返回的数属性的可用字节。 然后分配一个数组，并将为该数组中的传递`ppBlob`参数。

 属性字节表示的原始数据的自定义属性。

 如果`ppBlob`和`pdwLen`参数设置为 null 值，可以使用此方法以确定是否只是存在自定义属性。 但是，更轻松的替代方法是调用[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)