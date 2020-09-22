---
title: " (c + +) 的隔离 Shell 入口点参数 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Shell [Visual Studio], isolated mode%2C Start entry point
- Visual Studio shell, isolated mode%2C Start entry point
ms.assetid: 18f4b18b-2173-4afa-ba0a-42fe33e61118
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9e736343212c4bf6acd833f5740b996c6c032c3f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840732"
---
# <a name="isolated-shell-entry-point-parameters-c"></a>独立 Shell 入口点参数 (C++)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当基于 Visual Studio shell 的应用程序启动时，它将调用 Visual Studio shell 的开始入口点。 可以在调用 shell 的开始入口点时重写以下设置。 有关每个设置的说明，请参阅 [。.Pkgdef 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)。  
  
- AddinsAllowed  
  
- AllowsDroppedFilesOnMainWindow  
  
- 应用名称  
  
- CommandLineLogo  
  
- DefaultHomePage  
  
- DefaultProjectsLocation  
  
- DefaultSearchPage  
  
- DefaultUserFilesFolderRoot  
  
- DisableOutputWindow  
  
- HideMiscellaneousFilesByDefault  
  
- HideSolutionConcept  
  
- NewProjDlgInstalledTemplatesHdr  
  
- NewProjDlgSlnTreeNodeTitle  
  
- SolutionFileCreatorIdentifier  
  
- SolutionFileExt  
  
- UserFilesSubFolderName  
  
- UserOptsFileExt  
  
  Visual Studio Shell 独立模板会创建一个 *源文件（解决方案*名称 .cpp），其中 *，解决方案名称* 是应用程序的解决方案名称。 此文件定义应用程序的主入口点，_tWinMain 函数。 此函数将调用 shell 的开始入口点。  
  
  可以通过在应用程序启动时更改这些设置来更改应用程序的行为。  
  
## <a name="parameters"></a>parameters  
 Visual Studio shell 的开始入口点定义五个参数。 不要更改前四个参数。 第五个参数采用设置重写列表。 从应用程序的主入口点调用 shell 的开始入口点。  
  
 Shell 的开始入口点具有以下签名。  
  
```  
typedef int (__cdecl *STARTFCN)(LPSTR, LPWSTR, int, GUID *, WCHAR *pszSettings);  
```  
  
 如果你不希望重写任何应用程序设置，请将 settings override 参数的值保留为 null 指针。  
  
 若要重写一个或多个设置，请传递包含要重写的设置的 Unicode 字符串。 字符串是一个以分号分隔的名称-值对的列表。 每个对都包含要重写的设置的名称，后跟一个等号 (=) ，然后是要应用于该设置的值。  
  
> [!NOTE]
> 不要在 Unicode 字符串中包括空格。  
  
 对于布尔值设置，以下字符串表示值 true;所有其他字符串都表示值 false。 这些字符串不区分大小写。  
  
- \+  
  
- 1  
  
- -1  
  
- on  
  
- 是  
  
- 是  
  
## <a name="example"></a>示例  
 若要禁用外接程序并更改应用程序的默认项目位置，可以将最后一个参数设置为 "AddinsAllowed = false; DefaultProjectsLocation =%USERPROFILE%\temp"。  
  
## <a name="see-also"></a>另请参阅  
 [自定义独立 Shell](../extensibility/customizing-the-isolated-shell.md)   
 [.Pkgdef 文件](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)
