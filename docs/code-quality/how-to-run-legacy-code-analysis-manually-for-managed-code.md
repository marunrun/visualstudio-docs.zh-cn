---
title: 如何为托管代码手动运行旧代码分析
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 44190f8e828f9a971f15b57266978603dcac8139
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462057"
---
# <a name="how-to-run-legacy-code-analysis-manually-for-managed-code"></a>如何：手动运行托管代码的旧式代码分析
代码分析工具为您提供有关源代码中可能存在的缺陷的信息。 您可以在每次生成代码项目时自动运行代码分析，还可以手动运行代码分析。 代码分析运行时检查的规则在项目属性页的 "代码分析" 页上指定。 有关详细信息，请参阅[如何：配置托管代码项目的代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)。

## <a name="to-run-code-analysis-manually"></a>手动运行代码分析

1. 如果你在 Visual Studio 2019 版本16.5 或更高版本上，请在启动 Visual Studio 之前，在命令提示符下执行以下命令：

```
set EnableLegacyCodeAnalysis = true
```

2. 在**解决方案资源管理器**中，单击该项目。

3. 在 "**分析**" 菜单上，单击 "对*项目名称***运行代码分析**"。

