---
title: -ProjectConfig (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /projectconfig Devenv switch
- configurations, rebuilding
- deployment projects, creating
- configurations, cleaning
- deployment projects, specifying
- deployment projects, adding
- build configurations, specifying
- Devenv, /projectconfig switch
- projectconfig Devenv switch (/projectconfig)
- projects [Visual Studio], build configuration
- projects [Visual Studio], cleaning
ms.assetid: 6b54ef59-ffed-4f62-a645-1279ede97ebf
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a33c7cbaef473e75631bb4ac6c0d217198cbf250
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662089"
---
# <a name="projectconfig-devenvexe"></a>/ProjectConfig (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定生成、清理、重新生成或部署在 `/project` 参数中命名的项目时要应用的项目生成配置。

## <a name="syntax"></a>语法

```
devenv SolutionName {/build|/clean|/rebuild|/deploy} SolnConfigName [/project ProjName] [/projectconfig ProjConfigName]
```

## <a name="arguments"></a>参数
 /build 生成由指定的项目 `/project` `ProjName` 。

 /clean 清除在生成过程中创建的所有中间文件和输出目录。

 然后，/rebuild 清理生成由指定的项目 `/project` `ProjName` 。

 /deploy 指定在生成或重新生成后部署项目。

 `SolnConfigName`（必需）。 将应用于 `SolutionName` 中命名的解决方案的解决方案配置的名称。

 `SolutionName`（必需）。 解决方案文件的完整路径和名称。

 /project `ProjName`（可选）。 解决方案中项目文件的路径和名称。 可以输入从 `SolutionName` 文件夹到项目文件的相对路径、项目的显示名称或项目文件的完整路径和名称。

 /projectconfig `ProjConfigName`（可选）。 要应用于已命名的 `/project` 的项目生成配置的名称。

## <a name="remarks"></a>备注

- 必须作为 `devenv /build`、/`clean`、`/rebuild` 或 `/deploy` 命令的一部分与 `/project` 开关一起使用。

- 用双引号将含有空格的字符串引起来。

- 生成的摘要信息（包括错误）可以显示在 **命令** 窗口中，也可以显示在通过开关指定的任何日志文件中 `/out` 。

## <a name="example"></a>示例
 本示例使用 `MySolution` 的 `Debug` 解决方案配置中的 `Debug` 项目生成配置来生成 `CSharpConsoleApp` 项目。

```
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>另请参阅
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md) [/Project ( # A0) ](../../ide/reference/project-devenv-exe.md) [/Build ( # A1) ](../../ide/reference/build-devenv-exe.md) [/Clean ( # A2) ](../../ide/reference/clean-devenv-exe.md) [/Rebuild ( # A3) ](../../ide/reference/rebuild-devenv-exe.md) [/Deploy ( # A4) ](../../ide/reference/deploy-devenv-exe.md) [/out ( # A5) ](../../ide/reference/out-devenv-exe.md)
