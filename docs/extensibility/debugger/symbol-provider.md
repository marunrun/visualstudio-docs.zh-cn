---
title: 符号提供程序 |Microsoft Docs
description: 了解 Visual Studio 提供的用于使表达式计算器计算变量和表达式的符号提供程序。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 043014ebababd990c9cae03f28cb1b642d576071
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996040"
---
# <a name="symbol-provider"></a>符号提供程序
表达式计算器实现必须访问语言编译器生成的符号调试信息，才能计算变量和表达式。 它通过使用符号提供程序 (SP) （也称为符号处理程序）的接口来实现此目的。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用程序数据库为托管代码和本机代码提供 Sp (PDB) 符号文件格式。 除非你的程序很难使用以自定义格式存储的符号，否则建议你使用提供的 Sp [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="implementation-notes"></a>实现说明
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试引擎需要使用公共语言运行时 (CLR) 接口与 SPs 进行通信。 因此，将使用 Visual Studio 调试引擎的 SP 必须支持 CLR。 可以在 debugref.doc 中找到所有 CLR 调试接口的完整列表，该列表是的一部分 [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] 。

 如果您的 SP 只使用您的自定义调试引擎，则可以根据调试引擎的需求，根据您的需要实现 SP。

## <a name="see-also"></a>另请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
