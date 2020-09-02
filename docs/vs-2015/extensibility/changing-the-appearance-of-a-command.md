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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184510"
---
# <a name="changing-the-appearance-of-a-command"></a>更改命令的外观
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过更改命令的外观向用户提供反馈。 例如，你可能希望某个命令在不可用时的外观有所不同。 您可以使命令可用或不可用、隐藏或显示它们，或在菜单中选中或取消选中它们。  
  
 若要更改命令的外观，请执行以下操作之一：  
  
- 在命令表文件的命令定义中指定适当的标志。  
  
- 使用 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> 服务。  
  
- 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口并修改原始命令对象。  
  
  以下步骤演示了如何使用托管包框架 (MPF) 查找和更新命令的外观。  
  
### <a name="to-change-the-appearance-of-a-menu-command"></a>更改菜单命令的外观  
  
1. 按照 [更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md) 中的说明创建一个名为的菜单项 `New Text` 。  
  
2. 在 ChangeMenuText.cs 文件中，添加以下 using 语句：  
  
    ```csharp  
    using System.Security.Permissions;  
    ```  
  
3. 在 ChangeMenuTextPackageGuids.cs 文件中，添加以下行：  
  
    ```csharp  
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file  
    ```  
  
4. 在 ChangeMenuText.cs 文件中，将 ShowMessageBox 方法中的代码替换为以下代码：  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)  
    {  
        var command = sender as OleMenuCommand;  
        if (command.Text == "New Text")  
            ChangeMyCommand(command.CommandID.ID, false);}  
    }  
    ```  
  
5. 获取要从对象更新的命令 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> ，然后在命令对象上设置相应的属性。 例如，下面的方法使 VSPackage 命令集中的指定命令可用或不可用。 下面的代码在单击菜单项后将其命名为 " `New Text` 不可用"。  
  
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
  
7. 在 " **工具** " 菜单上，单击 " **调用 ChangeMenuText** " 命令。 此时，命令名称会 **调用 ChangeMenuText**，因此命令处理程序不会调用 ChangeMyCommand ( # A1。  
  
8. 此时，你应该会看到 " **工具** " 菜单上的 " **新文本**"。 单击 " **新文本**"。 该命令现在应显示为灰色。  
  
## <a name="see-also"></a>另请参阅  
 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)   
 [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
