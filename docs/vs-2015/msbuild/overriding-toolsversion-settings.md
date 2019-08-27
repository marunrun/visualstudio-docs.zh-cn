---
title: 替代 ToolsVersion 设置 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, overriding ToolsVersion setting
- MSBuild, building solutions with
ms.assetid: ccd42c07-0fb6-4e8b-9ebb-a6a6db18aa2e
caps.latest.revision: 27
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 468561a627a3ad7eb477328b5afef794c7acf2c7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199946"
---
# <a name="overriding-toolsversion-settings"></a>重写 ToolsVersion 设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可使用以下三种方式之一来更改项目和解决方案的工具集：  
  
1. 在从命令行生成项目或解决方案时，使用 `/ToolsVersion` 开关（或简称为 `/tv`）  
  
2. 设置 MSBuild 任务的 `ToolsVersion` 参数  
  
3. 设置解决方案中某个项目的 `$(ProjectToolsVersion)` 参数。 使用此方法，可以在解决方案中使用不同于其他项目的工具集版本生成项目。  
  
## <a name="override-the-toolsversion-settings-of-projects-and-solutions-on-command-line-builds"></a>在命令行生成上替代项目和解决方案的 ToolsVersion 设置  
 虽然 Visual Studio 项目通常使用在项目文件中指定的 ToolsVersion 生成，但也可以使用命令行上的 `/ToolsVersion`（或 `/tv`）开关来替代该值，并用不同的工具集来生成所有项目及其项目到项目依赖项。 例如:  
  
```  
msbuild.exe someproj.proj /tv:12.0 /p:Configuration=Debug  
```  
  
 在此示例中，所有项目均使用 ToolsVersion 12.0 生成。 （但请参阅本主题后面的“优先级顺序”一节。）  
  
 使用命令行上的 `/tv` 开关时，可以选择在个别项目中使用 `$(ProjectToolsVersion)` 属性，使用与解决方案中的其他项目不同的 ToolsVersion 值来生成这些项目。  
  
## <a name="override-the-toolsversion-settings-using-the-toolsversion-parameter-of-the-msbuild-task"></a>使用 MSBuild 任务的 ToolsVersion 参数替代 ToolsVersion 设置  
 MSBuild 任务是一个项目生成另一个项目的主要方式。 为了使 MSBuild 任务能够使用与项目中指定的值不同的 ToolsVersion 来生成项目，它提供了名为 `ToolsVersion` 的可选任务参数。 下面的示例演示如何使用此参数：  
  
1. 创建一个名为 `projectA.proj` 的文件，在其中包含以下代码：  
  
    ```  
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
    ToolsVersion="12.0">  
  
        <Target Name="go" >   
            <Message Text="projectA.proj" />  
            <Message Text="MSBuildToolsVersion: $(MSBuildToolsVersion)" />  
            <Message Text="MSBuildToolsPath:    $(MSBuildToolsPath)" />  
  
            <MSBuild Projects="projectB.proj"  
                ToolsVersion="2.0"  
                Targets="go" />  
        </Target>  
    </Project>  
    ```  
  
2. 创建另一个名为 `projectB.proj` 的文件，在其中包含以下代码：  
  
    ```  
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
    ToolsVersion="12.0">  
  
        <Target Name="go">  
            <Message Text="projectB.proj" />  
            <Message Text="MSBuildToolsVersion: $(MSBuildToolsVersion)" />  
            <Message Text="MSBuildToolsPath:    $(MSBuildToolsPath)" />  
        </Target>  
    </Project>  
    ```  
  
3. 在命令提示符处输入以下命令：  
  
    ```  
    msbuild projectA.proj /t:go /toolsversion:3.5  
    ```  
  
4. 将显示以下输出。 对于 `projectA`，命令行上的 `/toolsversion:3.5` 设置将替代 `Project` 标记中的 `ToolsVersion=12.0` 设置。  
  
     `ProjectB` 由 `projectA` 中的任务调用。 该任务具有 `ToolsVersion=2.0`，替代了 `projectB` 的其他 `ToolsVersion` 设置。  
  
    ```  
    Output:  
      projectA.proj  
      MSBuildToolsVersion: 3.5  
      MSBuildToolsPath:    C:\Windows\Microsoft.NET\Framework\v3.5  
  
      projectB.proj  
      MSBuildToolsVersion: 2.0  
      MSBuildToolsPath:    C:\Windows\Microsoft.NET\Framework\v2.0.50727  
    ```  
  
## <a name="order-of-precedence"></a>优先级顺序  
 用于确定 `ToolsVersion` 的优先级顺序从高到低是：  
  
1. 用于生成项目的 MSBuild 任务的 `ToolsVersion` 属性（如果有）。  
  
2. msbuild.exe 命令中使用的 `/toolsversion`（或 `/tv`）开关（如果有）。  
  
3. 如果设置了环境变量 `MSBUILDTREATALLTOOLSVERSIONSASCURRENT`，则使用当前 `ToolsVersion`。  
  
4. 如果设置了环境变量 `MSBUILDTREATHIGHERTOOLSVERSIONASCURRENT` 且项目文件中定义的 `ToolsVersion` 大于当前 `ToolsVersion`，则使用当前 `ToolsVersion`。  
  
5. 如果设置了环境变量 `MSBUILDLEGACYDEFAULTTOOLSVERSION`，或者如果未设置 `ToolsVersion`，则使用以下步骤：  
  
    1. 项目文件的 [Project](../msbuild/project-element-msbuild.md) 元素的 `ToolsVersion` 属性。 如果此属性不存在，则假定是当前版本。  
  
    2. MSBuild.exe.config 文件中的默认工具版本。  
  
    3. 注册表中的默认工具版本。 有关详细信息，请参阅[标准和自定义工具集配置](../msbuild/standard-and-custom-toolset-configurations.md)。  
  
6. 如果未设置环境变量 `MSBUILDLEGACYDEFAULTTOOLSVERSION`，则使用以下步骤：  
  
    1. 如果环境变量 `MSBUILDDEFAULTTOOLSVERSION` 设置为现有的 `ToolsVersion`，请使用它。  
  
    2. 如果在 MSBuild.exe.config 中设置了 `DefaultOverrideToolsVersion`，请使用它。  
  
    3. 如果在注册表中设置了 `DefaultOverrideToolsVersion`，请使用它。  
  
    4. 否则，使用当前 `ToolsVersion`。  
  
## <a name="see-also"></a>另请参阅  
 [多目标](../msbuild/msbuild-multitargeting-overview.md)   
 [MSBuild 概念](../msbuild/msbuild-concepts.md)   
 [工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)   
 [标准和自定义工具集配置](../msbuild/standard-and-custom-toolset-configurations.md)
