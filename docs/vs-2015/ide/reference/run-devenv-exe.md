---
title: /Run (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /run Devenv
- run Devenv switch
- applications [Visual Studio], running
- /r Devenv switch
- Devenv, /run switch
- r Devenv switch (/r)
ms.assetid: b1f22f9d-39a5-4918-8a2a-4b5c1e872665
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 68e5dcc5ff2e78fe87bbaad639c93f5532ea74fe
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163378"
---
# <a name="run-devenvexe"></a>/Run (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

编译并运行指定的项目或解决方案。  
  
## <a name="syntax"></a>语法  
  
```  
devenv {/run|/r} {SolutionName|ProjectName}  
```  
  
## <a name="arguments"></a>自变量  
 `SolutionName`  
 必需。 解决方案文件的完整路径和名称。  
  
 `ProjectName`  
 必需。 项目文件的完整路径和名称。  
  
## <a name="remarks"></a>备注  
 根据为活动解决方案配置指定的设置编译并运行指定项目或解决方案。 此开关启动集成开发环境 (IDE) ，并在项目或解决方案已完成运行后让该环境保持活动状态。  
  
- 用双引号将含有空格的字符串引起来。  
  
- “命令”窗口或使用 `/out` 开关指定的任何日志文件中都可显示摘要信息（包括错误）  。  
  
## <a name="example"></a>示例  
 该示例使用活动部署配置运行解决方案 `MySolution`。  
  
```  
devenv /run "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln"  
```  
  
## <a name="see-also"></a>另请参阅  
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)   
 [/Runexit (devenv.exe)](../../ide/reference/runexit-devenv-exe.md)   
 [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)   
 [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)   
 [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
