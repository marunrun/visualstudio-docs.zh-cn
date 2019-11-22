---
title: Validate code with layer diagrams | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams, validating
- validation, layer diagrams
- validation, code
- code exploration, validating
- architecture, validating
- Visual Studio Ultimate, validating code
- validation, architecture
- validation, dependencies
- MSBuild, tasks
- MSBuild, layer diagrams
- MSBuild, validating code
ms.assetid: 70cbe55d-4b33-4355-b0a7-88c770a6f75c
caps.latest.revision: 84
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 596711c5c59738d5356437bb761e80caeddfbd6b
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301349"
---
# <a name="validate-code-with-layer-diagrams"></a>用层关系图验证代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

要确保代码不与其设计冲突，可以在 Visual Studio 中使用层关系图验证代码。 这可帮助你：

- 查找代码中的依赖项和层关系图上的依赖项之间的冲突。

- 查找建议的更改可能会影响的依赖项。

   例如，可以编辑层关系图来显示潜在的体系结构更改，然后对代码进行验证以查看受影响的依赖项。

- 将代码重构或迁移到其他设计。

   查找在将代码移动到其他体系结构时需要工作的代码或依赖项。

  **惠?**

- Visual Studio

- Team Foundation Build 服务器上的 Visual Studio，用于使用 Team Foundation Build 自动验证代码

