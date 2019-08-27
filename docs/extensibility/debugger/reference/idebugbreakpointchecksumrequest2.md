---
title: IDebugBreakpointChecksumRequest2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBreakpointChecksumRequest2 interface
ms.assetid: 9cfdbca5-052c-48e9-8411-e2e9e4065d00
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: edfcb7d1603160c2f857508c3dd32ce0696b6d7f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352990"
---
# <a name="idebugbreakpointchecksumrequest2"></a>IDebugBreakpointChecksumRequest2
表示断点请求的文档校验和。

## <a name="syntax"></a>语法

```
IDebugBreakpointChecksumRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 实现的[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试包和已使用的调试引擎。

## <a name="methods"></a>方法
 下表显示的方法`IDebugBreakpointChecksumRequest2`。

|方法|描述|
|------------|-----------------|
|[GetChecksum](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-getchecksum.md)|检索给定的校验和算法的唯一标识符的断点请求使用的文档校验和。|
|[IsChecksumEnabled](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-ischecksumenabled.md)|确定是否为本文档中启用了校验和。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll