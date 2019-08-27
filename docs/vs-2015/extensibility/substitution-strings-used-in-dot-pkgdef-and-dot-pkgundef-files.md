---
title: 替换字符串中使用。Pkgdef 和。Pkgundef 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode%2C .pkgdef and .pkgundef files
ms.assetid: b1755d63-d794-4fd7-864b-70a9684881c2
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 47434d9d1dfcedeeaea330b1d65645d7a632c6e6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160538"
---
# <a name="substitution-strings-used-in-pkgdef-and-pkgundef-files"></a>.Pkgdef 和 .Pkgundef 文件中使用的替换字符串
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用在.pkgdef 下面列出的替换字符串和.pkgundef 文件定义为您的 Visual Studio 独立 shell 应用程序。  
  
## <a name="substitution-strings"></a>替换字符串  
  
|String|描述|  
|------------|-----------------|  
|$=*RegistryEntry*$|值*RegistryEntry*条目。 如果注册表条目字符串以反斜杠结尾 (\\)，则使用默认值的注册表子项。 例如，替换字符串 $= 的 HKEY_CURRENT_USER\Environment\TEMP$ 已扩展到当前用户的临时文件夹。|  
|$AppName$|传递给 AppEnv.dll 入口点的应用程序的限定的名称。 限定的名组成的应用程序名称、 下划线和也会记录为 ThisVersionDTECLSID 设置项目.pkgdef 文件中的值的应用程序自动化对象的类标识符 (CLSID)。|  
|$AppDataLocalFolder|为此应用程序 %LOCALAPPDATA%下的子文件夹。|  
|$BaseInstallDir$|Visual Studio 的安装位置的位置的完整路径。|  
|$CommonFiles$|%Commonprogramfiles%环境变量的值。|  
|$MyDocuments$|当前用户的我的文档文件夹的完整路径。|  
|$PackageFolder$|包含应用程序的包程序集文件的目录的完整路径。|  
|$ProgramFiles$|%Programfiles%环境变量的值。|  
|$RootFolder$|应用程序的根目录的完整路径。|  
|$RootKey $|应用程序的的根注册表项。 默认情况下是 HKEY_CURRENT_USER\Software\\*CompanyName*\\*ProjectName*\\*VersionNumber* （当应用程序正在运行，_Config 追加到此密钥）。 设置中的 RegistryRoot 值*SolutionName*.pkgdef 文件。<br /><br /> $RootKey$ 字符串可用于检索应用程序子项下的注册表值。 例如，字符串"$= $RootKey$ \AppIcon$"将返回应用程序根子项下的 AppIcon 条目的值。<br /><br /> 分析器按顺序处理.pkgdef 文件，并可以访问应用程序子项下的注册表项，仅当该条目之前已定义|  
|$ShellFolder$|Visual Studio 的安装位置的位置的完整路径。|  
|$System$|Windows\system32 文件夹中。|  
|$WINDIR $|Windows 文件夹中。|  
  
 如果分析器无法识别替换字符串或它无法确定注册表项或环境变量的值，然后它不会执行替换的字符串的该部件上。
