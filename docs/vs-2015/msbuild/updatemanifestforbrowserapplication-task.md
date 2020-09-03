---
title: UpdateManifestForBrowserApplication 任务 | Microsoft Docs
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
- UpdateManifestForBrowserApplication task [WPF MSBuild]
- adding the <hostInBrowser /> element to the application manifest [WPF MSBuild]
- building XBAP projects [WPF MSBuild]
- UpdateManifestForBrowserApplication task [WPF MSBuild], parameters
ms.assetid: 653339f7-654b-4d64-a26a-5c9f27036895
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6dffa98a8abbf74bd6eee8761d91f09a7c022666
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68740221"
---
# <a name="updatemanifestforbrowserapplication-task"></a>UpdateManifestForBrowserApplication 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:Microsoft.Build.Tasks.Windows.UpdateManifestForBrowserApplication>运行任务时，会将 **\<hostInBrowser />** 元素添加到应用程序清单中*projectname*， () [!INCLUDE[TLA#tla_xbap](../includes/tlasharptla-xbap-md.md)] 生成项目时。  
  
## <a name="task-parameters"></a>任务参数  
  
|参数|描述|  
|---------------|-----------------|  
|`ApplicationManifest`|必需的 **ITaskItem[]** 参数。<br /><br /> 指定想要将 `<hostInBrowser />` 元素添加到其中的应用程序清单文件的路径和名称。|  
|`HostInBrowser`|所需的 **Boolean** 参数。<br /><br /> 指定是否修改应用程序清单以包括 **\<hostInBrowser />** 元素。 如果**为 true**，则 `<` 元素中包括新的**hostInBrowser/>** 元素 **\<entryPoint />** 。 请注意，元素包含是累计的：如果 **\<hostInBrowser />** 元素已存在，则不会将其删除或覆盖。 而是创建一个附加 **\<hostInBrowser />** 元素。 如果为 **false**，则不会修改应用程序清单。|  
  
## <a name="remarks"></a>备注  
 通过使用 [!INCLUDE[TLA#tla_clickonce](../includes/tlasharptla-clickonce-md.md)] 部署运行 [!INCLUDE[TLA2#tla_xbap#plural](../includes/tla2sharptla-xbapsharpplural-md.md)]，因此，必须使用支持的部署和应用程序清单进行发布。 [!INCLUDE[TLA#tla_msbuild](../includes/tlasharptla-msbuild-md.md)] 使用 [GenerateApplicationManifest](/dotnet/api/microsoft.build.tasks.generateapplicationmanifest) 任务来生成应用程序清单。  
  
 然后，若要配置要从浏览器承载的应用程序，必须将另一个元素 **\<hostInBrowser />** 添加到应用程序清单中，如以下示例中所示：  
  
```  
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
  
 当生成 [!INCLUDE[TLA2#tla_xbap](../includes/tla2sharptla-xbap-md.md)] 项目时，将运行 <xref:Microsoft.Build.Tasks.Windows.UpdateManifestForBrowserApplication> 任务，以添加 `<hostInBrowser />` 元素。  
  
## <a name="example"></a>示例  
 以下示例演示如何确保 `<hostInBrowser />` 元素包括在应用程序清单文件中。  
  
```  
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
  
## <a name="see-also"></a>另请参阅  
 [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)   
 [任务引用](../msbuild/wpf-msbuild-task-reference.md)   
 [MSBuild 引用](../msbuild/msbuild-reference.md)   
 [任务引用](../msbuild/msbuild-task-reference.md)   
 [生成 wpf 应用程序 (WPF) ](https://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)   
 [WPF XAML 浏览器应用程序概述](https://msdn.microsoft.com/library/3a7a86a8-75d5-4898-96b9-73da151e5e16)
