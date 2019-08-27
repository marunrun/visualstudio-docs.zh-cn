---
title: 命令实现 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fbd0a9a1886bc1f8743ac8919bcc9cb39559dd19
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824945"
---
# <a name="command-implementation"></a>命令实现
若要在 VSPackage 中实现命令，必须执行以下任务：

1. 在中 *.vsct*文件设置了一个命令组，然后将该命令添加到它。 有关详细信息，请参阅[Visual Studio 命令表格 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

2. 通过 Visual Studio 注册该命令。

3. 实现命令。

以下部分介绍如何注册和实现命令。

## <a name="register-commands-with-visual-studio"></a>使用 Visual Studio 注册命令
 如果您的命令是显示在菜单上，您必须添加<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute>到你的 VSPackage，以及如何使用作为菜单的名称或其资源 ID 的值

```
[ProvideMenuResource("Menus.ctmenu", 1)]
...
    public sealed class MyPackage : Package
    {.. ..}

```

 此外，必须注册与命令<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>。 可以使用来获取此服务<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>方法，如果你的 VSPackage 派生自<xref:Microsoft.VisualStudio.Shell.Package>。

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
 有多种方法来实现命令。 如果您想静态菜单命令，这是始终显示相同方式，在相同菜单上的命令，创建该命令使用<xref:System.ComponentModel.Design.MenuCommand>上一节中的示例中所示。 若要创建静态命令，必须提供的事件处理程序负责执行该命令。 由于该命令始终启用且可见，则无需向 Visual Studio 提供其状态。 如果你想要更改根据某些条件命令的状态，可以创建命令的实例作为<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>类，并在其构造函数，提供一个事件处理程序，以执行命令和一个`QueryStatus`处理程序来通知 VisualStudio 命令的状态发生更改时。 您还可以实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>因为命令类或一部分，您可以实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>如果你要作为项目的一部分提供的命令。 两个接口和<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>类所有具有方法，以通知的命令的状态中的更改的 Visual Studio 和其他方法，都执行此命令。

 当命令添加到命令服务时，它只是一种命令链。 实现该命令的状态通知和执行方法时，请注意仅针对该特定命令提供，并将链中传递到其他命令的所有其他情况。 如果您不能传递命令 (通常通过返回<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>)，Visual Studio 可能会停止正常工作。

## <a name="querystatus-methods"></a>QueryStatus 方法
 如果要实现任一<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法或<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>方法中检查的命令所属命令集的 GUID 和命令的 ID。 请遵循这些指导：

- 如果无法识别的 GUID，这两种方法的实现必须返回<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP>。

- 如果这两种方法的实现可以识别的 GUID，但不是实现了该命令，则该方法应返回<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>。

- 如果这两种方法的实现可以识别的 GUID 和命令，则该方法的每个命令的命令标志字段应设置 (在`prgCmds`参数) 通过使用以下<xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF>标志：

  - `OLECMDF_SUPPORTED`：支持该命令。

  - `OLECMDF_INVISIBLE`：该命令不应是可见的。

  - `OLECMDF_LATCHED`：此命令上切换，似乎已签入。

  - `OLECMDF_ENABLED`：启用命令。

  - `OLECMDF_DEFHIDEONCTXTMENU`：如果它显示快捷菜单上，应隐藏该命令。

  - `OLECMDF_NINCHED`：该命令是菜单控制器且未启用，但其下拉列表菜单列表不为空，并且仍然可用。 （很少使用此标志。）

- 如果该命令中定义，则 *.vsct*文件具有`TextChanges`标志，请将以下参数：

  - 设置`rgwz`元素的`pCmdText`的新文本的命令的参数。

  - 设置`cwActual`元素的`pCmdText`命令字符串的大小参数。

此外，请确保当前上下文不是自动化函数，除非您的命令专门用于处理自动化功能。

若要指示支持特定的命令，返回<xref:Microsoft.VisualStudio.VSConstants.S_OK>。 对于所有其他命令，返回<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>。

在以下示例中，`QueryStatus`方法首先可确保上下文不是自动化函数，然后查找正确的命令集 GUID 和命令 id。 命令本身设置为启用和支持。 不支持任何其他命令。

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
 实现`Exec`方法类似于实现`QueryStatus`方法。 首先，请确保上下文不是自动化函数。 然后，测试的 GUID 和命令 id。 如果 GUID 或无法识别的命令 ID，返回<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>。

 若要处理该命令，执行它，并返回<xref:Microsoft.VisualStudio.VSConstants.S_OK>如果执行成功。 你的命令负责进行错误检测和通知;因此，执行失败时返回错误代码。 下面的示例演示了应如何实现执行方法。

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
