---
title: 更改命令的外观 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, changing appearance
- menu commands, changing appearance
- menus, changing command appearance
ms.assetid: da2474fa-f92d-4e9e-b8bf-67c61bf249c2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 653f516dda89f4895b8d19d77f7f49bf9c6aa45b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739861"
---
# <a name="change-the-appearance-of-a-command"></a>更改命令的外观
您可以通过更改命令的外观向用户提供反馈。 例如，您可能希望命令在不可用时看起来不同。 可以使命令可用或不可用，隐藏或显示它们，或检查或取消选中它们。

要更改命令的外观，可以执行以下操作之一：

- 在命令表文件中的命令定义中指定适当的标志。

- 使用<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>该服务。

- 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口并修改原始命令对象。

  以下步骤演示如何使用托管包框架 （MPF） 查找和更新命令的外观。

### <a name="to-change-the-appearance-of-a-menu-command"></a>更改菜单命令的外观

1. 按照[更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md)中的说明创建名为 的`New Text`菜单项。

2. 在*ChangeMenuText.cs*文件中，添加以下使用语句：

    ```csharp
    using System.Security.Permissions;
    ```

3. 在*ChangeMenuTextPackageGuids.cs*文件中，添加以下行：

    ```csharp
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    ```

4. 在*ChangeMenuText.cs*文件中，将 ShowMessageBox 方法中的代码替换为以下内容：

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var command = sender as OleMenuCommand;
        if (command.Text == "New Text")
            ChangeMyCommand(command.CommandID.ID, false);
    }
    ```

5. 获取要从对象更新的命令，<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>然后在命令对象上设置相应的属性。 例如，以下方法使 VSPackage 命令集中的指定命令可用或不可用。 以下代码使名为"菜单项"`New Text`的菜单项在单击后不可用。

    ```csharp
    public bool ChangeMyCommand(int cmdID, bool enableCmd)
    {
        bool cmdUpdated = false;
        var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService))
            as OleMenuCommandService;
        var newCmdID = new CommandID(new Guid(ChangeMenuTextPackageGuids.guidChangeMenuTextPackageCmdSet), cmdID);
        MenuCommand mc = mcs.FindCommand(newCmdID);
        if (mc != null)
        {
            mc.Enabled = enableCmd;
            cmdUpdated = true;
        }
        return cmdUpdated;
    }
    ```

6. 生成项目并启动调试。 应出现视觉工作室的实验实例。

7. 在 **"工具"** 菜单上，单击 **"调用更改菜单文本"** 命令。 此时，命令名称是 **"调用更改菜单文本**"，因此命令处理程序不调用**ChangeMyCommand（）**。

8. 在 **"工具"** 菜单上，您现在应该看到 **"新文本**"。 单击 **"新文本**"。 该命令现在应该灰显。

## <a name="see-also"></a>请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
- [VS包如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [可视化工作室命令表 （.Vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
