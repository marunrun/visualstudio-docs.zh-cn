---
title: 使用依赖项关系图验证代码
ms.date: 09/28/2018
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams, validating
- validation, dependency diagrams
- validation, code
- code exploration, validating
- architecture, validating
- Visual Studio Ultimate, validating code
- validation, architecture
- validation, dependencies
- MSBuild, tasks
- MSBuild, dependency diagrams
- MSBuild, validating code
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 975fe8eac5657e245027a4811e50bbc93528cfe5
ms.sourcegitcommit: 273b657e115c1756adb84e0e56b6f2c709bcee76
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "80759697"
---
# <a name="validate-code-with-dependency-diagrams"></a>使用依赖项关系图验证代码

## <a name="why-use-dependency-diagrams"></a>为什么要使用依赖关系关系图？

为了确保代码不与其设计冲突，请使用 Visual Studio 中的依赖关系图验证代码。 这可帮助你：

- 查找代码中的依赖项与依赖关系关系关系图的依赖项之间的冲突。

- 查找建议的更改可能会影响的依赖项。

   例如，您可以编辑依赖关系关系图以显示潜在的体系结构更改，然后验证代码以查看受影响的依赖项。

- 将代码重构或迁移到其他设计。

   查找在将代码移动到其他体系结构时需要工作的代码或依赖项。

**要求**

- Visual Studio

  要为 .NET Core 项目创建依赖关系关系图，必须具有 Visual Studio 2019 版本 16.2 或更高版本。

- 具有具有依赖关系关系图的建模项目的解决方案。 此依赖关系关系图必须链接到要验证的 C# 或 Visual Basic 项目中的项目。 请参阅[从代码创建依赖关系关系图](../modeling/create-layer-diagrams-from-your-code.md)。

