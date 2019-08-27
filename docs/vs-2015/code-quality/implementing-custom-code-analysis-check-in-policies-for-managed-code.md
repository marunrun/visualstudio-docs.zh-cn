---
title: 实现自定义代码分析签入策略的托管代码 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f0b22eabc4df4b6ce7e8596f0c6546cb3a4c61c8
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696660"
---
# <a name="implementing-custom-code-analysis-check-in-policies-for-managed-code"></a>对托管代码实施自定义代码分析签入策略
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

代码分析签入策略可指定一组签入到版本控制之前，团队项目的成员必须在源代码运行的规则。 Microsoft 提供的一组标准*规则集*到功能区域的组代码分析规则。 *自定义签入策略规则集*指定一组特定于团队项目的代码分析规则。 规则集存储在.ruleset 文件。  
  
 签入策略是在团队项目级别设置和指定的版本控制树中的.ruleset 文件的位置。 团队策略自定义规则集的版本控制位置没有限制。  
  
 代码分析配置为使用单个代码项目中的每个项目的属性窗口。 由本地计算机上的.ruleset 文件的物理位置指定的自定义规则集的代码项目。 如果所指定的 .ruleset 文件位于代码项目所在的驱动器上，则 Visual Studio 将在项目配置中使用文件的相对路径。  
  
 用于创建团队项目自定义规则集的建议的做法是将签入策略.ruleset 文件存储在不属于任何代码项目的特殊文件夹。 如果将文件存储在专用文件夹中，您可以应用权限，限制可以编辑该规则文件，并且可以轻松地移动的目录结构，包含到另一个目录或计算机的项目。  
  
## <a name="creating-the-team-project-custom-check-in-rule-set"></a>创建团队项目签入的自定义规则集  
 若要创建自定义规则集为团队项目，您首先创建签入策略规则中设置的特殊文件夹**源控件资源管理器**。 然后创建规则集文件，并将文件添加到版本控制。 最后，指定将规则集的代码分析签入策略的团队项目。  
  
> [!NOTE]
> 若要在团队项目中创建一个文件夹，首先必须映射团队项目根目录到本地计算机上的位置。 有关详细信息，请参阅[创建和使用工作区 （旧）](https://msdn.microsoft.com/db4d5692-179a-44fe-ad31-0c1c900c9cb2)。  
  
#### <a name="to-create-the-version-control-folder-for-the-check-in-policy-rule-set"></a>若要创建签入策略规则集的版本控制文件夹  
  
1. 在中[!INCLUDE[esprtfc](../includes/esprtfc-md.md)]，展开团队项目节点，并单击**源代码管理**。  
  
2. 在中**文件夹**窗格中，右键单击团队项目，然后单击**新文件夹**。  
  
3. 在主源代码管理窗格中，右键单击**新文件夹**，单击**重命名**，并键入规则集文件夹的名称。  
  
#### <a name="to-create-the-check-in-policy-rule-set"></a>若要创建签入策略规则集  
  
1. 上**文件**菜单，依次指向**新建**，然后单击**文件**。  
  
2. 在中**类别**列表中，单击**常规**。  
  
3. 在中**模板**列表中，双击**代码分析规则集**。  
  
4. 指定要在规则集中包含的规则，然后将规则集文件保存到您创建的规则集文件夹。  
  
     有关详细信息，请参阅[创建自定义规则集](../code-quality/creating-custom-code-analysis-rule-sets.md)  
  
#### <a name="to-add-the-rule-set-file-to-version-control"></a>若要将规则添加到版本控制设置文件  
  
1. 在中**源控件资源管理器**，右键单击新文件夹，然后单击**项目添加到文件夹**。  
  
     有关详细信息，请参阅[使用版本控制](https://msdn.microsoft.com/library/33267cee-fe5f-4aa3-b2cd-6d22ceace314)。  
  
2. 单击规则集文件的创建，然后单击**完成**。  
  
     添加到源代码管理文件并将其签出给您。  
  
3. 在中**源控件资源管理器**详细信息窗口中，右键单击文件名称，然后单击**签入挂起的更改**。  
  
4. 在中**签入**对话框中，您可以选择添加注释，然后单击**签入**。  
  
    > [!NOTE]
    > 如果已为你的团队项目配置代码分析签入策略和所选**执行签入以只包含属于当前解决方案的文件**，将触发策略失败警告。 在策略失败对话框中，选择**重写策略失败并继续签入**。 添加所需的注释，然后依次**确定**。  
  
#### <a name="to-specify-the-rule-set-file-as-the-check-in-policy"></a>若要指定该规则设置文件，为签入策略  
  
1. 上**团队**菜单，依次指向**团队项目设置**，然后单击**源代码管理**。  
  
2. 单击**签入策略**，然后单击**添加**。  
  
3. 在中**签入策略**列表中，双击**代码分析**，并确保选中**托管代码的执行代码分析**复选框处于选中状态。  
  
4. 在中**运行此规则集**列表中，单击 **\<从源代码管理选择规则集 >** 。  
  
5. 键入在版本控制中签入策略规则集文件的路径。  
  
     路径必须符合以下语法：  
  
     **$/** `TeamProjectName` **/** `VersionControlPath`  
  
    > [!NOTE]
    > 可以使用中的以下过程之一来复制路径**源控件资源管理器**:  
  
    - 在中**文件夹**窗格中，单击包含规则集文件的文件夹。 将复制的文件夹中显示的版本控制路径**源**框，然后手动键入规则集文件的名称。  
  
    - 在详细信息窗口中，右键单击规则集文件，然后依次**属性**。 上**常规**选项卡上，复制中的值**服务器名称**。  
  
## <a name="synchronizing-code-projects-to-the-check-in-policy-rule-set"></a>同步向签入策略规则集的代码项目  
 您指定的团队项目签入策略规则设置为代码项目的属性对话框中的代码项目配置代码分析规则集。 如果代码项目所在的驱动器位于规则集，则相对路径用于指定规则集，当从文件对话框中选择路径。 项目属性设置为可移植到其他计算机使用类似的本地版本的相对路径，可以控制结构。  
  
#### <a name="to-specify-a-team-project-rule-set-as-the-rule-set-of-a-code-project"></a>若要指定团队项目规则设置为代码项目规则集  
  
1. 如有必要，检索从版本控制签入策略规则集文件夹和文件。  
  
     您可以执行此步骤中的**源控件资源管理器**通过右键单击该规则设置文件夹，然后单击**获取最新版本**。  
  
2. 在中**解决方案资源管理器**，右键单击代码项目，然后单击**属性**。  
  
3. **单击代码分析**。  
  
4. 如有必要，单击中相应的选项**配置**并**平台**列出。  
  
5. 若要使用指定的配置生成的代码项目中的每次运行代码分析，请选择**启用生成代码分析 （定义 CODE_ANALYSIS 常量）** 复选框。  
  
6. 若要忽略来自其他公司的组件中的代码，请选择**禁止显示生成代码的结果**复选框。  
  
7. 在中**运行此规则集**列表中，单击 **\<浏览...>** 。  
  
8. 指定签入策略规则集文件的本地版本。
