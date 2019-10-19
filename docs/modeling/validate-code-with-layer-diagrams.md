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
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4a2b972c3c275f3e43819220532ac0a3c4a597e3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662938"
---
# <a name="validate-code-with-dependency-diagrams"></a>使用依赖项关系图验证代码

## <a name="why-use-dependency-diagrams"></a>为什么要使用依赖关系图？

若要确保代码不会与设计发生冲突，请通过 Visual Studio 中的依赖项关系图验证代码。 这可帮助你：

- 查找你的代码中的依赖项与依赖关系图上的依赖项之间的冲突。

- 查找建议的更改可能会影响的依赖项。

   例如，您可以编辑依赖关系图以显示潜在的体系结构更改，然后验证代码以查看受影响的依赖项。

- 将代码重构或迁移到其他设计。

   查找在将代码移动到其他体系结构时需要工作的代码或依赖项。

**惠?**

- Visual Studio

  若要创建 .NET Core 项目的依赖项关系图，必须安装有 Visual Studio 2019 版本16.2 或更高版本。

- 具有具有依赖关系图的建模项目的解决方案。 此依赖关系关系图必须链接到或C# Visual Basic 要验证的项目中的项目。 请参阅[通过代码创建依赖关系图](../modeling/create-layer-diagrams-from-your-code.md)。

若要查看支持此功能的 Visual Studio 版本，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

