---
title: -Clean (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- builds [Team System], cleaning files
- Clean Devenv switch
- /Clean Devenv switch
- Devenv, /Clean switch
ms.assetid: 79929dfd-22c9-4cec-a0d0-a16f15b8f7e4
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ac184f25d79a47814fee52b99bce1cddce247fc5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75570461"
---
# <a name="clean-devenvexe"></a>/Clean (devenv.exe)

清理所有中间文件和输出目录。

## <a name="syntax"></a>语法

```shell
devenv SolutionName /Clean [Config [/Project ProjName [/ProjectConfig ProjConfigName]] [/Out OutputFilename]]
```

## <a name="arguments"></a>自变量

- *SolutionName*

  必需。 解决方案文件的完整路径和名称。

- Config 

  可选。 用于为 SolutionName  中命名的解决方案清理中间文件的配置（如 `Debug` 或 `Release`）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。 如果未指定此参数或字符串为空 (`""`)，工具便会使用解决方案的有效配置。

- `/Project` *ProjName*

  可选。 解决方案中项目文件的路径和名称。 可以将项目在 SolutionName  文件夹中的显示名称或相对路径输入到项目文件中。 也可以输入项目文件的完整路径和名称。

- `/ProjectConfig` *ProjConfigName*

  可选。 要在清理已命名 `/Project` 时使用的项目生成配置的名称（如 `Debug` 或 `Release`）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。 如果此开关已指定，它会替代 Config  参数。

- `/Out` *OutputFilename*

  可选。 要将工具输出发送到的文件的文件名。 如果文件已有，工具将输出追加到文件末尾。

## <a name="remarks"></a>备注

在 IDE 中，此开关执行与“清理解决方案”  菜单命令相同的功能。

用双引号将含有空格的字符串引起来。

与清理和生成相关的摘要信息（包括错误）可以显示在“命令”  窗口中，也可以显示在使用 [/Out](out-devenv-exe.md) 开关指定的任何日志文件中。

如果 `/Project` 开关未指定，便会对解决方案中的所有项目完成清理操作，即使已将 FileName  指定为项目文件，也不例外。

## <a name="example"></a>示例

第一个示例使用解决方案文件中指定的默认配置清理 `MySolution` 解决方案。

第二个示例使用 `MySolution` 中的 `Debug` 项目生成配置来清理项目 `CSharpWinApp`。

```shell
devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /Clean

devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /Clean "Debug" /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig "Debug"
```

## <a name="see-also"></a>请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
