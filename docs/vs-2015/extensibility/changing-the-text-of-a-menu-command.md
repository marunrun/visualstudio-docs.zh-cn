---
title: 更改菜单命令的文本 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d8fd3fc01a5dd3e10e633b876b719695d6b26c18
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184496"
---
# <a name="changing-the-text-of-a-menu-command"></a>更改菜单命令的文本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下步骤演示如何使用更改菜单命令的文本标签<xref:System.ComponentModel.Design.IMenuCommandService>服务。  
  
## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>更改具有 IMenuCommandService 的菜单命令标签  
  
1. 创建一个名为的 VSIX 项目`MenuText`菜单命令与名为**ChangeMenuText**。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
2. 在.vstc 文件中，添加`TextChanges`标志到菜单命令中，如以下示例所示。  
  
    ```xml  
    <Button guid="guidChangeMenuTextPackageCmdSet" id="ChangeMenuTextId" priority="0x0100" type="Button">  
        <Parent guid="guidChangeMenuTextPackageCmdSet" id="MyMenuGroup" />  
        <Icon guid="guidImages" id="bmpPic1" />  
        <CommandFlag>TextChanges</CommandFlag>  
        <Strings>  
            <ButtonText>Invoke ChangeMenuText</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
3. 在 ChangeMenuText.cs 文件中，创建的事件处理程序将在显示的菜单命令之前调用。  
  
    ```csharp  
    private void OnBeforeQueryStatus(object sender, EventArgs e)  
    {  
        var myCommand = sender as OleMenuCommand;  
        if (null != myCommand)  
        {  
            myCommand.Text = "New Text";  
                    }  
    }  
    ```  
  
     此外可以通过更改来更新此方法中的菜单命令的状态<xref:System.ComponentModel.Design.MenuCommand.Visible%2A>， <xref:System.ComponentModel.Design.MenuCommand.Checked%2A>，并<xref:System.ComponentModel.Design.MenuCommand.Enabled%2A>上的属性<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>对象。  
  
4. 在 ChangeMenuText 构造函数中，用创建的代码替换原始命令初始化和放置代码<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>(而非`MenuCommand`)，表示菜单命令，将添加<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>事件处理程序，并提供菜单到菜单命令服务的命令。  
  
     下面是什么它应如下所示：  
  
    ```csharp  
    private ChangeMenuText(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
            EventHandler eventHandler = this.ShowMessageBox;  
            OleMenuCommand menuItem = new OleMenuCommand(ShowMessageBox, menuCommandID);  
            menuItem.BeforeQueryStatus +=  
                new EventHandler(OnBeforeQueryStatus);  
            commandService.AddCommand(menuItem);  
        }  
    }  
    ```  
  
5. 生成项目并启动调试。 将显示 Visual Studio 的实验实例。  
  
6. 上**工具**看到名为的命令菜单**调用 ChangeMenuText**。  
  
7. 单击该命令。 您应该看到消息框宣布推出 MenuItemCallback 已调用。 当您关闭消息框时，应看到工具菜单上的命令的名称现在是**新文本**。
