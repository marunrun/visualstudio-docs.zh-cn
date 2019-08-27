---
title: 同步项目规则集与签入策略
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.selecttfsruleset
ms.assetid: 9b02f934-2db6-41ec-aaff-9c31ceec2f04
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 80d13afe27eab28c88d2513b6c8be986ab1c960a
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66260853"
---
# <a name="how-to-synchronize-code-project-rule-sets-with-an-azure-devops-project-check-in-policy"></a>如何：使用 Azure DevOps 项目签入策略同步代码项目规则集

通过指定包含至少设置为签入策略规则中指定的规则的规则集同步到 Azure DevOps 项目的签入策略的代码项目的代码分析设置。 你的名称和位置的规则集签入策略，可以通知你开发人员的主管。 可以使用以下选项之一以确保项目的代码分析使用正确的规则集：

- 如果签入策略使用某个 Microsoft 内置规则集，打开代码项目的属性对话框，显示代码分析页中，然后选择代码项目设置的代码分析页上设置的规则。 Microsoft 标准规则集自动随 Visual Studio 设置为只读的不应编辑。 如果不编辑规则集，保证中的规则策略和本地规则集是匹配。

- 如果签入策略使用自定义规则集，请在版本控制，若要创建的本地副本中执行 get 操作的规则集文件。 然后在代码项目的代码分析设置中指定的本地位置。 可以保证规则是要匹配的规则集签入策略是最新。

     如果将版本控制位置映射到在与 Azure DevOps 项目根关系与你的代码项目相同的本地文件夹中，使用相对路径来设置规则的位置。 相对路径可确保代码分析的代码项目设置，可以移动到其他计算机。

- 自定义规则集的代码项目的签入策略的副本。 请确保新的规则集包含在签入策略中的所有规则和想要包括的任何其他规则。 必须确保规则集，为签入策略设置在规则中包含的所有规则。

## <a name="to-specify-a-microsoft-standard-rule-set"></a>若要指定 Microsoft 标准规则设置

1. 在中**解决方案资源管理器**，右键单击代码项目，然后单击**属性**。

2. 单击**代码分析**。

3. 在中**运行此规则集**列表中，单击签入策略规则设置。

## <a name="to-specify-a-custom-check-in-policy-rule-set"></a>若要指定自定义签入策略规则设置

1. 如果有必要，请执行 get 操作指定的签入策略的规则集文件。

2. 在中**解决方案资源管理器**，右键单击代码项目，然后单击**属性**。

3. 单击**代码分析**。

4. 在中**运行此规则集**列表中，单击 **\<浏览...>** 。

5. 在中**打开**对话框框中，指定签入策略规则集文件。

## <a name="to-create-a-custom-rule-set-for-a-code-project"></a>若要创建自定义规则设置为代码项目

1. 请单击以选择项目设置对话框的代码分析页上的 Azure DevOps 项目的签入策略本主题前面的过程之一。

2. 单击“打开”  。

3. 添加或删除规则通过使用[规则集编辑器](../code-quality/working-in-the-code-analysis-rule-set-editor.md)。

4. 保存已修改的规则设置为本地计算机上的.ruleset 文件或 UNC 路径。

5. 打开代码项目中，属性对话框并显示**代码分析**页。

6. 在中**运行此规则集**列表中，单击 **\<浏览...>** 。

7. 在中**打开**对话框框中，指定的规则集文件。
