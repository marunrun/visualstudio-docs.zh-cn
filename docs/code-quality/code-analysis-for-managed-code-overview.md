---
title: 托管代码分析
ms.date: 06/12/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a44465b5f3daf89e915a5f6f5e7abe6c856598e5
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546920"
---
# <a name="overview-of-code-analysis-for-managed-code-in-visual-studio"></a>Visual Studio 中托管代码的代码分析概述

Visual Studio 可以通过以下两种方式对托管代码执行代码分析: 通过[传统分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)(也称为 FxCop 静态分析) 托管程序集, 以及更新式的基于 .NET Compiler Platform 的[代码分析器](../code-quality/roslyn-analyzers-overview.md)。 基于 .NET Compiler Platform 的代码分析器 (在你键入时实时分析你的代码) 将替换旧的 FxCop 静态代码分析, 后者仅分析已编译的代码。

## <a name="see-also"></a>请参阅

- [基于 .NET Compiler Platform 的分析器概述](../code-quality/roslyn-analyzers-overview.md)
