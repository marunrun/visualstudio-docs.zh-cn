---
title: 更改命令的外观 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, changing appearance
- menu commands, changing appearance
- menus, changing command appearance
ms.assetid: da2474fa-f92d-4e9e-b8bf-67c61bf249c2
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4741059410e052c571d77088b9cbe109fb651642
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184510"
---
# <a name="changing-the-appearance-of-a-command"></a>更改命令的外观
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过更改命令的外观，可以向用户提供反馈。 例如，可能想要看起来不同，它不可用时的命令。 可以使命令可用或不可用、 隐藏或显示它们，或选中或取消它们选中的菜单上。  
  
 若要更改命令的外观，请执行以下操作之一：  
  
- 在命令表文件中的命令定义中指定适当的标记。  
  
- 使用<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>服务。  
  
- 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口，并修改原始命令对象。  
  
  以下步骤说明如何查找和使用托管包框架 (MPF) 更新命令的外观。  
  
### <a name="to-change-the-appearance-of-a-menu-command"></a>若要更改菜单命令的外观  
  
1. 按照中的说明[更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md)若要创建的菜单项名为`New Text`。  
  
2. 在 ChangeMenuText.cs 文件中，添加以下 using 语句：  
  
    ```csharp  
    using System.Security.Permissions;  
    ```  
  
3. 在 ChangeMenuTextPackageGuids.cs 文件中，添加以下行：  
  
    ```csharp  
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file  
    ```  
  
4. 在 ChangeMenuText.cs 文件中，将替换以下为 ShowMessageBox 方法中的代码：  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)  
    {  
        var command = sender as OleMenuCommand;  
        if (command.Text == "New Text")  
            ChangeMyCommand(command.CommandID.ID, false);}  
    }  
    ```  
  
5. 获取你想要从更新的命令<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>对象，然后在 command 对象上设置适当的属性。 例如，以下方法可指定的命令的 VSPackage 命令集可用或不可用。 下面的代码使名为菜单项`New Text`后单击它不可用。  
  
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
        return cmdUpdated;    }  
    }  
    ```  
  
6. 生成项目并启动调试。 应显示 Visual Studio 的实验实例。  
  
7. 上**工具**菜单上，单击**调用 ChangeMenuText**命令。 此时该命令名是**调用 ChangeMenuText**，因此，命令处理程序不会调用 ChangeMyCommand()。  
  
8. 上**工具**菜单现在应看到**新文本**。 单击**新文本**。 现在，该命令应灰显。  
  
## <a name="see-also"></a>请参阅  
 [命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)   
 [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
