---
title: 符号提供程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbol handler
- debugging [Debugging SDK], symbol handler
ms.assetid: 5fce651b-fead-4418-81b0-a011df7644ab
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65debb8fcb41bec1d42c82654c26bc7d19c04a67
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348518"
---
# <a name="symbol-provider"></a>符号提供程序
表达式计算器实现必须访问才能计算变量和表达式生成由语言编译器的符号调试信息。 它是通过使用符号提供程序 (SP) 的接口也称为符号处理程序。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 为托管的代码和本机代码使用程序数据库 (PDB) 符号文件格式提供 Sp。 如果没有强需要为您的程序以使用存储在自定义格式的符号，它是建议使用提供的 SPs [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

## <a name="implementation-notes"></a>实现说明
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的调试引擎期望与使用公共语言运行时 (CLR) 接口 SPs 交谈。 因此，将使用 Visual Studio 的调试引擎 SP 必须支持 CLR。 所有 CLR 调试接口的完整列表可在 debugref.doc，它是一部分的[!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)]。

 如果你 SP 将仅使用自定义调试引擎，可以实现 SP，根据具体取决于调试引擎的需求。

## <a name="see-also"></a>请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)