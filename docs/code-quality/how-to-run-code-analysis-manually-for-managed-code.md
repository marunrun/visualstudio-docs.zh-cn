---
title: 如何为托管代码手动运行代码分析
ms.date: 11/04/2019
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
- run code analysis
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: mavasani
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: bbd3d2023310b9412310fc86f419c2e8c4a127c4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "88893393"
---
# <a name="how-to-run-code-analysis-manually-for-managed-code-requires-visual-studio-2019-version-165-or-later"></a>如何：手动运行托管代码的代码分析 (需要 Visual Studio 2019 版本16.5 或更高版本) 
默认情况下，在进行实时分析时以及在生成期间，) 代码分析器 .NET Compiler Platform ( "Roslyn" 将分析 c # 或 Visual Basic 代码。 因此，您通常不需要手动触发代码分析。 但是，在某些情况下，你可能需要手动触发代码分析：

- 默认情况下，实时代码分析仅对 Visual Studio 中打开的文件执行分析器。 但是，你可能对查看特定项目或解决方案中的所有文件的代码分析警告感兴趣。 如果是这样，则需要对项目或解决方案触发一次代码分析。 或者，您可以启用连续的实时代码分析以对整个解决方案执行。 有关详细信息，请参阅[如何：配置托管代码的实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)。
- 您可能更倾向于通过连续实时分析或生成时分析执行的按需代码分析执行工作流。 如果是这样，则可以在 "实时分析" 和/或 "生成" 期间禁用分析器执行。 有关禁用分析的信息，请参阅 [如何禁用源代码分析](disable-code-analysis.md)。 然后，需要在项目或解决方案上手动触发一次代码分析。

### <a name="run-code-analysis-manually"></a>手动运行代码分析

1. 在 **解决方案资源管理器**中，选择项目。

2. 在 "**分析**" 菜单上，选择 "对*项目名称***运行代码分析**"。

代码分析将开始在后台执行。 你应在 Visual Studio 状态栏中看到消息 " **正在运行代码分析 \<project> ...** "。 完成代码分析后，状态消息将更改为 "**已完成 \<project> 代码分析**"。 将立即刷新错误列表，并将进行所有代码分析诊断。
