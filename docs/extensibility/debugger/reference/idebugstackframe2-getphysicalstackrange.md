---
title: IDebugStackFrame2::GetPhysicalStackRange | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
helpviewer_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
ms.assetid: 2f6992e2-ac1c-433f-83b7-a7f83a4ce63d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2cf0db9fa776116f1536ae137444160385a8b6a1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347717"
---
# <a name="idebugstackframe2getphysicalstackrange"></a>IDebugStackFrame2::GetPhysicalStackRange
获取依赖于计算机的形式，与堆栈帧关联的物理地址的范围。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPhysicalStackRange ( 
   UINT64* paddrMin,
   UINT64* paddrMax
);
```

```csharp
int GetPhysicalStackRange ( 
   out ulong paddrMin,
   out ulong paddrMax
);
```

## <a name="parameters"></a>参数
`paddrMin`\
[out]返回与此堆栈帧关联的最小物理地址。

`paddrMax`\
[out]返回与此堆栈帧关联的最高的物理地址。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 会话调试管理器 (SDM) 使用此方法返回的信息进行排序堆栈帧。

 假定，调用堆栈向下增长，也就是说，新堆栈帧添加越来越多地较低的内存地址。 运行时体系结构必须提供匹配这一假设的物理堆栈范围。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)