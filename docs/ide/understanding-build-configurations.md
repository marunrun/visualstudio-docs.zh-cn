---
title: 了解生成配置
ms.date: 01/20/2020
ms.technology: vs-ide-compile
ms.topic: conceptual
f1_keywords:
- SolutionProperties.ActiveConfig
- vs.build.newprojectconfiguration
- vc.proj.configurationsctrl.multipleconfigs
- vs.build.editsolutionconfigurations
- vs.build.editprojectconfigurations
- vs.multipleconfigurations
- vs.build.newsolutionconfiguration
- VS.ConfigurationManager
- VS.MultipleConfig
helpviewer_keywords:
- solution build configurations, about build configurations
- build configurations
- project build configurations
- build configurations, advanced
- projects [Visual Studio], build configuration
- solutions [Visual Studio], build configuration
ms.assetid: 934c727d-3a22-429c-bd13-3552cecf2e24
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a37d4fa5dc92253b94dc64590c9df5fec7703ceb
ms.sourcegitcommit: b016ea260856264eee730ee8cbcab198314a7ece
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "77904160"
---
# <a name="understand-build-configurations"></a>了解生成配置

需要生成具有不同设置的项目时，生成配置是必备项。 例如，“调试”  和“发布”  是配置，在生成这些项时，将相应地使用不同的编译器选项。  一种配置处于活动状态，并显示在 IDE 顶部的命令栏中。

![活动配置](media/understanding-build-configurations/active-config.png)

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[在 Visual Studio for Mac 中生成配置](/visualstudio/mac/configurations)。

用于存储生成的输出文件的配置和平台控件。 通常，在 Visual Studio 生成项目时，会将输出放置在以活动配置命名的项目子文件夹中（例如，“bin/Debug/x86”  ），这是可以更改的。

可以在解决方案和项目级别创建自己的生成配置。 解决方案配置确定该配置处于活动状态时在生成中包含哪些项目。 将仅生成在活动解决方案配置中指定的项目。 如果在配置管理器中选择了多个目标平台，则将生成适用于该平台的所有项目。 项目配置确定生成项目时使用的生成设置和编译器选项。

若要创建、选择、修改或删除配置，可以使用“配置管理器”  。 若要打开它，请在菜单栏上选择“生成”   > “配置管理器”  ，或者直接在搜索框中键入“配置”  。 也可以使用“标准”  工具栏上的“解决方案配置”  列表，选择配置或打开“配置管理器”  。

![配置管理器](media/understanding-build-configurations/config-manager.png)

