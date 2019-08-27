---
title: 创建或更新标准代码分析签入策略
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.policyeditor
helpviewer_keywords:
- code analysis, migrating check-in policy
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 768efb3e874f6427cd23f63f14671aa2db1bea71
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62816352"
---
# <a name="how-to-create-or-update-standard-code-analysis-check-in-policies"></a>如何：创建或更新标准代码分析签入策略

你可以要求运行代码分析是 Azure DevOps 项目中的所有代码项目通过使用代码分析签入策略。 需要代码分析可以提高签入代码库的代码的质量。

> [!NOTE]
> 仅当使用 Team Foundation Server 提供此功能。

代码分析签入策略设置在项目设置中，并将应用于每个代码项目。 代码分析运行的代码项目的项目 (.xxproj) 文件中的代码项目的配置。 代码分析运行在本地计算机上执行。 时启用代码分析签入策略、 要签入代码项目中的文件必须在其最后一次编辑后编译和代码分析运行的最小值，包含在项目设置中的规则必须在计算机上执行的更改s 所做。

- 通过指定的签入策略设置为托管代码中，*规则集*，其中包含代码分析规则的子集。

- 对于 C /C++代码，在 Visual Studio 2017 版本 15.6 及更早版本，签入策略需要运行所有代码分析规则。 可以添加预处理器指令，以禁用 Azure DevOps 项目中的单个代码项目的特定规则。 15.7 版中及更高版本，可以使用 **/analyze: ruleset**来指定要运行的规则。 有关详细信息，请参阅[使用规则集指定C++运行规则](using-rule-sets-to-specify-the-cpp-rules-to-run.md)。

指定托管代码的签入策略后，团队成员可以同步到 Azure DevOps 项目策略设置的代码项目及其代码分析设置。

## <a name="to-open-the-check-in-policy-editor"></a>若要打开签入策略编辑器

1. 在团队资源管理器中右键单击项目名称，指向**项目设置**，然后单击**源代码管理**。

1. 在中**源代码管理**对话框中，选择**签入策略**选项卡。

1. 执行下列操作之一：

    - 单击**添加**来创建新的签入策略。

    - 双击现有**代码分析**中的项**策略类型**要更改的策略列表。

## <a name="to-set-policy-options"></a>若要设置策略选项

选中或清除以下选项：

|选项|描述|
|------------|-----------------|
|**执行签入以只包含属于当前解决方案的文件。**|只能对解决方案和项目配置文件中指定的文件，可以运行代码分析。 此策略可确保所有代码都是一种解决方案的一部分进行都分析。|
|**强制执行 C /C++代码分析 (/analyze)**|需要的所有 C 或C++项目在生成使用 /analyze 编译器选项，它们可以在签入之前运行代码分析。|
|**为托管代码强制实施代码分析**|需要托管的所有项目运行代码分析和生成它们可以在签入之前。|

## <a name="to-specify-a-managed-rule-set"></a>若要指定托管的规则设置

从**运行此规则集**列出，请使用以下方法之一：

- 选择 Microsoft 标准规则集。

- 选择自定义规则集通过单击 **\<选择规则集从源代码管理...>** 。 然后，键入源代码管理浏览器中的规则集的版本控制的路径。 版本控制路径的语法是：

   **$/** `TeamProjectName` **/** `VersionControlPath`

详细了解如何创建和实现自定义签入策略规则集，请参阅[为托管代码实现自定义签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)。

## <a name="see-also"></a>请参阅

- [创建和使用代码分析签入策略](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)