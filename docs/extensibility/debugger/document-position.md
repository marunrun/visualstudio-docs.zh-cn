---
title: 文档位置 |Microsoft Docs
description: 了解 Visual Studio 中的文档位置调试如何在源文件中提供 IDE 已知的位置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: b59d739c-7572-427f-a70d-4e5df63d02c1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fef3debcbce3a178c4321114d69c87c627611a07
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915318"
---
# <a name="document-position"></a>文档位置
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中， *文档位置*：

- 在源文件中提供对 IDE 已知的位置的抽象。 目前大多数语言都可以将文档位置视为源文件中的位置。

- 描述源文档中到调试引擎的位置。

- 由 [IDebugDocumentPosition2](../../extensibility/debugger/reference/idebugdocumentposition2.md) 接口实现。

## <a name="see-also"></a>另请参阅
- [代码上下文](../../extensibility/debugger/code-context.md)
- [文档上下文](../../extensibility/debugger/document-context.md)
- [符号提供程序](../../extensibility/debugger/symbol-provider.md)
- [符号提供程序接口](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