> [!NOTE]
> 如果在工具栏上找不到解决方案配置设置且无法访问“配置管理器”  ，[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 开发设置可能适用。 有关详细信息，请参阅[如何：在应用 Visual Basic 开发人员设置后管理生成配置](../ide/how-to-manage-build-configurations-with-visual-basic-developer-settings-applied.md)。

默认情况下，“调试”  和“发布”  配置包含在使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 模板创建的项目中。 “调试”  配置支持调试应用，而“发布”  配置生成可部署的应用的版本。 有关详细信息，请参阅[如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)。 还可以创建自定义解决方案配置和项目配置。 有关详细信息，请参阅[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)。

## <a name="solution-configurations"></a>解决方案配置

解决方案配置指定如何生成和部署解决方案中的项目。 若要修改解决方案配置或定义新的配置，请在“配置管理器”  中的“活动解决方案配置”  下，选择“编辑”  或“新建”  。

解决方案配置的“项目上下文”  框中的每个条目均表示解决方案中的一个项目。 对于“活动解决方案配置”  和“活动解决方案平台”  的每个组合，都可以设置每个项目的使用方式。 （有关解决方案平台的详细信息，请参阅[了解生成平台](../ide/understanding-build-platforms.md)。）

在定义新的解决方案配置并选中“创建新的项目配置”  复选框后，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会自动将新的配置分配给所有项目。 同样，在定义新的解决方案平台并选中“创建新的项目平台”  复选框后，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 也会自动将新的平台分配给所有项目。 此外，如果您添加一个面向新平台的项目，则 Visual Studio 会将该平台添加到解决方案平台列表中并将其分配给所有项目。 您仍可以修改每个项目的设置。

活动解决方案配置还为 IDE 提供了上下文。 例如，如果处理的是项目，并且配置指定将针对移动设备生成，那么“工具箱”  只会显示可在移动设备项目中使用的项。

## <a name="project-configurations"></a>项目配置

项目针对的配置和平台结合使用以指定在生成时要使用的生成设置和编译器选项。 对于配置和平台的每种组合，项目可以具有不同的设置。 要修改项目属性，请在“解决方案资源管理器”  中打开项目的快捷菜单，然后选择“属性”  。  在项目设计器的“生成”  选项卡的顶部，选择活动配置以编辑其生成设置。

![项目设计器配置](media/understanding-build-configurations/project-designer-configuration.png)

## <a name="building-multiple-configurations"></a>生成多个配置

使用“生成”   > “生成解决方案”  命令生成解决方案时，Visual Studio 只会生成活动配置。 将生成在该解决方案配置中指定的所有项目，并且生成的唯一项目配置是活动解决方案配置和活动解决方案平台中指定的项目配置，该配置在 Visual Studio 的工具栏中显示。 例如：“调试”  和“x86”  。 不会生成其他定义的配置和平台。

如果要在一个操作中生成多个配置和平台，可以使用 Visual Studio 中的“生成”   > “批生成”  选项。 若要访问此功能，请按 Ctrl  +Q  打开搜索框，然后输入 `Batch build`。 批生成并非适用于所有项目类型。 请参阅[如何：同时生成多个配置](how-to-build-multiple-configurations-simultaneously.md)。

## <a name="how-visual-studio-assigns-project-configurations"></a>Visual Studio 如何分配项目配置

在定义新的解决方案配置且未复制现有配置中的设置时，Visual Studio 会使用以下标准来分配默认的项目配置。 按所示顺序对条件进行评估。

1. 如果项目的配置名称 ( *\<配置名称> \<平台名称>* ) 与新解决方案配置的名称完全一致，就会分配相应的配置。 配置名称不区分大小写。

1. 如果项目有一个与新解决方案配置的名称部分匹配的配置名称，则分配该配置，无论平台部分是否匹配。

1. 如果仍没有匹配项，则分配项目中列出的第一个配置。

## <a name="how-visual-studio-assigns-solution-configurations"></a>Visual Studio 如何分配解决方案配置

创建项目配置（在“配置管理器”  中，在相应项目的“配置”  列中选择下拉菜单中的“新建”  ）并选中“创建新的解决方案配置”  复选框后，Visual Studio 会查找名称相似的解决方案配置，以在它支持的每个平台上生成项目。 在某些情况下，Visual Studio 会重命名现有解决方案配置或定义新的配置。

Visual Studio 使用以下标准来分配解决方案配置。

- 如果项目配置未指定平台或仅指定一个平台，则将查找或添加一个其名称与新项目配置名称匹配的解决方案配置。 此解决方案配置的默认名称不包含平台名称，采用 *\<项目配置名称>* 的形式。

- 如果项目支持多个平台，则可为每个受支持的平台找到或添加解决方案配置。 每个解决方案配置的名称均包含项目配置名称和平台名称，采用 *\<项目配置名称> \<平台名称>* 的形式。

## <a name="see-also"></a>请参阅

- [演练：构建应用程序](../ide/walkthrough-building-an-application.md)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
- [解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)
- [C/C++ 生成参考](/cpp/build/reference/c-cpp-building-reference)
- [了解生成平台](understanding-build-platforms.md)
- [生成配置 (Visual Studio for Mac)](/visualstudio/mac/configurations)
