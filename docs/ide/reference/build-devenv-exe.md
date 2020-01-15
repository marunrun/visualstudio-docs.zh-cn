---
title: -Build (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- builds, command-line
- /build Devenv switch
- Devenv, /build switch
- build Devenv switch
- command-line builds
ms.assetid: ced21627-7653-455b-8821-3e31c6a448cf
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1766fe22573554b41ebfaa38fbd9e8d6c90c5790
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595756"
---
# <a name="build-devenvexe"></a>/Build (devenv.exe)

使用指定解决方案配置文件来生成解决方案或项目。

## <a name="syntax"></a>语法

```shell
devenv SolutionName /Build [SolnConfigName [/Project ProjName [/ProjectConfig ProjConfigName]] [/Out OutputFilename]]
```

## <a name="arguments"></a>自变量

- *SolutionName*

  必需。 解决方案文件的完整路径和名称。

- *SolnConfigName*

  可选。 要用于生成 SolutionName  中命名的解决方案的解决方案配置的名称（如 `Debug` 或 `Release`）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。 如果未指定此参数或字符串为空 (`""`)，工具便会使用解决方案的有效配置。

- `/Project` *ProjName*

  可选。 解决方案中项目文件的路径和名称。 可以输入从 SolutionName 文件夹到项目文件的相对路径、项目的显示名称或项目文件的完整路径和名称  。

- `/ProjectConfig` *ProjConfigName*

  可选。 要在生成已命名项目时使用的项目生成配置的名称（如 `Debug` 或 `Release`）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。 如果此开关已指定，它会替代 SolnConfigName  参数。

- `/Out` *OutputFilename*

  可选。 要将工具输出发送到的文件的文件名。 如果文件已有，工具将输出追加到文件末尾。

## <a name="remarks"></a>备注

- 在集成开发环境 (IDE) 中，`/Build` 开关执行与“生成解决方案”  菜单命令相同的功能。

- 用双引号将含有空格的字符串引起来。

- 与生成相关的摘要信息（包括错误）可以显示在“命令”窗口中，也可以显示在使用 `/Out` 开关指定的任何日志文件中。

- `/Build` 开关仅生成自上次生成后发生变化的项目。 若要生成解决方案中的所有项目，请改用 [/rebuild](../../ide/reference/rebuild-devenv-exe.md)。

- 如果看到错误消息“项目配置无效”  ，请确保已指定解决方案平台或项目平台（例如，`Debug|Win32`）。

## <a name="example"></a>示例

下面的命令使用 `MySolution` 中的 `Debug` 项目生成配置来生成项目 `CSharpWinApp`。

```shell
devenv "%USERPROFILE%\source\repos\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>请参阅

- [生成并清理项目和解决方案](../../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
