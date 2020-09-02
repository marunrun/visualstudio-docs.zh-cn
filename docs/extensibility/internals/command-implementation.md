---
title: 命令实现 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c7a536120c81c154cf894717a2af6a4e048d56e2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709583"
---
# <a name="command-implementation"></a>命令实现
若要在 VSPackage 中实现命令，您必须执行以下任务：

1. 在 *.vsct* 文件中，设置命令组，然后向其添加命令。 有关详细信息，请参阅 [Visual Studio 命令表 ( .vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

2. 向 Visual Studio 注册命令。

3. 实现命令。

以下部分介绍如何注册和实现命令。

## <a name="register-commands-with-visual-studio"></a>向 Visual Studio 注册命令
 如果你的命令将显示在菜单上，则必须将添加 <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> 到你的 VSPackage，并将其用作菜单名称或其资源 ID 的值。

```
[ProvideMenuResource("Menus.ctmenu", 1)]
...
    public sealed class MyPackage : Package
    {.. ..}

```

 此外，还必须将命令注册到 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> 。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>如果 VSPackage 是从派生的，则可以使用方法获取此服务 <xref:Microsoft.VisualStudio.Shell.Package> 。

```
OleMenuCommandService mcs = GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
if ( null != mcs )
{
    // Create the command for the menu item.
    CommandID menuCommandID = new CommandID(guidCommandGroup, myCommandID);
    MenuCommand menuItem = new MenuCommand(MenuItemCallback, menuCommandID );
    mcs.AddCommand( menuItem );
}

```

## <a name="implement-commands"></a>实现命令
 有多种方法来实现命令。 如果需要静态菜单命令（它是始终以相同方式出现在同一菜单上的命令），请使用创建命令， <xref:System.ComponentModel.Design.MenuCommand> 如前一节中的示例中所示。 若要创建静态命令，必须提供负责执行命令的事件处理程序。 由于命令始终处于启用状态，因此不需要将其状态提供给 Visual Studio。 如果要根据某些条件更改命令的状态，可以将命令创建为类的实例， <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 并在其构造函数中提供一个事件处理程序来执行命令，并在 `QueryStatus` 命令的状态发生更改时通知 Visual Studio。 你还可以 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 作为命令类的一部分实现，也可以在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 将命令作为项目的一部分提供时实现。 这两个接口和 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 类都具有一些方法，这些方法可通知 Visual Studio 对命令状态的更改，以及提供命令执行的其他方法。

 将命令添加到命令服务时，它将成为命令链中的一个。 当你为命令实现状态通知和执行方法时，请注意仅为该特定命令提供，并将所有其他情况传递到链中的其他命令。 如果无法通过返回) 在 (上传递命令 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> ，Visual Studio 可能会停止正常工作。

## <a name="querystatus-methods"></a>QueryStatus 方法
 如果要实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 方法，请检查命令所属的命令集的 GUID 以及命令的 ID。 请遵循这些指导：

- 如果无法识别 GUID，则这两个方法的实现必须返回 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP> 。

- 如果这两个方法的实现都可识别 GUID 但尚未实现命令，则该方法应返回 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> 。

- 如果这两种方法的实现都同时识别 GUID 和命令，则该方法应 `prgCmds` 使用以下标志设置参数) 中每个命令 (的命令标志字段 <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> ：

  - `OLECMDF_SUPPORTED`：支持该命令。

  - `OLECMDF_INVISIBLE`：该命令不应为可见。

  - `OLECMDF_LATCHED`：此命令已切换，并且已被选中。

  - `OLECMDF_ENABLED`：命令已启用。

  - `OLECMDF_DEFHIDEONCTXTMENU`：如果命令显示在快捷菜单上，则应隐藏该命令。

  - `OLECMDF_NINCHED`：该命令是菜单控制器并且未启用，但其下拉菜单列表不为空并且仍可用。  (很少使用此标志。 ) 

- 如果在带有标志的 *.vsct* 文件中定义该命令 `TextChanges` ，请设置以下参数：

  - 将 `rgwz` 参数的元素设置 `pCmdText` 为命令的新文本。

  - 将 `cwActual` 参数的元素设置 `pCmdText` 为命令字符串的大小。

此外，请确保当前上下文不是自动化函数，除非你的命令专门用于处理自动化函数。

若要指示支持特定命令，请返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 。 对于所有其他命令，返回 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> 。

在下面的示例中， `QueryStatus` 方法首先确保上下文不是自动化函数，然后查找正确的命令集 GUID 和命令 ID。 命令本身设置为 "已启用" 和 "支持"。 不支持任何其他命令。

```csharp
public int QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)
{
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))
    {
        if (pguidCmdGroup == VSConstants.VSStd2K && cCmds > 0)
        {
            // make the Right command visible
            if ((uint)prgCmds[0].cmdID == (uint)VSConstants.VSStd2KCmdID.RIGHT)
            {
                prgCmds[0].cmdf = (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_ENABLED | (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_SUPPORTED;
                return VSConstants.S_OK;
            }
        }
        return Constants.OLECMDERR_E_NOTSUPPORTED;
    }
}
```

## <a name="execution-methods"></a>执行方法
 方法的实现 `Exec` 类似于方法的实现 `QueryStatus` 。 首先，请确保上下文不是自动化函数。 然后，测试 GUID 和命令 ID。 如果无法识别 GUID 或命令 ID，则返回 <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> 。

 若要处理命令，请执行该命令，并 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 在执行成功时返回。 命令负责错误检测和通知;因此，如果执行失败，则返回错误代码。 下面的示例演示了应如何实现执行方法。

```csharp
public int Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)
{
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))
    {
        if (pguidCmdGroup == VSConstants.GUID_VSStandardCommandSet97)
        {
             if (nCmdID ==(uint) uint)VSConstants.VSStd2KCmdID.RIGHT)
            {
                //execute the command
                return VSConstants.S_OK;
            }
        }
    }
    return Constants.OLECMDERR_E_NOTSUPPORTED;
}
```

## <a name="see-also"></a>请参阅

- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