你可以在 Visual Studio 中打开的依赖项关系图中或从命令提示符手动验证代码。 你还可以在运行本地生成或 Azure Pipelines 生成时自动验证代码。 请参阅第[9 频道视频：使用依赖关系图设计和验证体系结构](http://go.microsoft.com/fwlink/?LinkID=252073)。

> [!IMPORTANT]
> 如果要使用 Team Foundation Server （TFS）运行层验证，则还必须在生成服务器上安装相同版本的 Visual Studio。

## <a name="live-dependency-validation"></a>实时依赖项验证

依赖项验证会实时发生，错误会立即显示在**错误列表**中。

* 支持实时验证C#和 Visual Basic。

* 若要在使用实时依赖项验证时启用完整解决方案分析，请从 "**错误列表**" 中显示的 "黄金" 栏中打开 "选项" 设置。

  - 如果你不想查看解决方案中的所有体系结构问题，则可以永久消除黄金条。
  - 如果未启用完整解决方案分析，则只对正在编辑的文件进行分析。

* 升级项目以启用实时验证时，会出现一个对话框，其中显示了转换的进度。

* 更新项目以进行实时依赖项验证时，NuGet 包的版本升级为对所有项目均相同，并且是所使用的最高版本。

* 添加新的依赖项验证项目会触发项目更新。

## <a name="see-if-an-item-supports-validation"></a>查看项是否支持验证

你可以将层链接到网站、Office 文档、纯文本文件和项目中跨多个应用共享的文件，但验证过程不包含这些文件。 如果引用的项目或程序集链接到单独的层，而且这些层之间没有依赖关系出现，则将不会出现验证错误。 除非代码使用此类引用，否则这些引用不被视为依赖项。

1. 在依赖项关系图上，选择一个或多个层，右键单击所选内容，然后单击 "**查看链接**"。

2. 在 "**层资源管理器**" 中，查看 "**支持验证**" 列。 如果该值为 false，则项不支持验证。

## <a name="include-other-net-assemblies-and-projects-for-validation"></a>包括其他 .NET 程序集和项目以进行验证

将项拖动到依赖关系图中时，会自动将对相应 .NET 程序集或项目的引用添加到建模项目中的 "**层引用**" 文件夹。 此文件夹包含对验证过程中分析的程序集和项目的引用。 可以包含其他 .NET 程序集和项目进行验证，而无需手动将其拖到依赖关系图。

1. 在**解决方案资源管理器**中，右键单击建模项目或 "**层引用**" 文件夹，然后单击 "**添加引用**"。

2. 在 "**添加引用**" 对话框中，选择程序集或项目，然后单击 **"确定"** 。

## <a name="validate-code-manually"></a>手动验证代码

如果已打开一个链接到解决方案项的依赖项关系图，则可以从关系图中运行 "**验证**" 快捷方式命令。 你还可以使用命令提示符运行**msbuild**命令，并将 **/p： ValidateArchitecture**自定义属性设置为**True**。 例如，在对代码进行更改时，请定期执行层验证以便能够提前捕获依赖项冲突。

### <a name="validate-code-from-an-open-dependency-diagram"></a>从打开的依赖项关系图验证代码

1. 右键单击关系图图面，然后单击 "**验证体系结构**"。

    > [!NOTE]
    > 默认情况下，依赖关系关系图（. microsoft.visualstudio.teamarchitect.layerdesigner.diagrams.layerdiagram.show）文件的 "**生成操作**" 属性设置为 "**验证**"，以使关系图包含在验证过程中。

     "**错误列表**" 窗口将报告发生的任何错误。 有关验证错误的详细信息，请参阅[排除层验证问题](#troubleshoot-layer-validation-issues)。

2. 若要查看每个错误的源，请在 "**错误列表**" 窗口中双击错误。

    > [!NOTE]
    > Visual Studio 可能会显示代码图，而不是错误的源。 当代码依赖于依赖关系图未指定的程序集时，或者代码缺少依赖项关系图指定的依赖项时，会发生这种情况。 检查代码映射或代码，以确定此依赖关系是否应该存在。 有关代码图的详细信息，请参阅[映射解决方案之间的依赖关系](../modeling/map-dependencies-across-your-solutions.md)。

3. 若要管理错误，请参阅[解决层验证错误](#resolve-layer-validation-errors)。

### <a name="validate-code-at-the-command-prompt"></a>在命令提示符下验证代码

1. 打开 Visual Studio 命令提示符。

2. 选择以下选项之一：

   - 若要针对解决方案中的特定建模项目验证代码，请使用以下自定义属性运行 MSBuild。

       ```
       msbuild <FilePath+ModelProjectFileName>.modelproj /p:ValidateArchitecture=true
       ```

     - 或 -

       浏览到包含建模项目（.modelproj）文件和依赖关系图的文件夹，然后运行具有以下自定义属性的 MSBuild：

       ```
       msbuild /p:ValidateArchitecture=true
       ```

   - 若要针对解决方案中的所有建模项目验证代码，请运行包含以下自定义属性的 MSBuild：

       ```
       msbuild <FilePath+SolutionName>.sln /p:ValidateArchitecture=true
       ```

     - 或 -

       浏览到解决方案文件夹，该文件夹必须包含一个包含依赖关系图的建模项目，然后使用以下自定义属性运行 MSBuild：

       ```
       msbuild /p:ValidateArchitecture=true
       ```

     将列出发生的任何错误。 有关 MSBuild 的详细信息，请参阅[msbuild](../msbuild/msbuild.md)和[msbuild 任务](../msbuild/msbuild-task.md)。

   有关验证错误的详细信息，请参阅[排除层验证问题](#troubleshoot-layer-validation-issues)。

### <a name="manage-validation-errors"></a>管理验证错误

在开发过程中，你可能需要在验证期间禁止显示报告的某些冲突。 例如，你可能希望禁止显示你已解决或与特定情形不相关的错误。 当您禁止显示错误时，最好是在 Team Foundation 中记录工作项。

> [!WARNING]
> 必须已连接到 TFS 源代码管理 (SCC) 才可创建或链接到工作项。 如果尝试打开到其他 TFS SCC 的连接，则 Visual Studio 会自动关闭当前解决方案。 请先确保已连接到相应的 SCC，然后再尝试创建或链接到工作项。 在更高版本的 Visual Studio 中，如果未连接到 SCC，则菜单命令不可用。

#### <a name="create-a-work-item-for-a-validation-error"></a>为验证错误创建工作项

- 在 "**错误列表**" 窗口中，右键单击错误，指向 "**创建工作项**"，然后单击要创建的工作项的类型。

使用以下任务来管理**错误列表**窗口中的验证错误：

|**若要**|**请按照以下步骤操作**|
|-|-|
|禁止在验证过程中显示选定的错误|右键单击一个或多个选定的错误，指向 "**管理验证错误**"，然后单击 "**取消错误**"。<br /><br /> 禁止显示的错误在显示时均带有删除线格式。 在你下次运行验证时，这些错误将不会显示。<br /><br /> 对于相应的依赖关系关系图文件，禁止显示隐藏的错误。|
|停止禁止显示选定的错误|右键单击选定的抑制错误或错误，指向 "**管理验证错误**"，然后单击 "**停止禁止显示错误**"。<br /><br /> 在你下次运行验证时，这些所选的禁止显示的错误将会显示。|
|在**错误列表**窗口中还原所有禁止显示的错误|右键单击 "**错误列表**" 窗口中的任意位置，指向 "**管理验证错误**"，然后单击 "**显示所有禁止显示的错误**"。|
|从 "**错误列表**" 窗口中隐藏所有禁止显示的错误|右键单击 "**错误列表**" 窗口中的任意位置，指向 "**管理验证错误**"，然后单击 "**隐藏所有禁止显示的错误**"。|

## <a name="validate-code-automatically"></a>自动验证代码

每次运行本地生成时，都可以执行层验证。 如果你的团队使用 Azure DevOps，则可以使用封闭签入来执行层验证，可以通过创建自定义 MSBuild 任务来指定，并使用生成报告来收集验证错误。 若要创建封闭签入生成，请参阅[TFVC 封闭签入](/azure/devops/pipelines/build/triggers#gated)。

### <a name="to-validate-code-automatically-during-a-local-build"></a>在本地生成期间自动验证代码

使用文本编辑器打开建模项目 (.modelproj) 文件，然后包括以下属性：

```xml
<ValidateArchitecture>true</ValidateArchitecture>
```

\- 或 -

1. 在**解决方案资源管理器**中，右键单击包含依赖关系图或关系图的建模项目，然后单击 "**属性**"。

2. 在 "**属性**" 窗口中，将建模项目的 "**验证体系结构**" 属性设置为 " **True**"。

    这将在验证过程中包括建模项目。

3. 在**解决方案资源管理器**中，单击要用于验证的依赖项关系图（microsoft.visualstudio.teamarchitect.layerdesigner.diagrams.layerdiagram.show）文件。

4. 在 "**属性**" 窗口中，确保已将关系图的 "**生成操作**" 属性设置为 "**验证**"。

    这包括验证过程中的依赖关系图。

若要在错误列表 "窗口中管理错误，请参阅[解决层验证错误](#resolve-layer-validation-errors)。

## <a name="troubleshoot-layer-validation-issues"></a>层验证问题疑难解答

下表描述了层验证问题及其解决方法。 这些问题不同于代码与设计发生冲突而导致出现的错误。 有关这些错误的详细信息，请参阅[排除层验证问题](#troubleshoot-layer-validation-issues)。

|**问题**|**可能的原因**|**解决方法**|
|-|-|-|
|验证错误不按预期发生。|验证不适用于从解决方案资源管理器中的其他依赖关系图复制到同一建模项目中的依赖关系图。 以这种方式复制的依赖项关系图包含与原始依赖关系图相同的引用。|将新的依赖关系图添加到建模项目。<br /><br /> 将源依赖关系图中的元素复制到新关系图中。|

## <a name="resolve-layer-validation-errors"></a>解决层验证错误

根据依赖关系图验证代码时，如果代码与设计发生冲突，则会发生验证错误。 例如，以下情况可能导致发生验证错误：

- 将项目指派给了错误的层。 在这种情况下，请移动项目。

- 项目（例如类）以与你的体系结构相冲突的方式使用了其他类。 在这种情况下，请重构代码以移除依赖关系。

若要解决这些错误，请更新代码，直至验证过程中不出现其他错误为止。 可以反复执行此任务。

以下各节描述这些错误中使用的语法，解释了这些错误的含义，并提供了纠正或管理这些错误的方法。

|**语法**|**描述**|
|-|-|
|*ArtifactN*（*ArtifactTypeN*）|*ArtifactN*是与依赖关系图上的层关联的项目。<br /><br /> *ArtifactTypeN*是*ArtifactN*的类型，例如**类**或**方法**，例如：<br /><br /> MySolution.MyProject.MyClass.MyMethod(Method)|
|*NamespaceNameN*|命名空间的名称。|
|*LayerNameN*|依赖关系图层的名称。|
|*DependencyType*|*Artifact1*和*Artifact2*之间的依赖关系的类型。 例如， *Artifact1*具有与*Artifact2*的**调用**关系。|

| **Error 语法** | **错误描述** |
|-|-|
| DV0001：**依赖关系无效** | 当映射到层的代码元素（命名空间、类型、成员）引用映射到另一层的代码元素时，将报告此问题，但在包含此层的依赖项验证关系图中，这些层之间没有依赖项箭头。 这是依赖项约束冲突。 |
| DV1001：**无效的命名空间名称** | 此问题将在与 "允许的命名空间名称" 属性不包含定义此代码元素的命名空间的层关联的代码元素上报告。 这是一个命名约束冲突。 请注意，"允许的命名空间名称" 的语法应为命名空间的分号列表，在这些命名空间中，将允许定义与关联的代码元素。 |
| DV1002：**依赖不可引用命名空间** | 此问题在与层关联的代码元素上报告，并引用在层的 "不可引用 Namespace" 属性中定义的命名空间中定义的另一个代码元素。 这是一个命名约束冲突。 请注意，"不可引用命名空间" 属性定义为不应在与此层关联的代码元素中引用的以分号分隔的命名空间列表。 |
| DV1003：不**允许的命名空间名称** | 此问题将在与 "不允许的命名空间名称" 属性包含定义此代码元素的命名空间的层关联的代码元素上报告。 这是一个命名约束冲突。 请注意，"不允许的命名空间名称" 属性定义为分号分隔的命名空间列表，其中不应定义与此层关联的代码元素。 |
| DV3001：**缺少链接** | 层 "*LayerName*" 链接到了找不到的 "*项目*"。 是否缺少程序集引用? |
| DV9001：**体系结构分析找到内部错误** | 结果可能不完整。 有关详细信息，请参阅详细的生成事件日志或输出窗口。 |

## <a name="see-also"></a>请参阅

- [Visual Studio 中的实时依赖项验证](https://devblogs.microsoft.com/devops/live-dependency-validation-in-visual-studio-2017/)
- [在开发过程中验证系统](../modeling/validate-your-system-during-development.md)
- [视频：实时验证你的体系结构依赖关系](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)
