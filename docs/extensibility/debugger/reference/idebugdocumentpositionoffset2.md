---
title: IDebug文档位置偏移2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2 interface
ms.assetid: f1b05db3-50d8-453f-a72f-e68b239236a4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d967ec9cf406f7dae691c3f05eda514e0907c7e3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731596"
---
# <a name="idebugdocumentpositionoffset2"></a>IDebugDocumentPositionOffset2
将源文件中的位置表示为字符偏移量。

## <a name="syntax"></a>语法

```
IDebugDocumentPositionOffset2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 由 IDE 实现，并由调试引擎使用。

## <a name="methods"></a>方法
 下表显示了 的方法`IDebugDocumentPositionOffset2`。

|方法|描述|
|------------|-----------------|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2-getrange.md)|检索当前文档位置的范围。|

## <a name="remarks"></a>备注
 这将返回与[GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)相同的信息，`char`但从文档开头的偏移量返回。 这呈现的文档就像它存在于磁盘上一样，即一维字符数组，而不是通常返回的行和列信息。

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
