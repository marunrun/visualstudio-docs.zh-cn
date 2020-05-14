---
title: IDebugModOpt |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt interface
ms.assetid: ebd525e3-d140-4071-9d8c-41871de4125e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e142ed1229f59cfc22ff33cba48e9e35eb4e4406
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726973"
---
# <a name="idebugmodopt"></a>IDebugModOpt
表示调试可选修改器。

## <a name="syntax"></a>语法

```
IDebugModOpt : IUnknown
```

## <a name="notes-for-callers"></a>呼叫者备注
 从表示类或方法的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象获取。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetModOpts](../../../extensibility/debugger/reference/idebugmodopt-getmodopts.md)|检索可选修改器的列表。|

## <a name="requirements"></a>要求
 标题： Sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
