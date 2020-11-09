---
title: UpdateManifestForBrowserApplication 任务 | Microsoft Docs
description: 了解 MSBuild 如何运行 UpdateManifestForBrowserApplication 任务将 hostInBrowser 元素添加到应用程序清单中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- UpdateManifestForBrowserApplication task [WPF MSBuild]
- adding the <hostInBrowser /> element to the application manifest [WPF MSBuild]
- building XBAP projects [WPF MSBuild]
- UpdateManifestForBrowserApplication task [WPF MSBuild], parameters
ms.assetid: 653339f7-654b-4d64-a26a-5c9f27036895
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 43e8fc7b9b09af51ea3be73409e2dcde9a718cee
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93046820"
---
# <a name="updatemanifestforbrowserapplication-task"></a>UpdateManifestForBrowserApplication 任务

运行 <xref:Microsoft.Build.Tasks.Windows.UpdateManifestForBrowserApplication> 任务，以便在生成 XAML 浏览器应用程序 (XBAP) 项目时，将 \<hostInBrowser /> 元素添加到应用程序清单 (\<projectname>.exe.manifest)。

## <a name="task-parameters"></a>任务参数

|参数|描述|
|---------------|-----------------|
|`ApplicationManifest`|必需的 **ITaskItem[]** 参数。<br /><br /> 指定想要将 `<hostInBrowser />` 元素添加到其中的应用程序清单文件的路径和名称。|
|`HostInBrowser`|所需的 **Boolean** 参数。<br /><br /> 指定是否要修改应用程序清单以包括 \<hostInBrowser /> 元素。 如果为 True，则 \<entryPoint /> 元素中将包含一个新的 \<hostInBrowser /> 元素  。 元素包含是累计的：如果 \<hostInBrowser /> 元素已存在，则不会删除或覆盖它。 相反，将创建额外的 \<hostInBrowser /> 元素。 如果为 false  ，则不会修改应用程序清单。|

## <a name="remarks"></a>备注

 XBAP 通过 ClickOnce 部署运行，因此必须使用支持部署和应用程序清单进行发布。 MSBuild 使用 [GenerateApplicationManifest](generateapplicationmanifest-task.md) 任务来生成应用程序清单。

 然后，要将应用程序配置为从浏览器中托管，则必须将额外的 \<hostInBrowser /> 元素添加到应用程序清单中，如以下示例所示：

```xml
<!--MyXBAPApplication.exe.manifest-->
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly ... >
    <asmv1:assemblyIdentity ... />
    <application />
    <entryPoint>
      ...
      <hostInBrowser xmlns="urn:schemas-microsoft-com:asm.v3" />
    </entryPoint>
  ...
/>
```

 当生成 XBAP 项目时，将运行 <xref:Microsoft.Build.Tasks.Windows.UpdateManifestForBrowserApplication> 任务，以添加 `<hostInBrowser />` 元素。

## <a name="example"></a>示例

 以下示例演示如何确保 `<hostInBrowser />` 元素包括在应用程序清单文件中。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.UpdateManifestForBrowserApplication"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="UpdateManifestForBrowserApplicationTask">
    <UpdateManifestForBrowserApplication
      ApplicationManifest="MyXBAPApplication.exe.manifest"
      HostInBrowser="true" />
  </Target>
</Project>
```

## <a name="see-also"></a>请参阅

- [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)
- [任务参考](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
- [生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
- [WPF XAML 浏览器应用程序概述](/dotnet/framework/wpf/app-development/wpf-xaml-browser-applications-overview)