要查看哪些版本的 Visual Studio 支持此功能，请参阅[版本支持体系结构和建模工具](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

可以从 Visual Studio 中的打开依赖关系图或命令提示符手动验证代码。 您还可以在运行本地生成或 Azure 管道生成时自动验证代码。 请参阅[第 9 频道视频：使用依赖关系关系图设计和验证体系结构](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Using-layer-diagrams-to-design-and-validate-your-architecture)。

> [!IMPORTANT]
> 如果要使用团队基础服务器 （TFS） 运行图层验证，还必须在生成服务器上安装相同版本的 Visual Studio。

## <a name="live-dependency-validation"></a>实时依赖项验证

依赖项验证实时进行，错误将立即显示在**错误列表中**。

* 支持 C# 和可视化基本版的实时验证。

* 要在使用实时依赖项验证时启用完整的解决方案分析，请使用**错误列表**中显示的金条打开选项设置。

  - 如果您对解决方案中的所有体系结构问题不感兴趣，则可以永久关闭金条。
  - 如果不启用完整的解决方案分析，则仅针对正在编辑的文件执行分析。

* 升级项目以启用实时验证时，将显示转换的进度。

* 更新项目进行实时依赖项验证时，NuGet 包的版本将升级为对所有项目相同，并且是正在使用的最高版本。

* 添加新的依赖项验证项目将触发项目更新。

## <a name="see-if-an-item-supports-validation"></a>查看项是否支持验证

您可以将图层链接到网站、Office 文档、纯文本文件和跨多个应用共享的项目中的文件，但验证过程不包括它们。 如果引用的项目或程序集链接到单独的层，而且这些层之间没有依赖关系出现，则将不会出现验证错误。 除非代码使用此类引用，否则这些引用不被视为依赖项。

1. 在依赖关系关系图上，选择一个或多个图层，右键单击您的选择，然后单击"**查看链接**"。

2. 在**层资源管理器中**，查看 **"支持验证"** 列。 如果该值为 false，则项不支持验证。

## <a name="include-other-net-assemblies-and-projects-for-validation"></a>包括其他 .NET 程序集和项目以进行验证

将项目拖动到依赖关系关系图时，对相应的 .NET 程序集或项目的引用将自动添加到建模项目中的 **"图层引用"** 文件夹中。 此文件夹包含对验证过程中分析的程序集和项目的引用。 您可以包括其他 .NET 程序集和项目进行验证，而无需手动将它们拖动到依赖关系关系图。

1. 在**解决方案资源管理器**中，右键单击建模项目或**图层引用**文件夹，然后单击"**添加参考**"。

2. 在"**添加参考"** 对话框中，选择装配体或项目，然后单击"**确定**"。

## <a name="validate-code-manually"></a>手动验证代码

如果有链接到解决方案项的开放依赖关系关系图，则可以从关系图运行 **"验证**快捷方式"命令。 您还可以使用命令提示符运行**msbuild**命令，将 **/p：验证体系结构**自定义属性设置为**True**。 例如，在对代码进行更改时，请定期执行层验证以便能够提前捕获依赖项冲突。

### <a name="validate-code-from-an-open-dependency-diagram"></a>从打开的依赖关系关系图验证代码

1. 右键单击关系图曲面，然后单击 **"验证体系结构**"。

    > [!NOTE]
    > 默认情况下，依赖关系关系图 （.layer 关系图） 文件上的**生成操作**属性设置为 **"验证**"，以便该关系图包含在验证过程中。

     "**错误列表"** 窗口报告发生的任何错误。 有关验证错误的详细信息，请参阅[排除层验证问题。](#troubleshoot-layer-validation-issues)

2. 要查看每个错误的源，请在 **"错误列表"** 窗口中双击错误。

    > [!NOTE]
    > Visual Studio 可能会显示代码映射，而不是错误源。 当代码对依赖关系关系图未指定的程序集具有依赖项，或者代码缺少依赖关系关系图指定的依赖项时，将发生这种情况。 检查代码映射或代码，以确定此依赖关系是否应该存在。 有关代码映射的详细信息，请参阅[解决方案中的映射依赖项](../modeling/map-dependencies-across-your-solutions.md)。

3. 要管理错误，请参阅[解决图层验证错误](#resolve-layer-validation-errors)。

### <a name="validate-code-at-the-command-prompt"></a>在命令提示符处验证代码

1. 打开可视化工作室命令提示符。

2. 选择以下选项之一：

   - 要根据解决方案中的特定建模项目验证代码，请使用以下自定义属性运行 MSBuild。

       ```
       msbuild <FilePath+ModelProjectFileName>.modelproj /p:ValidateArchitecture=true
       ```

     - 或 -

       浏览到包含建模项目 （.modelproj） 文件和依赖关系关系图的文件夹，然后使用以下自定义属性运行 MSBuild：

       ```
       msbuild /p:ValidateArchitecture=true
       ```

   - 要针对解决方案中的所有建模项目验证代码，请使用以下自定义属性运行 MSBuild：

       ```
       msbuild <FilePath+SolutionName>.sln /p:ValidateArchitecture=true
       ```

     - 或 -

       浏览到解决方案文件夹，该文件夹必须包含包含依赖关系关系图的建模项目，然后使用以下自定义属性运行 MSBuild：

       ```
       msbuild /p:ValidateArchitecture=true
       ```

     将列出发生的任何错误。 有关 MSBuild 的详细信息，请参阅[MSBuild](../msbuild/msbuild.md)和[MSBuild 任务](../msbuild/msbuild-task.md)。

   有关验证错误的详细信息，请参阅[排除层验证问题。](#troubleshoot-layer-validation-issues)

### <a name="manage-validation-errors"></a>管理验证错误

在开发过程中，你可能需要在验证期间禁止显示报告的某些冲突。 例如，你可能希望禁止显示你已解决或与特定情形不相关的错误。 当您抑制错误时，最好在团队基础中记录工作项。

> [!WARNING]
> 必须已连接到 TFS 源代码管理 (SCC) 才可创建或链接到工作项。 如果尝试打开到其他 TFS SCC 的连接，则 Visual Studio 会自动关闭当前解决方案。 请先确保已连接到相应的 SCC，然后再尝试创建或链接到工作项。 在更高版本的 Visual Studio 中，如果未连接到 SCC，则菜单命令不可用。

#### <a name="create-a-work-item-for-a-validation-error"></a>为验证错误创建工作项

- 在 **"错误列表"** 窗口中，右键单击错误，指向 **"创建工作项**"，然后单击要创建的工作项的类型。

使用这些任务在 **"错误列表"** 窗口中管理验证错误：

|**自**|**按照以下步骤操作**|
|-|-|
|禁止在验证过程中显示选定的错误|右键单击一个或多个选定的错误，指向**管理验证错误**，然后单击 **"禁止错误**"。<br /><br /> 禁止显示的错误在显示时均带有删除线格式。 在你下次运行验证时，这些错误将不会显示。<br /><br /> 在相应的依赖关系关系图文件中跟踪抑制错误。|
|停止禁止显示选定的错误|右键单击所选抑制错误或错误，指向**管理验证错误**，然后单击"**停止禁止错误**"。<br /><br /> 在你下次运行验证时，这些所选的禁止显示的错误将会显示。|
|在 **"错误列表"** 窗口中还原所有已抑制的错误|右键单击 **"错误列表"** 窗口中的任意位置，指向 **"管理验证错误**"，然后单击"**显示所有压缩错误**"。|
|从 **"错误列表"** 窗口隐藏所有已抑制的错误|右键单击 **"错误列表"** 窗口中的任意位置，指向 **"管理验证错误**"，然后单击"**隐藏所有抑制错误**"。|

## <a name="validate-code-automatically"></a>自动验证代码

每次运行本地生成时，都可以执行层验证。 如果团队使用 Azure DevOps，则可以使用封闭签入执行图层验证，可以通过创建自定义 MSBuild 任务来指定该值，并使用生成报告收集验证错误。 要创建门控签入生成，请参阅[TFVC 门控签入](/azure/devops/pipelines/build/triggers)。

### <a name="to-validate-code-automatically-during-a-local-build"></a>在本地生成期间自动验证代码

使用文本编辑器打开建模项目 (.modelproj) 文件，然后包括以下属性：

```xml
<ValidateArchitecture>true</ValidateArchitecture>
```

\- 或 -

1. 在**解决方案资源管理器**中，右键单击包含依赖关系关系图或关系图的建模项目，**然后单击属性**。

2. 在 **"属性"** 窗口中，将建模项目的 **"验证体系结构"** 属性设置为**True**。

    这将在验证过程中包括建模项目。

3. 在**解决方案资源管理器中**，单击要用于验证的依赖关系图 （.layer 关系图）文件。

4. 在 **"属性"** 窗口中，请确保关系图的**生成操作**属性设置为 **"验证**"。

    这包括验证过程中的依赖关系图。

要在"错误列表"窗口中管理错误，请参阅[解决图层验证错误](#resolve-layer-validation-errors)。

## <a name="troubleshoot-layer-validation-issues"></a>层验证问题疑难解答

下表描述了层验证问题及其解决方法。 这些问题不同于代码与设计发生冲突而导致出现的错误。 有关这些错误的详细信息，请参阅[排除层验证问题。](#troubleshoot-layer-validation-issues)

|**问题**|**可能的原因**|**分辨率**|
|-|-|-|
|验证错误不按预期发生。|验证不适用于从解决方案资源管理器中的其他依赖关系关系关系图复制且位于同一建模项目中的依赖关系关系关系图。 以这种方式复制的依赖关系关系图包含与原始依赖关系关系图相同的引用。|向建模项目添加新的依赖关系关系图。<br /><br /> 将元素从源依赖关系关系关系图复制到新关系图。|

## <a name="resolve-layer-validation-errors"></a>解决层验证错误

当您根据依赖关系关系图验证代码时，当代码与设计冲突时，将发生验证错误。 例如，以下情况可能导致发生验证错误：

- 将项目指派给了错误的层。 在这种情况下，请移动项目。

- 项目（例如类）以与你的体系结构相冲突的方式使用了其他类。 在这种情况下，请重构代码以移除依赖关系。

若要解决这些错误，请更新代码，直至验证过程中不出现其他错误为止。 可以反复执行此任务。

以下各节描述这些错误中使用的语法，解释了这些错误的含义，并提供了纠正或管理这些错误的方法。

|**语法**|**说明**|
|-|-|
|*工件N*（*工件类型N*）|*工件N*是与依赖关系关系图上的图层关联的项目。<br /><br /> *工件类型N*是*工件N*的类型，例如**类**或**方法**，例如：<br /><br /> MySolution.MyProject.MyClass.MyMethod(Method)|
|*NamespaceNameN*|命名空间的名称。|
|*LayerNameN*|依赖关系关系图上图层的名称。|
|*DependencyType*|*项目 1*和*工件 2*之间的依赖关系类型。 例如，*工件1*与*工件2*具有**调用**关系。|

| **错误语法** | **错误说明** |
|-|-|
| DV0001：**无效依赖项** | 当映射到图层的代码元素（命名空间、类型、成员）引用映射到另一个图层的代码元素时，将报告此问题，但在包含此图层的依赖项验证图中这些图层之间没有依赖关系箭头。 这是依赖项约束冲突。 |
| DV1001：**无效的命名空间名称** | 此问题报告在与"允许命名名称"属性不包含定义此代码元素的命名空间的层关联的代码元素上。 这是命名约束冲突。 请注意，"允许的命名名称"的语法是允许定义与图层关联的代码元素的命名空间的分号列表。 |
| DV1002：**对不可引用命名空间的依赖** | 此问题报告在与图层关联的代码元素上，并引用在命名空间中定义的另一个代码元素，该代码元素在图层的"不可引用命名空间"属性中定义。 这是命名约束冲突。 请注意，"不可引用的命名空间"属性定义为不应在与此图层关联的代码元素中引用的命名空间的分号分隔列表。 |
| DV1003：**不允许命名空间名称** | 此问题报告在与"不允许命名名称"属性包含定义此代码元素的命名空间的图层关联的代码元素上。 这是命名约束冲突。 请注意，"不允许命名空间名称"属性定义为不应在此层关联的代码元素的命名空间的分号分隔列表。 |
| DV2001：**层图存在** | 此问题报告在不包含依赖关系关系关系关系图文件但引用依赖项验证分析器的项目上。 如果未使用依赖项验证，则可以直接从解决方案资源管理器中删除"Microsoft.依赖验证.分析器"或禁止此警告。 要添加依赖关系关系关系图，请参阅[从代码创建依赖关系关系关系图](../modeling/create-layer-diagrams-from-your-code.md)。 |
| DV2002：**未映射类型库** | 当代码元素未映射到任何图层时，将报告此问题。 |
| DV3001：**缺少链接** | 图层 "*图层名称*"链接到找不到的"*工件*"。 是否缺少程序集引用? |
| DV9001：**架构分析发现内部错误** | 结果可能不完整。 有关详细信息，请参阅详细的生成事件日志或输出窗口。 |

## <a name="see-also"></a>另请参阅

- [可视化工作室中的实时依赖项验证](https://devblogs.microsoft.com/devops/live-dependency-validation-in-visual-studio-2017/)
- [在开发过程中验证系统](../modeling/validate-your-system-during-development.md)
- [视频：实时验证体系结构依赖关系](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)
