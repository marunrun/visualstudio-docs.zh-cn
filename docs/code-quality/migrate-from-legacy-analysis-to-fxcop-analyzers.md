---
title: '从 FxCop 迁移到源分析 (FxCop 分析器) '
ms.custom: SEO-VS-2020
description: 了解如何首次分析代码或者如何从二进制分析迁移 (FxCop) 到使用源分析 (FxCop 分析器) 分析托管代码的新方式。
ms.date: 03/06/2020
ms.topic: conceptual
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- FxCop, migration
- legacy analysis, migration
- source code analysis, migration
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2109d7cbcaaf56600812e27c3055fb3198848228
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810202"
---
# <a name="migrate-from-legacy-analysis-fxcop-to-source-analysis-fxcop-analyzers"></a> (FxCop 分析器中，从旧式分析 (FxCop) 迁移到源分析) 

.NET Compiler Platform ( "Roslyn" 的源分析 ) 分析器替换托管代码的 [旧式分析](../code-quality/code-analysis-for-managed-code-overview.md) 。 对于更高版本的项目模板（如 .NET Core 和 .NET Standard 项目），旧版分析不可用。

许多旧分析 (FxCop) 规则已被重写为 FxCop 分析器，一组 Roslyn 代码分析器。 将 [FxCop 分析器安装为](install-fxcop-analyzers.md#nuget-package) 项目或解决方案所引用的 NuGet 包。 FxCop 分析器在编译器执行期间运行基于源代码的分析。 报告分析器结果以及编译器结果。

有关旧分析与源分析之间的差异的详细信息，请参阅以下内容：

- [源代码分析与传统分析](../code-quality/fxcop-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-fxcop-analyzers)

- [FxCop 分析器常见问题](../code-quality/fxcop-analyzers-faq.md)

若要迁移到源分析，请 [安装 FxCop 分析器](../code-quality/install-fxcop-analyzers.md)。 与传统的分析规则冲突一样，源代码分析冲突会出现在 Visual Studio 的“错误列表”窗口中。 此外，源代码分析冲突也会在代码编辑器中显示，表现为违规代码下有波浪线**。 规则的[严重性设置](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)决定波浪线的颜色。 若要查看移植到新 FxCop 分析器的规则的状态，请参阅 [移植和 unported 规则](../code-quality/fxcop-rule-port-status.md)。

若要详细了解如何配置 FxCop 分析器：

- 若要配置 FxCop 分析器，请参阅 [配置 fxcop 分析器](../code-quality/configure-fxcop-analyzers.md)。

- 若要了解如何使用预定义的规则和 EditorConfig 或规则集文件来配置分析器，请参阅 [启用规则类别](../code-quality/analyzer-rule-sets.md)。