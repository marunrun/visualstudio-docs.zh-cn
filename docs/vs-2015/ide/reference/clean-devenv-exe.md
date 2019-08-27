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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e1c32e062cf2a5406f235133fb646a16d21707cb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190411"
---
# <a name="clean-devenvexe"></a>/Clean (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

清理所有中间文件和输出目录。  
  
## <a name="syntax"></a>语法  
  
```  
devenv FileName /Clean [ /project projectnameorfile [/projectconfig name ] ]  
```  
  
## <a name="arguments"></a>自变量  
 `FileName`  
 必需。 解决方案文件或项目文件的完整路径和名称。  
  
 /project `ProjName`  
 可选。 解决方案中项目文件的路径和名称。 可以输入从 `SolutionName` 文件夹到项目文件的相对路径、项目的显示名称或项目文件的完整路径和名称。  
  
 /projectconfig `ProjConfigName`  
 可选。 清理命名的 `/project` 时要使用的项目生成配置的名称。  
  
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
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)   
 [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)   
 [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)   
 [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
