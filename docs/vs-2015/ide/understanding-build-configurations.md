---
title: 了解生成配置 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
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
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f3b4898166ec24cb429463f55f8b166056123e78
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65683862"
---
# <a name="understanding-build-configurations"></a>了解生成配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以存储不同的解决方案配置和项目属性以便在各种生成中使用。 若要创建、选择、修改或删除配置，可以使用“配置管理器”。 若要打开它，请在菜单栏上依次选择“生成”和“配置管理器”，或在“快速启动”框中键入“配置”。 也可以使用“标准”工具栏上的“解决方案配置”列表，选择配置或打开“配置管理器”。  
  
> [!NOTE]
> 如果在工具栏上找不到解决方案配置设置且无法访问“配置管理器”，[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 开发设置可能适用。 有关详细信息，请参阅[如何：管理配置应用的 Visual Basic 开发人员设置](../ide/how-to-manage-build-configurations-with-visual-basic-developer-settings-applied.md)。  
  
 默认情况下，调试和发布配置包含在使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 模板创建的项目中。 调试配置支持应用的调试，而发布配置生成可部署的应用版本。 有关详细信息，请参阅[如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)。 还可以创建自定义解决方案配置和项目配置。 有关详细信息，请参阅[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)。  
  
## <a name="solution-configurations"></a>解决方案配置  
 解决方案配置指定如何生成和部署解决方案中的项目。 若要修改解决方案配置或定义新的配置，请在“配置管理器”中的“活动解决方案配置”下，选择“编辑”或“新建”。  
  
 解决方案配置的“项目上下文”框中的每个条目均表示解决方案中的一个项目。 对于“活动解决方案配置”和“活动解决方案平台”的每个组合，都可以设置每个项目的使用方式。 （有关解决方案平台的详细信息，请参阅[了解生成平台](../ide/understanding-build-platforms.md)。）  
  
> [!NOTE]
> 在定义新的解决方案配置并选中“创建新的项目配置”复选框后，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 会自动将新的配置分配给所有项目。 同样，在定义新的解决方案平台并选中“创建新的项目平台”复选框后，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 也会自动将新的平台分配给所有项目。 此外，如果您添加一个面向新平台的项目，则 Visual Studio 会将该平台添加到解决方案平台列表中并将其分配给所有项目。  
>   
> 您仍可以修改每个项目的设置。  
  
 活动解决方案配置还为 IDE 提供了上下文。 例如，如果处理的是项目，并且配置指定将针对移动设备生成，那么“工具箱”只会显示可在移动设备项目中使用的项。  
  
## <a name="project-configurations"></a>项目配置  
 项目针对的配置和平台结合使用以指定在生成时要使用的属性。 对于配置和平台的每种组合，项目可以具有一组不同的属性定义。 若要修改项目的属性，可以使用其属性页。 （在“解决方案资源管理器”中，打开项目的快捷菜单，然后选择“属性”。）  
  
 对于每个项目配置，您可以根据需要定义配置相关属性。 例如，对于特定生成，您可以设置将包含哪些项目项、将创建哪些输出文件、在何处放置这些文件以及如何对其进行优化。  
  
 项目配置可能相差很大。 例如，一个配置的属性可能指定优化其输出文件以占用最小空间，而另一个配置可能指定其可执行文件以最快速度运行。  
  
 项目配置是按解决方案存储，而不是按用户存储，所以团队可以共享项目配置。  
  
 尽管项目依赖项与配置无关，但将只生成在活动解决方案配置中指定的项目。  
  
## <a name="how-visual-studio-assigns-project-configurations"></a>Visual Studio 如何分配项目配置  
 在定义新的解决方案配置且未复制现有配置中的设置时，Visual Studio 会使用以下标准来分配默认的项目配置。 按所示顺序对条件进行评估。  
  
1. 如果项目的配置名称 (*\<配置名称> \<平台名称>*) 与新解决方案配置的名称完全一致，就会分配相应的配置。 配置名称不区分大小写。  
  
2. 如果项目有一个与新解决方案配置的名称部分匹配的配置名称，则分配该配置，无论平台部分是否匹配。  
  
3. 如果仍没有匹配项，则分配项目中列出的第一个配置。  
  
## <a name="how-visual-studio-assigns-solution-configurations"></a>Visual Studio 如何分配解决方案配置  
 创建项目配置（在“配置管理器”中，在相应项目的“配置”列中选择下拉菜单中的“新建”）并选中“创建新的解决方案配置”复选框后，Visual Studio 会查找名称相似的解决方案配置，以在它支持的每个平台上生成项目。 在某些情况下，Visual Studio 会重命名现有解决方案配置或定义新的配置。  
  
 Visual Studio 使用以下标准来分配解决方案配置。  
  
- 如果项目配置未指定平台或仅指定一个平台，则将查找或添加一个其名称与新项目配置名称匹配的解决方案配置。 此解决方案配置的默认名称不包含平台名称，采用 *\<项目配置名称>* 的形式。  
  
- 如果项目支持多个平台，则可为每个受支持的平台找到或添加解决方案配置。 每个解决方案配置的名称均包含项目配置名称和平台名称，采用 *\<项目配置名称> \<平台名称>* 的形式。  
  
## <a name="see-also"></a>请参阅  
 [演练：生成应用程序](../ide/walkthrough-building-an-application.md)   
 [编译和生成](../ide/compiling-and-building-in-visual-studio.md)   
 [解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)   
 [C/C++ 生成参考](https://msdn.microsoft.com/library/100b4ccf-572c-4d1f-970c-fa0bc0cc0d2d)   
 [Devenv 命令行开关](../ide/reference/devenv-command-line-switches.md)
