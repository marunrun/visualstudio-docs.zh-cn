---
title: 注册工具窗口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering managed
- tool windows, registering
ms.assetid: 8c8c4a24-3da4-497b-9db2-0ddd7cfbfdd2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34fddd6513aad612398c700b935c6d1d3ee72b59
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186262"
---
# <a name="register-a-tool-window"></a>注册工具窗口
您可以使用 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> 和 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>注册您的工具窗口。

## <a name="example"></a>示例

```csharp

[ProvideToolWindow(typeof(PersistedWindowPane), Style = MsVsShell.VsDockStyle.Tabbed, Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
[ProvideToolWindow(typeof(DynamicWindowPane), PositionX=250, PositionY=250, Width=160, Height=180, Transient=true)]
[ProvideToolWindowVisibility(typeof(DynamicWindowPane), /*UICONTEXT_SolutionExists*/"f1536ef8-92ec-443c-9ed7-fdadf150da82")]
[ProvideMenuResource(1000, 1)]
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("01069CDD-95CE-4620-AC21-DDFF6C57F012")]
public class PackageToolWindow : Package
{
```

 在上面的代码中，<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> 向 Visual Studio 注册 `PersistedWindowPane` 和 `DynamicWindowPane` 工具窗口。 保留的工具窗口与**解决方案资源管理器**停靠在一起，并为动态窗口提供了一个默认起始位置和大小。 动态窗口被设为暂时性窗口，这表示它不是在启动时创建的。 这会在系统注册表的 `ToolWindows` 项中写入 `DontForceCreate` 值。 有关详细信息，请参阅[工具窗口显示配置](/visualstudio/extensibility/tool-window-display-configuration?view=vs-2015)。
