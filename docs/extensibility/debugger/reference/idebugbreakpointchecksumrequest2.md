---
title: IDebug 突破点检查和请求2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBreakpointChecksumRequest2 interface
ms.assetid: 9cfdbca5-052c-48e9-8411-e2e9e4065d00
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 632c3611f6c03a47a7d46e985eb6aa2685864a7f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735125"
---
# <a name="idebugbreakpointchecksumrequest2"></a>IDebugBreakpointChecksumRequest2
表示断点请求的文档校验和。

## <a name="syntax"></a>语法

```
IDebugBreakpointChecksumRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 由[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试包实现，由调试引擎使用。

## <a name="methods"></a>方法
 下表显示了 的方法`IDebugBreakpointChecksumRequest2`。

|方法|描述|
|------------|-----------------|
|[GetChecksum](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-getchecksum.md)|检索断点请求的文档校验和，给定要使用的校验和算法的唯一标识符。|
|[IsChecksumEnabled](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-ischecksumenabled.md)|确定是否为此文档启用了校验和。|

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
