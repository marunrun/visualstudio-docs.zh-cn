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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62535631"
---
# <a name="registering-a-tool-window"></a>注册工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以注册你使用的工具窗口<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>和  <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>  
  
## <a name="example"></a>示例  
  
```csharp  
  
      [ProvideToolWindow(typeof(PersistedWindowPane), Style = MsVsShell.VsDockStyle.Tabbed, Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")] [ProvideToolWindow(typeof(DynamicWindowPane), PositionX=250, PositionY=250, Width=160, Height=180, Transient=true)] [ProvideToolWindowVisibility(typeof(DynamicWindowPane), /*UICONTEXT_SolutionExists*/"f1536ef8-92ec-443c-9ed7-fdadf150da82")]  
[ProvideMenuResource(1000, 1)]  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[Guid("01069CDD-95CE-4620-AC21-DDFF6C57F012")]  
public class PackageToolWindow : Package  
{  
```  
  
 在上面的代码，<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>向 Visual Studio 注册 persistedwindowpane 注册时和 DynamicWindowPane 工具窗口。 保留的工具窗口停靠，并使用选项卡式**解决方案资源管理器**，并且动态窗口中将提供默认值的起始位置和大小。 由暂时的指示在启动时不创建动态窗口中。 这将 DontForceCreate 值写入系统注册表中的工具 Windows 键。 有关详细信息，请参阅[工具窗口中显示配置](../extensibility/tool-window-display-configuration.md)。
