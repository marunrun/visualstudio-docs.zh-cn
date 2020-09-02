---
title: 注册工具窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering managed
- tool windows, registering
ms.assetid: 8c8c4a24-3da4-497b-9db2-0ddd7cfbfdd2
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8178938715278bf69fe8f4cc1b336bbd19cec04e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62535631"
---
# <a name="registering-a-tool-window"></a>注册工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以使用和注册您的工具窗口。 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute><xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>  
  
## <a name="example"></a>示例  
  
```csharp  
  
      [ProvideToolWindow(typeof(PersistedWindowPane), Style = MsVsShell.VsDockStyle.Tabbed, Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")] [ProvideToolWindow(typeof(DynamicWindowPane), PositionX=250, PositionY=250, Width=160, Height=180, Transient=true)] [ProvideToolWindowVisibility(typeof(DynamicWindowPane), /*UICONTEXT_SolutionExists*/"f1536ef8-92ec-443c-9ed7-fdadf150da82")]  
[ProvideMenuResource(1000, 1)]  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[Guid("01069CDD-95CE-4620-AC21-DDFF6C57F012")]  
public class PackageToolWindow : Package  
{  
```  
  
 在上面的代码中，向 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> Visual Studio 注册了 PersistedWindowPane 和 DynamicWindowPane 工具窗口。 保留的工具窗口与 **解决方案资源管理器**停靠在一起，并为动态窗口提供了一个默认起始位置和大小。 动态窗口被设为暂时性窗口，这表示它不是在启动时创建的。 这会在系统注册表中的 ToolWindows 项中写入一个 DontForceCreate 值。 有关详细信息，请参阅 [工具窗口显示配置](../extensibility/tool-window-display-configuration.md)。
