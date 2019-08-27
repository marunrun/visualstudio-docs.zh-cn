---
title: IDebugWindowsComputerPort2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugWindowsComputerPort2 interface
ms.assetid: 25f327b8-0303-4268-88d1-74df630436aa
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b2a60572c652080f2655ab7fe33954a661fbe07e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319744"
---
# <a name="idebugwindowscomputerport2"></a>IDebugWindowsComputerPort2
允许的目标计算机的信息进行查询。

## <a name="syntax"></a>语法

```
IDebugWindowsComputerPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 此接口是由会话调试管理器的 port 对象实现的。

## <a name="methods"></a>方法
 下表显示的方法`IDebugWindowsComputerPort2`。

|方法|描述|
|------------|-----------------|
|[GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)|检索有关计算机上的信息的调试器中运行。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll