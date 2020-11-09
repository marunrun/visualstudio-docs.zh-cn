---
title: UidManager 任务 | Microsoft Docs
description: 了解 MSBuild UidManager 任务如何检查、更新或删除唯一标识符 (UID)，以对源 XAML 文件中的所有 XAML 元素进行本地化。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- UidManager task [WPF MSBuild]
- UidManager task [WPF MSBuild], parameters
- managing UIDs when localizing XAML elements [WPF MSBuild]
- localizing XAML elements [WPF MSBuild], managing UIDs
- checking UIDs when localizing XAML elements [WPF MSBuild]
ms.assetid: 4fc7b5a5-11b0-46ca-9656-8c2a0b08d1fe
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 852b910de742676e1fe7dd0c85129640eb37a9ae
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93046929"
---
# <a name="uidmanager-task"></a>UidManager 任务

<xref:Microsoft.Build.Tasks.Windows.UidManager> 任务将检查、更新或删除唯一标识符 (UID)，以对源 XAML 文件中包含的所有 XAML 元素进行本地化。

## <a name="task-parameters"></a>任务参数

| 参数 | 说明 |
|-------------------------| - |
| `IntermediateDirectory` | 可选 **String** 参数。<br /><br /> 指定用于备份由 MarkupFiles 参数指定的源 XAML 文件的目录。 |
| `MarkupFiles` | 必需的 **ITaskItem[]** 参数。<br /><br /> 指定要包含的源 XAML 文件，以用于 UID 检查、更新或删除。 |
| `Task` | 必需的 **String** 参数。<br /><br /> 指定想要执行的 UID 管理任务。 有效选项为“检查”、“更新”或“删除”。 |

## <a name="example"></a>示例

 下例使用 <xref:Microsoft.Build.Tasks.Windows.UidManager> 任务来检查指定的源 XAML 文件是否包含具有适当 UID 的 XAML 元素。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.UidManager"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="UidManagerTask">
    <UidManager
      Task="Check"
      MarkupFiles="Page1.xaml;Page2.xaml"
      IntermediateDirectory="c:\UidManagerIntermediateDirectory" />
  </Target>
</Project>
```

## <a name="see-also"></a>请参阅

- [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)
- [任务参考](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
- [生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
- [如何：对应用程序进行本地化](/dotnet/framework/wpf/advanced/how-to-localize-an-application)