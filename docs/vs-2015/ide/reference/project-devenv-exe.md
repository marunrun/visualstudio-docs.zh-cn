---
title: -Project (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /project Devenv switch
- projects [Visual Studio], rebuilding
- projects [Visual Studio], building
- deployment projects, specifying
- project Devenv switch (/project)
- Devenv, /project switch
- projects [Visual Studio], cleaning
ms.assetid: 8b07859c-3439-436d-9b9a-a8ee744eee30
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7f9c54691ed343493ef1e43798faf4d2ab6f60fb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662112"
---
# <a name="project-devenvexe"></a>/Project (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

标识在指定解决方案配置中要生成、清理、重新生成或部署的单个项目。

## <a name="syntax"></a>语法

```
devenv SolutionName {/build|/clean|/rebuild|/deploy} SolnConfigName
[/project ProjName] [/projectconfig ProjConfigName]
```

## <a name="arguments"></a>自变量
 /build 生成 `/project` `ProjName` 指定的项目。

 /clean 清除在生成过程中创建的所有中间文件和输出目录。

 然后，/rebuild 清理生成 `/project` `ProjName` 指定的项目。

 /deploy 指定在生成或重新生成后部署项目。

 `SolnConfigName`（必需）。 将应用于 `SolutionName` 中命名的解决方案的解决方案配置的名称。

 `SolutionName`（必需）。 解决方案文件的完整路径和名称。

 /project `ProjName`（可选）。 解决方案中项目文件的路径和名称。 可以输入从 `SolutionName` 文件夹到项目文件的相对路径、项目的显示名称或项目文件的完整路径和名称。

 /projectconfig `ProjConfigName`（可选）。 要应用于已命名的 `/project` 的项目生成配置的名称。

## <a name="remarks"></a>备注

- 必须使用部分 `devenv /build`、/`clean`、`/rebuild` 或 `/deploy` 命令。

- 用双引号将含有空格的字符串引起来。

- “命令”  窗口或使用 `/out` 开关指定的任何日志文件中都可显示生成的摘要信息（包括错误）。

## <a name="example"></a>示例
 本示例使用 `MySolution` 的 `Debug` 解决方案配置中的 `Debug` 项目生成配置来生成 `CSharpConsoleApp` 项目。

```
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>另请参阅
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md) [/ProjectConfig （devenv）](../../ide/reference/projectconfig-devenv-exe.md) [/Build （node.js）](../../ide/reference/build-devenv-exe.md) [/Clean （](../../ide/reference/clean-devenv-exe.md) devenv） [/Rebuild （devenv](../../ide/reference/rebuild-devenv-exe.md) ） [/Deploy （devenv](../../ide/reference/deploy-devenv-exe.md) ） [/out （devenv）](../../ide/reference/out-devenv-exe.md)
