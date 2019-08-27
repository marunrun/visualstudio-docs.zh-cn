---
title: WPF MSBuild 任务引用 | Microsoft Docs
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
- WPF MSBuild task reference [WPF MSBuild], term/definition table
- build tasks [WPF MSBuild], Microsoft build engine
- build tasks using the Microsoft build engine [WPF MSBuild], compile markup and process resources
- WPF MSBuild task reference [WPF MSBuild]
ms.assetid: 96df0370-e50f-4ffc-9771-b12fb8721143
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: eb21495954801d55c1db0bb9156a813ab73db683
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687100"
---
# <a name="wpf-msbuild-task-reference"></a>WPF MSBuild 任务引用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows Presentation Foundation (WPF) 生成进程通过另一组生成任务扩展 Microsoft 生成引擎 (MSBuild)，这些任务包括编译标记和进程资源的任务。  
  
## <a name="in-this-section"></a>本节内容  
 [FileClassifier](../msbuild/fileclassifier-task.md)  
 将一组源资源分类为将嵌入到程序集的源资源。 如果资源不可本地化，则将其嵌入主应用程序程序集；否则，将其嵌入附属程序集。  
  
 [GenerateTemporaryTargetAssembly](../msbuild/generatetemporarytargetassembly-task.md)  
 如果项目中至少有一个 [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] 页引用该项目中本地声明的类型，则生成一个程序集。 在生成过程完成后或者在生成过程失败的情况下，生成的程序集会被删除。  
  
 [GetWinFXPath](../msbuild/getwinfxpath-task.md)  
 返回当前 [!INCLUDE[TLA#tla_winfx](../includes/tlasharptla-winfx-md.md)] 运行时的目录。  
  
 [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md)  
 将非本地化的 [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] 项目文件转换成已编译的二进制格式。  
  
 [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md)  
 在引用同一项目中的类型的 [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] 文件中执行第二轮标记编译。  
  
 [MergeLocalizationDirectives](../msbuild/mergelocalizationdirectives-task.md)  
 将本地化属性和一个或多个 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 二进制格式文件的注释合并到整个程序集的单一文件中。  
  
 [ResourcesGenerator](../msbuild/resourcesgenerator-task.md)  
 将一个或多个资源（二进制格式的 .jpg、.ico、.bmp、[!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 以及其他扩展名类型）嵌入 .resources 文件中。  
  
 [UidManager](../msbuild/uidmanager-task.md)  
 检查、更新或删除唯一标识符 (UID)，以对源 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 文件中包含的所有 [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] 元素进行本地化。  
  
 [UpdateManifestForBrowserApplication](../msbuild/updatemanifestforbrowserapplication-task.md)  
 生成 [!INCLUDE[TLA#tla_xbap](../includes/tlasharptla-xbap-md.md)] 项目时，将\<hostInBrowser /> 元素添加到应用程序清单中 (projectname.exe.manifest)。  
  
## <a name="see-also"></a>请参阅  
 [MSBuild](https://msdn.microsoft.com/7c49aba1-ee6c-47d8-9de1-6f29a906e20b)
