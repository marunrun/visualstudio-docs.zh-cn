---
title: MSBuild 响应文件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- response files, MSBuild
- MSBuild, response files
- MSBuild, .rsp files
- .rsp files
ms.assetid: 9f53987b-20ee-470a-ab62-fce997bb5e15
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a1ce11edac37368b9c4993a87a8c2b3e734b7862
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189374"
---
# <a name="msbuild-response-files"></a>MSBuild 响应文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

响应 (.rsp) 文件是包含 MSBuild.exe 命令行开关的文本文件。 每个开关可以单独占一行，或者所有开关仅占一行。 注释行以 # 符号开头。 **@** 开关用于将其他响应文件传递给 MSBuild.exe。  
  
 自动响应文件是在生成项目时 MSBuild.exe 自动使用的特殊 .rsp 文件。 MSBuild.rsp 文件必须位于 MSBuild.exe 所在的目录中，否则无法找到该文件。 可以编辑此文件，向 MSBuild.exe 指定默认命令行开关。 例如，如果每次生成项目时都使用相同的记录器，则可以将 **/logger** 开关添加到 msbuild.exe，MSBuild.exe 将在每次生成项目时使用记录器。  
  
## <a name="see-also"></a>另请参阅  
 [MSBuild 引用](../msbuild/msbuild-reference.md)   
 [命令行参考](../msbuild/msbuild-command-line-reference.md)
