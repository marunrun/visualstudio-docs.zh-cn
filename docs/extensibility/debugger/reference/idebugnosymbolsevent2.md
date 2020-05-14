---
title: IDebugNoSymbolevent2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugNoSymbolsEvent2 interface
ms.assetid: f6fb6388-47f6-4385-9ad5-95d62f9a7592
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9483c5a434ddfddb3f877111deabea9be6520b05
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726708"
---
# <a name="idebugnosymbolsevent2"></a>IDebugNoSymbolsEvent2
向[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试器 UI 发出信号，警告用户无法为启动的可执行文件找到符号。

## <a name="syntax"></a>语法

```
IDebugNoSymbolsEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 由调试引擎实现，并由[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试器 UI 使用。

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
