---
title: 模块 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- modules
- debugging [Debugging SDK], modules
ms.assetid: c4cf2809-dbdb-4e75-9273-b3d3d77b67d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: abdf76c7f5f031d2ef7f3bcac2bae8a2c508b783
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738347"
---
# <a name="modules"></a>模块
在调试器体系结构方面，*模块*：

- 是代码的物理容器，如可执行文件或 DLL。

- 可以重新加载其符号并描述自身。 模块说明显示在 IDE 的"模块"窗口中。

- 由[IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)接口表示，该接口由调试引擎创建，用于描述模块。

## <a name="see-also"></a>请参阅
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)
