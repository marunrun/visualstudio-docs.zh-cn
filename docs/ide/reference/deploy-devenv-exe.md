---
title: -Deploy (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /Deploy switch
- Deploy Devenv switch
- deploying applications [Visual Studio], after build
- /Deploy Devenv switch
ms.assetid: e47c8723-df08-4645-aa2d-0c956e7ccca2
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8eeb1a03e584b0b39030ec56ca6945a2d5ced78
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75570123"
---
# <a name="deploy-devenvexe"></a>/Deploy (devenv.exe)

生成或重新生成后部署解决方案。 仅适用于托管代码项目。

## <a name="syntax"></a>语法

```shell
devenv SolutionName /Deploy [SolnConfigName [/Project ProjName [/ProjectConfig ProjConfigName]] [/Out OutputFilename]]
```

## <a name="arguments"></a>自变量

- *SolutionName*

  必需。 解决方案文件的完整路径和名称。

- *SolnConfigName*

  可选。 要用于生成 SolutionName  中命名的解决方案的解决方案配置的名称（如 `Debug` 或 `Release`）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。 如果未指定此参数或字符串为空 (`""`)，工具便会使用解决方案的有效配置。

- `/Project` *ProjName*

  可选。 解决方案中项目文件的路径和名称。 可以将项目在 SolutionName  文件夹中的显示名称或相对路径输入到项目文件中。 也可以输入项目文件的完整路径和名称。

- `/ProjectConfig` *ProjConfigName*

  可选。 要在生成已命名 `/Project` 时使用的项目生成配置的名称（如 `Debug` 或 `Release`）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。 如果此开关已指定，它会替代 SolnConfigName  参数。

- `/Out` *OutputFilename*

  可选。 要将工具输出发送到的文件的文件名。 如果文件已有，工具将输出追加到文件末尾。

## <a name="remarks"></a>备注

指定的项目必须是部署项目。 如果指定的项目不是部署项目，当已生成的项目进行传递以供部署时，便会失败并出现错误。

用双引号将含有空格的字符串引起来。

与生成相关的摘要信息（包括错误）可以显示在“命令”  窗口中，也可以显示在使用 [/Out](out-devenv-exe.md) 开关指定的任何日志文件中。

## <a name="example"></a>示例

下面的示例使用 `MySolution` 中的 `Release` 项目生成配置来部署项目 `CSharpWinApp`。

```shell
devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /deploy Release /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Release
```

## <a name="see-also"></a>请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [/Project (devenv.exe)](../../ide/reference/project-devenv-exe.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
