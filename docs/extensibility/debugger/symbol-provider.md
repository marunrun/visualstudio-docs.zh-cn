---
title: 符号提供程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbol handler
- debugging [Debugging SDK], symbol handler
ms.assetid: 5fce651b-fead-4418-81b0-a011df7644ab
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31b90846d9494ee046cf9dc4a3e5de9ff033ea3f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712812"
---
# <a name="symbol-provider"></a>符号提供程序
表达式赋值器实现必须访问语言编译器生成的符号调试信息，以便计算变量和表达式。 它通过使用符号提供程序 （SP） 的接口（也称为符号处理程序）来这样做。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用程序数据库 （PDB） 符号文件格式为托管代码和本机代码提供 SP。 除非程序非常需要使用以自定义格式存储的符号，否则建议您使用 提供的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]SP。

## <a name="implementation-notes"></a>实现说明
 调试[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]引擎需要使用通用语言运行时 （CLR） 接口与 SP 进行对话。 因此，将配合 Visual Studio 调试引擎工作的 SP 必须支持 CLR。 所有 CLR 调试接口的完整列表可以在 debugref.doc 中找到，这是 的一[!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)]部分。

 如果您的 SP 将仅与自定义调试引擎一起使用，则可以根据调试引擎的需要，实现您认为合适的 SP。

## <a name="see-also"></a>请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
