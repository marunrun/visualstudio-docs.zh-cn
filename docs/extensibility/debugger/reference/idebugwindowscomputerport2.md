---
title: IDebugWindows计算机端口2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugWindowsComputerPort2 interface
ms.assetid: 25f327b8-0303-4268-88d1-74df630436aa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ef4162469651e4b69502d3a9639d1e86c62e0b7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718224"
---
# <a name="idebugwindowscomputerport2"></a>IDebugWindowsComputerPort2
允许查询有关目标计算机的信息。

## <a name="syntax"></a>语法

```
IDebugWindowsComputerPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由会话调试管理器的端口对象实现。

## <a name="methods"></a>方法
 下表显示了 的方法`IDebugWindowsComputerPort2`。

|方法|描述|
|------------|-----------------|
|[获取计算机信息](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)|检索有关调试器运行的计算机的信息。|

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
