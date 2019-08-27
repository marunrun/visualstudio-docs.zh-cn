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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4b956fb09681f6f4a1f916f4b108028f69f009cd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200900"
---
# <a name="projectconfig-devenvexe"></a>/ProjectConfig (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定生成、清理、重新生成或部署在 `/project` 参数中命名的项目时要应用的项目生成配置。  
  
## <a name="syntax"></a>语法  
  
```  
devenv SolutionName {/build|/clean|/rebuild|/deploy} SolnConfigName [/project ProjName] [/projectconfig ProjConfigName]  
```  
  
## <a name="arguments"></a>自变量  
 /build  
 生成 `/project` `ProjName` 指定的项目。  
  
 /clean  
 清理在生成过程中创建的所有中间文件和输出目录。  
  
 /rebuild  
 清理，然后生成 `/project` `ProjName` 指定的项目。  
  
 /deploy  
 指定生成或重新生成后部署该项目。  
  
 `SolnConfigName`  
 必需。 将应用于 `SolutionName` 中命名的解决方案的解决方案配置的名称。  
  
 `SolutionName`  
 必需。 解决方案文件的完整路径和名称。  
  
 /project `ProjName`  
 可选。 解决方案中项目文件的路径和名称。 可以输入从 `SolutionName` 文件夹到项目文件的相对路径、项目的显示名称或项目文件的完整路径和名称。  
  
 /projectconfig `ProjConfigName`  
 可选。 要应用于已命名的 `/project` 的项目生成配置的名称。  
  
## <a name="remarks"></a>备注  
  
- 必须作为 `devenv /build`、/`clean`、`/rebuild` 或 `/deploy` 命令的一部分与 `/project` 开关一起使用。  
  
- 用双引号将含有空格的字符串引起来。  
  
- “命令”  窗口或使用 `/out` 开关指定的任何日志文件中都可显示生成的摘要信息（包括错误）。  
  
## <a name="example"></a>示例  
 本示例使用 `MySolution` 的 `Debug` 解决方案配置中的 `Debug` 项目生成配置来生成 `CSharpConsoleApp` 项目。  
  
```  
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug   
```  
  
## <a name="see-also"></a>另请参阅  
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)   
 [/Project (devenv.exe)](../../ide/reference/project-devenv-exe.md)   
 [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)   
 [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)   
 [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)   
 [/Deploy (devenv.exe)](../../ide/reference/deploy-devenv-exe.md)   
 [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
