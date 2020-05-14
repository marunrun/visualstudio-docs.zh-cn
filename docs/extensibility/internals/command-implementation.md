---
title: 命令实现 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709583"
---
# <a name="command-implementation"></a>命令实现
要在 VSPackage 中实现命令，必须执行以下任务：

1. 在 *.vsct*文件中，设置一个命令组，然后将命令添加到该文件中。 有关详细信息，请参阅[可视化工作室命令表 （.vsct） 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

2. 向可视化工作室注册该命令。

3. 实现命令。

以下各节说明如何注册和实现命令。

## <a name="register-commands-with-visual-studio"></a>在可视化工作室注册命令
 如果命令要显示在菜单上，则必须<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute>将 添加到 VSPackage，并将菜单的名称或其资源 ID 用作值。

```
[ProvideMenuResource("Menus.ctmenu", 1)]
...
    public sealed class MyPackage : Package
    {.. ..}

```

 此外，必须向 注册<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>命令。 如果 VSPackage 派生自<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A><xref:Microsoft.VisualStudio.Shell.Package>，则可以使用 方法获取此服务。

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
 实现命令的方法有很多种。 如果需要静态菜单命令（该命令是始终以相同方式显示的命令，并且在同一菜单上）使用，请使用<xref:System.ComponentModel.Design.MenuCommand>上一节中的示例中所示创建该命令。 要创建静态命令，必须提供负责执行该命令的事件处理程序。 由于该命令始终处于启用状态且可见，因此您不必向 Visual Studio 提供其状态。 如果要根据特定条件更改命令的状态，则可以将该命令创建为<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>类的实例，并在其构造函数中提供事件处理程序来执行命令，并提供一个`QueryStatus`处理程序，以便在命令的状态更改时通知 Visual Studio。 还可以作为命令类<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>的一部分实现，或者，如果作为项目的一<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>部分提供命令，则可以实现。 两个接口和<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>类都有通知 Visual Studio 命令状态更改的方法，以及提供执行命令的其他方法。

 将命令添加到命令服务时，该命令将成为命令链之一。 实现命令的状态通知和执行方法时，请注意仅提供该特定命令，并将所有其他情况传递给链中的其他命令。 如果您未能传递命令（通常是返回<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>），Visual Studio 可能会停止正常工作。

## <a name="querystatus-methods"></a>查询状态方法
 如果要实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法或<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>方法，请检查命令所属的命令集的 GUID 和命令的 ID。 请遵循这些指导：

- 如果识别 GUID，则任一方法的实现都必须返回<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP>。

- 如果任一方法的实现都识别 GUID，但尚未实现该命令，则 该方法应返回<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>。

- 如果任一方法的实现同时识别 GUID 和 命令，则该方法应使用以下`prgCmds`<xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF>标志设置每个命令（在参数中）的命令标志字段：

  - `OLECMDF_SUPPORTED`：该命令受支持。

  - `OLECMDF_INVISIBLE`：该命令不应可见。

  - `OLECMDF_LATCHED`： 命令已切换，似乎已选中。

  - `OLECMDF_ENABLED`：命令已启用。

  - `OLECMDF_DEFHIDEONCTXTMENU`：如果命令出现在快捷菜单上，则应隐藏该命令。

  - `OLECMDF_NINCHED`：该命令是菜单控制器，未启用，但其下拉菜单列表不为空，仍然可用。 （此标志很少使用。

- 如果命令是在带`TextChanges`标志的 *.vsct*文件中定义的，则设置以下参数：

  - 将`rgwz``pCmdText`参数的元素设置为命令的新文本。

  - 将`cwActual``pCmdText`参数的元素设置为命令字符串的大小。

此外，请确保当前上下文不是自动化函数，除非您的命令专门用于处理自动化函数。

要指示您支持特定命令，请返回<xref:Microsoft.VisualStudio.VSConstants.S_OK>。 对于所有其他命令，返回<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>。

在下面的示例中，`QueryStatus`该方法首先确保上下文不是自动化函数，然后找到正确的命令集 GUID 和命令 ID。 命令本身设置为启用和支持。 不支持其他命令。

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
 `Exec`方法的实现类似于方法的`QueryStatus`实现。 首先，请确保上下文不是自动化函数。 然后，测试 GUID 和命令 ID。 如果无法识别 GUID 或命令 ID，<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>则返回 。

 要处理该命令，请执行该命令<xref:Microsoft.VisualStudio.VSConstants.S_OK>，并在执行成功时返回。 您的命令负责错误检测和通知;因此，如果执行失败，则返回错误代码。 下面的示例演示如何实现执行方法。

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

- [VS包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
