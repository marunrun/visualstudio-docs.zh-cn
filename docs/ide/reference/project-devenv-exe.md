---
title: -Project (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /Project Devenv switch
- projects [Visual Studio], rebuilding
- projects [Visual Studio], building
- deployment projects, specifying
- Project Devenv switch (/Project)
- Devenv, /Project switch
- projects [Visual Studio], cleaning
ms.assetid: 8b07859c-3439-436d-9b9a-a8ee744eee30
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a4b57a5bd51ff20de8da87798aa398db04bc1c7d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75567770"
---
# <a name="project-devenvexe"></a>/Project (devenv.exe)

标识在指定解决方案配置中要生成、清理、重新生成或部署的单个项目。

## <a name="syntax"></a>语法

```shell
devenv SolutionName {/Build|/Clean|/Deploy|/Rebuild} [SolnConfigName [/Project ProjName [/ProjectConfig ProjConfigName]] [/Out OutputFilename]]
```

## <a name="arguments"></a>参数

- *SolutionName*

  必需。 解决方案文件的完整路径和名称。

- {`/Build`|`/Clean`|`/Deploy`|`/Rebuild`}

  必需。 [生成](build-devenv-exe.md)、[清理](clean-devenv-exe.md)、[部署](deploy-devenv-exe.md)或[重新生成](rebuild-devenv-exe.md)项目。

- *SolnConfigName*

  可选。 应用于 SolutionName`Debug``Release` 中命名的解决方案的解决方案配置的名称（如 *或*）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。 如果未指定此参数或字符串为空 (`""`)，工具便会使用解决方案的有效配置。

- `/Project` *ProjName*

  可选。 解决方案中项目文件的路径和名称。 可以将项目在 SolutionName  文件夹中的显示名称或相对路径输入到项目文件中。 也可以输入项目文件的完整路径和名称。

- `/ProjectConfig` *ProjConfigName*

  可选。 要应用于已命名 `Debug` 的项目生成配置名称（如 `Release` 或 `/Project`）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。

- `/Out` *OutputFilename*

  可选。 要将工具输出发送到的文件的文件名。 如果文件已有，工具将输出追加到文件末尾。

## <a name="remarks"></a>备注

- 必须用作 `devenv` `/Build`、`/Clean`、`/Rebuild` 或 `/Deploy` 命令的一部分。

- 用双引号将含有空格的字符串引起来。

- “命令”  窗口或使用 `/Out` 开关指定的任何日志文件中都可显示生成的摘要信息（包括错误）。

## <a name="example"></a>示例

下面的示例使用 `CSharpWinApp` 中的 `Debug` 项目生成配置来生成项目 `MySolution`。

```shell
devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>另请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [/ProjectConfig (devenv.exe)](../../ide/reference/projectconfig-devenv-exe.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Deploy (devenv.exe)](../../ide/reference/deploy-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
