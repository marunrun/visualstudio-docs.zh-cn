---
title: 注册工具窗口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering managed
- tool windows, registering
ms.assetid: 8c8c4a24-3da4-497b-9db2-0ddd7cfbfdd2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2e7971de5ae5301d99147bbfc374dda6b039662a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701599"
---
# <a name="register-a-tool-window"></a>注册工具窗口
您可以使用<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>和<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>注册工具窗口。

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

 在上面的代码中，<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>将`PersistedWindowPane`和`DynamicWindowPane`工具窗口与 Visual Studio 注册。 持久化工具窗口与**解决方案资源管理器**停靠并选项卡化，并且动态窗口被赋予默认起始位置和大小。 动态窗口为瞬态窗口，表示它不是在启动时创建的。 这将在系统`DontForceCreate`注册表中的`ToolWindows`密钥中写入值。 有关详细信息，请参阅[工具窗口显示配置](/visualstudio/extensibility/tool-window-display-configuration?view=vs-2015)。
