---
title: 如何：手动运行托管代码的旧代码分析
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code analysis, running
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 9d2693bcff8e83839b4171bae60b138c967f10e5
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2020
ms.locfileid: "79432083"
---
# <a name="how-to-run-legacy-code-analysis-manually-for-managed-code"></a>如何：手动运行托管代码的旧代码分析
代码分析工具提供有关源代码中可能存在缺陷的信息。 您可以在代码项目的每个生成中自动运行代码分析，也可以手动运行代码分析。 运行代码分析时检查的规则在项目属性页的"代码分析"页上指定。 有关详细信息，请参阅[如何：为托管代码项目配置代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)。

## <a name="to-run-code-analysis-manually"></a>手动运行代码分析

1. 如果您在 Visual Studio 2019 版本 16.5 或更高版本上，请在启动 Visual Studio 之前对命令提示符执行以下命令：

```
set EnableLegacyCodeAnalysis = true
```

2. 在**解决方案资源管理器中**，单击项目。

3. 在 **"分析"** 菜单上，单击"*在项目名称***上运行代码分析**"。

