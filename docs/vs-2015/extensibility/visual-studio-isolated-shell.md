---
title: Visual Studio Isolated Shell | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Shell [Visual Studio], shell-based applications%2C isolated mode
- Visual Studio shell, isolated mode
- isolated shell-based applications [Visual Studio]
- Visual Studio shell, shell-based applications%2C isolated mode
- Shell [Visual Studio], isolated mode
ms.assetid: d2620e71-be9e-44c9-b5b7-03a4c8d9cf0b
caps.latest.revision: 36
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 36491d9d590a45256e297654f71652ab5de5cd98
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299723"
---
# <a name="visual-studio-isolated-shell"></a>Visual Studio 独立 Shell
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

The Visual Studio isolated shell allows you to create stand-alone applications that can run side-by-side with other versions of Visual Studio. It is used primarily to host specialized tools that can use Visual Studio services but also have a customized appearance and branding. Visual Studio features and menu command groups can be easily turned on and off. Application titles, application icons, and splash screens are fully customizable. For a list of customizable features, see [Customizing the Isolated Shell](../extensibility/customizing-the-isolated-shell.md).  
  
 To work with an isolated shell project, you must install the Visual Studio SDK. Starting in Visual Studio 2015, you do not install the Visual Studio SDK from the download center. It is included as an optional feature in Visual Studio setup. You can also install the VS SDK later on. For more information, see [Installing the Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md).  
  
 To create an isolated shell application, start with a Visual Studio Shell Isolated project. This project contains everything that you need to develop and test your own isolated shell application. When you are ready to write the setup program that deploys your application, you must get the isolated shell redistributable package from [Microsoft Visual Studio Shell (Isolated) Redistributable Package](https://go.microsoft.com/fwlink/?LinkId=616022).  
  
> [!NOTE]
> Before you can access the isolated shell redistributable package, you will be asked to fill out a brief customer survey.  After filling out the survey, you’ll be directed to a Visual Studio Connect page with redistributable package download links.  You can find the download links on subsequent visits to the Visual Studio Connect site under the **PROGRAMS &#124; VISUAL STUDIO 2015 INTEGRATED AND ISOLATED SHELL** tab.  
  
> [!NOTE]
> For more information about how to deploy an isolated shell-based application, see [Walkthrough: Creating a Basic Isolated Shell Application](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).  
  
## <a name="working-with-the-isolated-shell"></a>Working with the isolated shell  
 A Visual Studio isolated shell application has full access to Visual Studio services and supports special customization and branding. There are several ways you can customize an isolated shell application:  
  
- You can use VSPackages and Managed Extensibility Framework (MEF) component parts to extend an isolated shell application just as you would use them in any other Visual Studio extension. For more information, see [Extending the Isolated Shell](../extensibility/extending-the-isolated-shell.md).  
  
- To make Visual Studio features and menu command groups available or unavailable, update the .vsct file in the user interface (UI) project of the application.  
  
- To remove **Options** pages or other Visual Studio shell components from the application, update the .pkgundef file of the application.  
  
- To modify other aspects of the appearance or behavior of the shell, update the .pkgdef file of the application.  
  
- Some aspects of the shell can also be specified when the application is started. To do this, update the parameters in the call to the Start entry point of the appenvstub.dll.  
  
  For more information about the different elements that you can customize, see [Elements of the Isolated Shell](../extensibility/elements-of-the-isolated-shell.md).  
  
## <a name="standard-features-of-the-isolated-shell"></a>Standard Features of the Isolated Shell  
 The following features are standard to all editions of Visual Studio.  
  
|功能类别|功能|  
|----------------------|-------------|  
|IDE Features|Import/Export Settings<br /><br /> Toolbox Control Installer<br /><br /> Task List & Error List<br /><br /> “输出”窗口<br /><br /> 起始页<br /><br /> “属性”窗口<br /><br /> 工具箱<br /><br /> “解决方案资源管理器”<br /><br /> “书签”窗口<br /><br /> 类视图<br /><br /> 对象浏览器<br /><br /> “命令”窗口<br /><br /> 文档大纲<br /><br /> Resource View<br /><br /> External Tool<br /><br /> Windows Communication Foundation (WCF) Add Service Reference<br /><br /> Language Integrated Query (LINQ) Support|  
|Editor/Designer|Code browsing tools (unified find, source definition, inheritance)<br /><br /> IntelliSense<br /><br /> SmartTags<br /><br /> 代码片段管理器<br /><br /> 代码段<br /><br /> Refactoring<br /><br /> Pretty listing<br /><br /> IntelliSense Filtering<br /><br /> “代码定义”窗口<br /><br /> 应用程序设计器<br /><br /> Windows Forms Designer — Windows 窗体设计器<br /><br /> Windows Presentation Foundation (WPF) Designer|  
|调试|C# Expression Evaluator<br /><br /> Local debugging<br /><br /> Managed debugging<br /><br /> 编辑并继续<br /><br /> Cross-thread debugging<br /><br /> Visualizations<br /><br /> 数据提示<br /><br /> Native debugging<br /><br /> Script debugging<br /><br /> Interop debugging<br /><br /> Just-in-time (JIT) debugging<br /><br /> Multi-process debugging<br /><br /> XSLT 调试<br /><br /> Attach to local process<br /><br /> 跟踪点<br /><br /> Breakpoint Constraints|  
|数据|Server Explorer (Simplified - Data Only)<br /><br /> Data bind to local data (.MDF or .MDB)<br /><br /> Data bind to object<br /><br /> Data bind to Web service<br /><br /> Full set of data controls<br /><br /> XML 编辑器<br /><br /> Data bind to local database server<br /><br /> “数据源”窗口|  
|Web|HTML 编辑器<br /><br /> Web 浏览器<br /><br /> Web 窗体设计器<br /><br /> Web Site Project<br /><br /> Web Application Project|  
|扩展性|Consumes VSPackages and MEF components|  
  
## <a name="see-also"></a>请参阅  
 [Shell（独立或集成）](../extensibility/shell-isolated-or-integrated.md)
