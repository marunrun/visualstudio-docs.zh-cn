---
title: IDebugField::GetExtendedInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetExtendedInfo
helpviewer_keywords:
- IDebugField::GetExtendedInfo method
ms.assetid: 46c0dd4d-4fd5-4efd-a908-71e4248e8e8d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3ddae4ea7ecc58d67279ae638d19bf95ec2cc591
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352646"
---
# <a name="idebugfieldgetextendedinfo"></a>IDebugField::GetExtendedInfo
此方法获取扩展字段的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetExtendedInfo( 
   REFGUID guidExtendedInfo,
   BYTE**  prgBuffer,
   DWORD*  pdwLen
);
```

```csharp
int GetExtendedInfo(
   ref Guid guidExtendedInfo,
   IntPtr[] prgBuffer,
   ref uint pdwLen
);
```

## <a name="parameters"></a>参数
`guidExtendedInfo`\
[in]选择要返回的信息。 有效值为：

|值|描述|
|-----------|-----------------|
|`guidConstantValue`|作为一个字节序列的值。|
|`guidConstantType`|类型签名形式的类型。|

`prgBuffer`\
[out]返回扩展的信息。

`pdwLen`\
[in、 out]以字节为单位返回大小的扩展信息。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 目前，此方法返回类型或常量的值。 调用方必须释放中返回的缓冲区`prgBuffer`通过调用 COM 的`CoTaskMemFree`函数 (C++) 或<xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A>(C#)。

## <a name="see-also"></a>请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)