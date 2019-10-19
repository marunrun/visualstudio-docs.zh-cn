---
title: 为托管代码实现自定义代码分析签入策略 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.code.analysis.selecttfsrulesets
- vs.code.analysis.browsefortfsruleset
- vs.code.analysis.policyeditor
ms.assetid: fd029003-5671-4b24-8b6f-032e0a98b2e8
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1cf759e01e5f152f2220124c90f145bfbbe3c01d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651588"
---
# <a name="implementing-custom-code-analysis-check-in-policies-for-managed-code"></a>对托管代码实施自定义代码分析签入策略
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

代码分析签入策略指定团队项目成员必须在源代码中运行的一组规则，才能将其签入到版本控制中。 Microsoft 提供一组标准*规则集*，将代码分析规则分组到功能区域。 *自定义签入策略规则集*指定一组特定于团队项目的代码分析规则。 规则集存储在一个. 规则文件中。

 签入策略是在团队项目级别设置的，并由版本控制树中的规则集文件的位置指定。 团队策略自定义规则集的版本控制位置没有限制。

 为每个项目的 "属性" 窗口中的各个代码项目配置代码分析。 代码项目的自定义规则集由本地计算机上的文件组文件的物理位置指定。 如果所指定的 .ruleset 文件位于代码项目所在的驱动器上，则 Visual Studio 将在项目配置中使用文件的相对路径。

 创建团队项目自定义规则集的建议做法是将签入策略 "规则集文件" 存储在不属于任何代码项目的特殊文件夹中。 如果将文件存储在专用文件夹中，则可以应用权限来限制谁可以编辑规则文件，并且可以轻松地将包含项目的目录结构移到另一个目录或计算机。

## <a name="creating-the-team-project-custom-check-in-rule-set"></a>创建团队项目自定义签入规则集
 若要为团队项目创建自定义规则集，请首先在**源代码管理器**中创建签入策略规则集的特殊文件夹。 然后，创建规则集文件并将文件添加到版本控制。 最后，将规则集指定为团队项目的代码分析签入策略。

> [!NOTE]
> 若要在团队项目中创建文件夹，首先必须将团队项目根映射到本地计算机上的某个位置。 有关详细信息，请参阅[创建和使用工作区（旧）](https://msdn.microsoft.com/db4d5692-179a-44fe-ad31-0c1c900c9cb2)。

#### <a name="to-create-the-version-control-folder-for-the-check-in-policy-rule-set"></a>为签入策略规则集创建版本控制文件夹

1. 在 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 中，展开 "团队项目" 节点，然后单击 "**源代码管理**"。

2. 在 "**文件夹**" 窗格中，右键单击团队项目，然后单击 "**新建文件夹**"。

3. 在主 "源代码管理" 窗格中，右键单击 "**新建文件夹**"，单击 "**重命名**"，然后键入规则集文件夹的名称。

#### <a name="to-create-the-check-in-policy-rule-set"></a>创建签入策略规则集

1. 在 "**文件**" 菜单上，指向 "**新建**"，然后单击 "**文件**"。

2. 在 "**类别**" 列表中，单击 "**常规**"。

3. 在 "**模板**" 列表中，双击 "**代码分析规则集**"。

4. 指定规则集中要包含的规则，然后将规则集文件保存到创建的规则集文件夹中。

     有关详细信息，请参阅[创建自定义规则集](../code-quality/creating-custom-code-analysis-rule-sets.md)

#### <a name="to-add-the-rule-set-file-to-version-control"></a>将规则集文件添加到版本控制

1. 在**源代码管理器**中，右键单击新文件夹，然后单击 "**将项添加到文件夹**"。

     有关详细信息，请参阅[使用版本控制](https://msdn.microsoft.com/library/33267cee-fe5f-4aa3-b2cd-6d22ceace314)。

2. 单击您创建的规则集文件，然后单击 "**完成**"。

     文件将被添加到源代码管理中并签出给你。

3. 在 "**源代码管理器**详细信息" 窗口中，右键单击文件名，然后单击 "**签入挂起的更改**"。

4. 在 "**签入**" 对话框中，您可以选择添加注释，然后单击 "**签入**"。

    > [!NOTE]
    > 如果你已经为你的团队项目配置了代码分析签入策略，并且已选择 "**强制签入只包含属于当前解决方案的文件**"，则会触发策略失败警告。 在 "策略失败" 对话框中，选择 "**重写策略失败并继续签入**"。 添加所需注释，然后单击 **"确定"** 。

#### <a name="to-specify-the-rule-set-file-as-the-check-in-policy"></a>将规则集文件指定为签入策略

1. 在 "**团队**" 菜单上，指向 "**团队项目设置**"，然后单击 "**源代码管理**"。

2. 单击 "**签入策略**"，然后单击 "**添加**"。

3. 在 "**签入策略**" 列表中，双击 "**代码分析**"，并确保已选中 "**强制对托管代码执行代码分析**" 复选框。

4. 在 "**运行此规则集**" 列表中，单击 "**从源代码管理 > \<Select 规则集**"。

5. 在版本控制中键入签入策略规则集文件的路径。

     路径必须符合以下语法：

     **$/** `TeamProjectName` **/** `VersionControlPath`

    > [!NOTE]
    > 可以在**源代码管理器**中使用以下过程之一来复制路径：

    - 在 "**文件夹**" 窗格中，单击包含规则集文件的文件夹。 复制 "**源**" 框中显示的文件夹的版本控制路径，然后手动键入规则集文件的名称。

    - 在详细信息窗口中，右键单击规则集文件，然后单击 "**属性**"。 在 "**常规**" 选项卡上，复制 "**服务器名称**" 中的值。

## <a name="synchronizing-code-projects-to-the-check-in-policy-rule-set"></a>将代码项目同步到签入策略规则集
 在代码项目的 "属性" 对话框中，将团队项目签入策略规则集指定为代码项目配置的代码分析规则集。 如果规则集与代码项目位于同一驱动器上，则在从 "文件" 对话框中选择路径时，使用相对路径来指定规则集。 相对路径使项目属性设置可移植到使用相似本地版本控制结构的其他计算机。

#### <a name="to-specify-a-team-project-rule-set-as-the-rule-set-of-a-code-project"></a>将团队项目规则集指定为代码项目的规则集

1. 如有必要，请从版本控制中检索签入策略规则集文件夹和文件。

     可以通过右键单击规则集文件夹，然后单击 "**获取最新版本**"，在**源代码管理器**中执行此步骤。

2. 在**解决方案资源管理器**中，右键单击代码项目，然后单击 "**属性**"。

3. **单击 "代码分析"** 。

4. 如有必要，请单击 "**配置**" 和 "**平台**" 列表中的相应选项。

5. 若要在每次使用指定配置生成代码项目时运行代码分析，请选中 "**生成时启用代码分析（定义 CODE_ANALYSIS 常量）** " 复选框。

6. 若要忽略其他公司的组件中的代码，请选中 "**禁止显示生成代码的结果**" 复选框。

7. 在 "**运行此规则集**" 列表中，单击 " **\<Browse .。。>** 。

8. 指定签入策略规则集文件的本地版本。
