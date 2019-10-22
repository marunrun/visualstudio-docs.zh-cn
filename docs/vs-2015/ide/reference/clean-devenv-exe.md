---
title: -Clean (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- builds [Team System], cleaning files
- clean Devenv switch
- /clean Devenv switch
- Devenv, /clean switch
ms.assetid: 79929dfd-22c9-4cec-a0d0-a16f15b8f7e4
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 043e9373f242523b7925a9ae775be6789f7cfc20
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660876"
---
# <a name="clean-devenvexe"></a>/Clean (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

清理所有中间文件和输出目录。

## <a name="syntax"></a>语法

```
devenv FileName /Clean [ /project projectnameorfile [/projectconfig name ] ]
```

## <a name="arguments"></a>自变量
 `FileName`（必需）。 解决方案文件或项目文件的完整路径和名称。

 /project `ProjName`（可选）。 解决方案中项目文件的路径和名称。 可以输入从 `SolutionName` 文件夹到项目文件的相对路径、项目的显示名称或项目文件的完整路径和名称。

 /projectconfig `ProjConfigName`（可选）。 清理命名的 `/project` 时要使用的项目生成配置的名称。

## <a name="remarks"></a>备注
 在集成开发环境 (IDE) 中，此开关执行与“清理解决方案”菜单命令相同的功能  。

 用双引号将含有空格的字符串引起来。

 “命令”窗口或使用 `/out` 开关指定的任何日志文件中都可显示清理和生成的摘要信息（包括错误）  。

## <a name="example"></a>示例
 第一个示例使用解决方案文件中指定的默认配置清理 `MySolution` 解决方案。

 第二个示例使用 `MySolution` 的 `Debug` 解决方案配置中的 `Debug` 项目生成配置来清理 `CSharpConsoleApp` 项目。

```
Devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /Clean

devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /Clean /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig "Debug"
```

## <a name="see-also"></a>另请参阅
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md) [/Build （devenv）](../../ide/reference/build-devenv-exe.md) [/Rebuild （devenv](../../ide/reference/rebuild-devenv-exe.md) ） [/out （devenv](../../ide/reference/out-devenv-exe.md) ）
