---
title: 取消生成的代码的代码分析冲突
ms.date: 05/13/2019
ms.topic: conceptual
ms.assetid: 3a96434e-d419-43a7-81ba-95cccac835b8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6ee4e3df94e46b4d3cc996a23fc1e40401195e21
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551132"
---
# <a name="how-to-suppress-code-analysis-warnings-for-generated-code"></a>如何：禁止对生成的代码显示代码分析警告

生成的代码包括通过托管代码编译器或第三方工具添加到你的项目中的代码。 你可能想要查看代码分析在生成的代码中发现的规则冲突。 但是, 由于无法查看和维护包含冲突的代码, 因此你可能不想看到它们。

项目的 "代码分析" 属性页上的 "**禁止显示生成的代码结果**" 复选框使您可以选择是否显示第三方工具生成的代码的代码分析警告。

> [!NOTE]
> 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 可以查看和维护窗体或模板的源代码。

### <a name="to-suppress-warnings-for-generated-code-in-a-project"></a>禁止显示项目中生成的代码的警告

1. 右键单击 "**解决方案资源管理器**中的项目, 然后单击"**属性**"。

2. 选择 "**代码分析**" 选项卡。

3. 选中 "**禁止显示生成的代码结果**" 复选框。

> [!NOTE]
> 您只能禁止显示旧分析中的警告。 目前不能取消[分析器](roslyn-analyzers-overview.md)中的代码分析警告。