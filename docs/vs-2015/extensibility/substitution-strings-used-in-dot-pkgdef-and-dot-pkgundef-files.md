---
title: 中使用的替换字符串。.Pkgdef 和。.Pkgundef Files |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160538"
---
# <a name="substitution-strings-used-in-pkgdef-and-pkgundef-files"></a>.Pkgdef 和 .Pkgundef 文件中使用的替换字符串
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在为 Visual Studio 独立 shell 应用程序定义的 .pkgdef 和 .pkgundef 文件中使用下面列出的替换字符串。  
  
## <a name="substitution-strings"></a>替换字符串  
  
|String|描述|  
|------------|-----------------|  
|$=*RegistryEntry*$|*RegistryEntry*项的值。 如果注册表项字符串以反斜杠 () 结束 \\ ，则使用注册表子项的默认值。 例如，替换字符串 $ = HKEY_CURRENT_USER \Environment\TEMP $ 将扩展到当前用户的临时文件夹。|  
|$AppName $|传递到 AppEnv.dll 入口点的应用程序的限定名称。 限定名称包括应用程序名称、下划线以及类标识符 (应用程序自动化对象的 CLSID) ，该对象也会记录为 .pkgdef 文件中 ThisVersionDTECLSID 设置的值。|  
|$AppDataLocalFolder|此应用程序的% LOCALAPPDATA% 下的子文件夹。|  
|$BaseInstallDir $|安装 Visual Studio 的位置的完整路径。|  
|$CommonFiles $|% CommonProgramFiles% 环境变量的值。|  
|$MyDocuments $|当前用户的 "我的文档" 文件夹的完整路径。|  
|$PackageFolder $|包含应用程序的包程序集文件的目录的完整路径。|  
|$ProgramFiles $|% ProgramFiles% 环境变量的值。|  
|$RootFolder $|应用程序的根目录的完整路径。|  
|$RootKey $|应用程序的根注册表项。 默认情况下， \\ *CompanyName* \\ *ProjectName* \\ *VersionNumber*当应用程序正在运行时) _Config，根位于 HKEY_CURRENT_USER \software 的 (VersionNumber 它由 .pkgdef 文件 *中的 RegistryRoot*值设置。<br /><br /> $RootKey $ string 可用于检索应用程序子项下的注册表值。 例如，字符串 "$ = $RootKey $ \AppIcon $" 将返回应用程序根子项下的 AppIcon 项的值。<br /><br /> 分析器按顺序处理 .pkgdef 文件，并且仅当先前定义了该项时，才能访问应用程序子项下的注册表项|  
|$ShellFolder $|安装 Visual Studio 的位置的完整路径。|  
|$System $|Windows\system32 文件夹。|  
|$WINDIR $|Windows 文件夹。|  
  
 如果分析器无法识别替换字符串，或者无法确定注册表项或环境变量的值，则它不会在字符串的该部分执行替换。