- 一个具有建模项目和层关系图的解决方案。 该层关系图必须链接到要验证的 Visual C# .NET 或 Visual Basic .NET 项目中的项。 See [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md).

  若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

  你可以从 Visual Studio 中打开的层关系图或从命令提示符手动验证代码。 你还可以在运行本地生成或 Team Foundation Build 时自动验证代码。 See [Channel 9 Video: Design and validate your architecture using layer diagrams](https://go.microsoft.com/fwlink/?LinkID=252073).

> [!IMPORTANT]
> 如果想要使用 Team Foundation Build 运行层验证，则还必须在生成服务器上安装相同版本的 Visual Studio。

- [See if an item supports validation](#SupportsValidation)

- [Include other .NET assemblies and projects for validation](#IncludeReferences)

- [Validate code manually](#ValidateManually)

- [Validate code automatically](#ValidateAuto)

- [Troubleshoot layer validation issues](#TroubleshootingValidation)

- [Understand and resolve layer validation errors](#UnderstandingValidationErrors)

## <a name="SupportsValidation"></a> See if an item supports validation
 你可以将层链接到网站、Office 文档、纯文本文件和项目中跨多个应用共享的文件，但验证过程不包含这些内容。 如果引用的项目或程序集链接到单独的层，而且这些层之间没有依赖关系出现，则将不会出现验证错误。 除非代码使用此类引用，否则这些引用不被视为依赖项。

1. On the layer diagram, select one or more layers, right-click your selection, and then click **View Links**.

2. In **Layer Explorer**, look at the **Supports Validation** column. 如果该值为 false，则项不支持验证。

## <a name="IncludeReferences"></a> Include other .NET assemblies and projects for validation
 When you drag items to the layer diagram, references to the corresponding .NET assemblies or projects are added automatically to the **Layer References** folder in the modeling project. 此文件夹包含对验证过程中分析的程序集和项目的引用。 你也可以包含要验证的其他 .NET 程序集和项目，而无需将它们手动拖到层关系图上。

1. In **Solution Explorer**, right-click the modeling project or the **Layer References** folder, and then click **Add Reference**.

2. In the **Add Reference** dialog box, select the assemblies or projects, and then click **OK**.

## <a name="ValidateManually"></a> Validate code manually
 If you have an open layer diagram that is linked to solution items, you can run the **Validate** shortcut command from the diagram. You can also use the command prompt to run the **msbuild** command with the **/p:ValidateArchitecture** custom property set to **True**. 例如，在对代码进行更改时，请定期执行层验证以便能够提前捕获依赖项冲突。

#### <a name="to-validate-code-from-an-open-layer-diagram"></a>从打开的层关系图中验证代码

1. Right-click the diagram surface, and then click **Validate Architecture**.

    > [!NOTE]
    > By default, the **Build Action** property on the layer diagram (.layerdiagram) file is set to **Validate** so that the diagram is included in the validation process.

     The **Error List** window reports any errors that occur. For more information about validation errors, see [Understand and resolve layer validation errors](#UnderstandingValidationErrors).

2. To view the source of each error, double-click the error in the **Error List** window.

    > [!NOTE]
    > [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 可能会显示代码图，而不是显示错误的根源。 若代码所依赖的程序集不是由层关系图指定的，或代码缺少层关系图所指定的依赖项，则会出现此情况。 检查代码映射或代码，以确定此依赖关系是否应该存在。 For more information about code maps, see [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md).

3. To manage errors, see [Manage validation errors](#ManageErrors).

#### <a name="to-validate-code-at-the-command-prompt"></a>在命令提示符处验证代码

1. 打开 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 命令提示。

2. 选择以下选项之一：

   - 若要对照解决方案中的特定建模项目验证代码，请使用下面的自定义属性运行 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]。

     ```
     msbuild <FilePath+ModelProjectFileName>.modelproj /p:ValidateArchitecture=true
     ```

     - 或 -

       浏览到包含建模项目文件 (.modelproj) 和层关系图的文件夹，然后使用下面的自定义属性运行 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]：

     ```
     msbuild /p:ValidateArchitecture=true
     ```

   - 若要对照解决方案中的所有建模项目验证代码，请使用下面的自定义属性运行 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]：

     ```
     msbuild <FilePath+SolutionName>.sln /p:ValidateArchitecture=true
     ```

     - 或 -

       浏览到必须包含建模项目（包含层关系图）的解决方案文件夹，然后使用下面的自定义属性运行 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]：

     ```
     msbuild /p:ValidateArchitecture=true
     ```

     将列出发生的任何错误。 For more information about [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)], see [MSBuild](../msbuild/msbuild.md) and [MSBuild Task](../msbuild/msbuild-task.md).

   For more information about validation errors, see [Understand and resolve layer validation errors](#UnderstandingValidationErrors).

### <a name="ManageErrors"></a> Manage validation errors
 在开发过程中，你可能需要在验证期间禁止显示报告的某些冲突。 例如，你可能希望禁止显示你已解决或与特定情形不相关的错误。 禁止显示错误时，最好在 [!INCLUDE[esprfound](../includes/esprfound-md.md)] 中记录工作项。

> [!WARNING]
> 必须已连接到 TFS 源代码管理 (SCC) 才可创建或链接到工作项。 如果尝试打开到其他 TFS SCC 的连接，则 Visual Studio 会自动关闭当前解决方案。 请先确保已连接到相应的 SCC，然后再尝试创建或链接到工作项。 在更高版本的 Visual Studio 中，如果未连接到 SCC，则菜单命令不可用。

##### <a name="to-create-a-work-item-for-a-validation-error"></a>为验证错误创建工作项

- In the **Error List** window, right-click the error, point to **Create Work Item**, and then click the type of work item that you want to create.

  Use these tasks to manage validation errors in the **Error List** window:

|**若要**|**Follow these steps**|
|------------|----------------------------|
|禁止在验证过程中显示选定的错误|Right-click the one or multiple selected errors, point to **Manage Validation Errors**, and then click **Suppress Errors**.<br /><br /> 禁止显示的错误在显示时均带有删除线格式。 在你下次运行验证时，这些错误将不会显示。<br /><br /> 系统会在相应层关系图文件的 .suppressions 文件中对禁止显示的错误进行跟踪。|
|停止禁止显示选定的错误|Right-click the selected suppressed error or errors, point to **Manage Validation Errors**, and then click **Stop Suppressing Errors**.<br /><br /> 在你下次运行验证时，这些所选的禁止显示的错误将会显示。|
|Restore all suppressed errors in the **Error List** window|Right-click anywhere in the **Error List** window, point to **Manage Validation Errors**, and then click **Show All Suppressed Errors**.|
|Hide all suppressed errors from the **Error List** window|Right-click anywhere in the **Error List** window, point to **Manage Validation Errors**, and then click **Hide All Suppressed Errors**.|

## <a name="ValidateAuto"></a> Validate code automatically
 每次运行本地生成时，都可以执行层验证。 如果你的团队使用 Team Foundation Build，则可使用能够通过创建自定义 MSBuild 任务指定的封闭签入来执行层验证，并使用生成报告来收集验证错误。 To create gated check-in builds, see [Use a gated check-in build process to validate changes](https://msdn.microsoft.com/library/9cfc8b9c-1023-40fd-8ab5-1b1bd9c172ec).

#### <a name="to-validate-code-automatically-during-a-local-build"></a>在本地生成期间自动验证代码

- 使用文本编辑器打开建模项目 (.modelproj) 文件，然后包括以下属性：

```
<ValidateArchitecture>true</ValidateArchitecture>
```

 \- 或 -

1. In **Solution Explorer**, right-click the modeling project that contains the layer diagram or diagrams, and then click **Properties**.

2. In the **Properties** window, set the modeling project's **Validate Architecture** property to **True**.

    这将在验证过程中包括建模项目。

3. In **Solution Explorer**, click the layer diagram (.layerdiagram) file that you want to use for validation.

4. In the **Properties** window, make sure that the diagram's **Build Action** property is set to **Validate**.

    这将在验证过程中包括层关系图。

   To manage errors in the Error List window, see [Manage Validation Errors](#ManageErrors).

#### <a name="to-validate-code-automatically-during-a-team-foundation-build"></a>在 Team Foundation Build 期间自动验证代码

1. In **Team Explorer**, double-click the build definition, and then click **Process**.

2. Under **Build process parameters**, expand **Compilation**, and type the following in the **MSBuild Arguments** parameter:

    `/p:ValidateArchitecture=true`

   For more information about validation errors, see [Understand and resolve layer validation errors](#UnderstandingValidationErrors). 有关 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 的详细信息，请参阅：

- [生成应用程序](/azure/devops/pipelines/index)

- [Use the Default Template for your build process](https://msdn.microsoft.com/library/43930b12-c21b-4599-a980-2995e3d16e31)

- [Modify a Legacy Build that is Based on UpgradeTemplate.xaml](https://msdn.microsoft.com/library/ee1a8259-1dd1-4a10-9563-66c5446ef41c)

- [自定义生成过程模板](https://msdn.microsoft.com/library/b94c58f2-ae6f-4245-bedb-82cd114f6039)

- [Monitor Progress of a Running Build](https://msdn.microsoft.com/library/e51e3bad-2d1d-4b7b-bfcc-c43439c6c8ef)

## <a name="TroubleshootingValidation"></a> Troubleshoot layer validation issues
 下表描述了层验证问题及其解决方法。 这些问题不同于代码与设计发生冲突而导致出现的错误。 For more information about these errors, see [Understand and resolve layer validation errors](#UnderstandingValidationErrors).

|**问题**|**Possible Cause**|**解决方法**|
|---------------|------------------------|--------------------|
|验证错误不按预期发生。|在解决方案资源管理器中，从同一建模项目中的其他层关系图复制的层关系图上，验证不起作用。 以这种方式复制的层关系图包含与原始层关系图相同的引用。|向建模项目中添加一个新的层关系图。<br /><br /> 将源层关系图中的元素复制到新关系图。|

## <a name="UnderstandingValidationErrors"></a> Understanding and Resolving Layer Validation Errors
 在对照层关系图验证代码时，如果代码与设计发生冲突，则会出现验证错误。 例如，以下情况可能导致发生验证错误：

- 将项目指派给了错误的层。 在这种情况下，请移动项目。

- 项目（例如类）以与你的体系结构相冲突的方式使用了其他类。 在这种情况下，请重构代码以移除依赖关系。

  若要解决这些错误，请更新代码，直至验证过程中不出现其他错误为止。 可以反复执行此任务。

  以下各节描述这些错误中使用的语法，解释了这些错误的含义，并提供了纠正或管理这些错误的方法。

|**语法**|**描述**|
|----------------|---------------------|
|*ArtifactN*(*ArtifactTypeN*)|*ArtifactN* is an artifact that is associated with a layer on the layer diagram.<br /><br /> *ArtifactTypeN* is the type of *ArtifactN*, such as a **Class** or **Method**, for example:<br /><br /> MySolution.MyProject.MyClass.MyMethod(Method)|
|*NamespaceNameN*|命名空间的名称。|
|*LayerNameN*|层在层关系图上的名称。|
|*DependencyType*|The type of dependency relationship between *Artifact1* and *Artifact2*. For example, *Artifact1* has a **Calls** relationship with *Artifact2*.|

|**Error Syntax**|**Error Description**|
|----------------------|---------------------------|
|AV0001: Invalid Dependency: *Artifact1*(*ArtifactType1*) --> *Artifact2*(*ArtifactType2*)<br /><br /> Layers: *LayerName1*, *LayerName2* &#124; Dependencies: *DependencyType*|*Artifact1* in *LayerName1* should not have a dependency on *Artifact2* in *LayerName2* because *LayerName1* does not have a direct dependency on *LayerName2*.|
|AV1001: Invalid Namespace: *Artifact*<br /><br /> Layer: *LayerName* &#124; Required Namespace: *NamespaceName1* &#124; Current Namespace: *NamespaceName2*|*LayerName* requires that its associated artifacts must belong to *NamespaceName1*. *Artifact* is in *NamespaceName2*, not *NamespaceName1*.|
|AV1002: Depends on Forbidden Namespace: *Artifact1*(*ArtifactType1*) &#124; *Artifact2*(*ArtifactType2*)<br /><br /> Layer: *LayerName* &#124; Forbidden Namespace: *NamespaceName* &#124; Dependencies: *DependencyType*|*LayerName* requires that its associated artifacts must not depend on *NamespaceName*. *Artifact1* cannot depend on *Artifact2* because *Artifact2* is in *NamespaceName*.|
|AV1003: In Forbidden Namespace: *Artifact*(*ArtifactType*)<br /><br /> Layer: *LayerName* &#124; Forbidden Namespace: *NamespaceName*|*LayerName* requires that its associated artifacts cannot belong to *NamespaceName*. *Artifact* belongs to *NamespaceName*.|
|AV3001: Missing Link: Layer '*LayerName*' links to '*Artifact*' which cannot be found. 是否缺少程序集引用?|*LayerName* links to an artifact that cannot be found. 例如，由于建模项目缺少对包含某个类的程序集的引用，因此可能缺少指向该类的链接。|
|AV9001: 体系结构分析遇到了内部错误。 结果可能不完整。 有关详细信息，请参阅详细的生成事件日志或输出窗口。|有关更多详细信息，请参阅生成事件日志或输出窗口。|

## <a name="security"></a>安全

## <a name="see-also"></a>请参阅
 [在开发过程中验证系统](../modeling/validate-your-system-during-development.md)
