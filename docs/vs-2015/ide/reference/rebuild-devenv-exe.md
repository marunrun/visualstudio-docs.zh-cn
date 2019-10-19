---
title: /Rebuild (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /rebuild switch
- rebuild Devenv switch (/rebuild)
- projects [Visual Studio], rebuilding
- /rebuild Devenv switch
- applications [Visual Studio], rebuilding
ms.assetid: c5a8a4bf-0e2b-46eb-a44a-8aeb29b92c32
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 008169829a6cf76e959d00f010959239a5f390b5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665650"
---
# <a name="rebuild-devenvexe"></a>/Rebuild (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

清理然后生成指定解决方案配置。

## <a name="syntax"></a>语法

```
devenv SolutionName /rebuild SolnConfigName [/project ProjName] [/projectconfig ProjConfigName]
```

## <a name="arguments"></a>自变量
 `SolnConfigName`（必需）。 用于重新生成在 `SolutionName` 中命名的解决方案的解决方案配置名称。

 `SolutionName`（必需）。 解决方案文件的完整路径和名称。

 /project `ProjName`（可选）。 解决方案中项目文件的路径和名称。 可以输入从 `SolutionName` 文件夹到项目文件的相对路径、项目的显示名称或项目文件的完整路径和名称。

 /projectconfig `ProjConfigName`（可选）。 重新生成命名的 `/project` 时要使用的项目生成配置的名称。

## <a name="remarks"></a>备注

- 在集成开发环境 (IDE) 中，此开关执行与“重新生成解决方案”菜单命令相同的功能  。

- 用双引号将含有空格的字符串引起来。

- “命令”窗口或使用 `/out` 开关指定的任何日志文件中都可显示清理和生成的摘要信息（包括错误）  。

## <a name="example"></a>示例
 本示例使用 `MySolution` 的 `Debug` 解决方案配置中的 `Debug` 项目生成配置来清理和重新生成 `CSharpWinApp` 项目。

```
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /rebuild Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>另请参阅
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md) [/Build （devenv）](../../ide/reference/build-devenv-exe.md) [/Clean （devenv](../../ide/reference/clean-devenv-exe.md) ） [/out （devenv](../../ide/reference/out-devenv-exe.md) ）
