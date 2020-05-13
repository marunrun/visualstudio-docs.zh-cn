---
title: 更改菜单命令的文本 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ff6af7bdd64342e86201af79dbe5c7968b247d6b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739843"
---
# <a name="change-the-text-of-a-menu-command"></a>更改菜单命令的文本
以下步骤演示如何使用<xref:System.ComponentModel.Design.IMenuCommandService>服务更改菜单命令的文本标签。

## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>使用 IMenu命令服务更改菜单命令标签

1. 创建`MenuText`一个 VSIX 项目，该项目名为 **"更改菜单文本**"的菜单命令。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 在 *.vsct*文件中，将`TextChanges`标志添加到菜单命令，如以下示例所示。

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

3. 在*ChangeMenuText.cs*文件中，创建一个事件处理程序，该处理程序将在显示菜单命令之前调用。

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

    还可以<xref:System.ComponentModel.Design.MenuCommand.Visible%2A>通过更改<xref:System.ComponentModel.Design.MenuCommand.Checked%2A><xref:System.ComponentModel.Design.MenuCommand.Enabled%2A><xref:Microsoft.VisualStudio.Shell.OleMenuCommand>对象 上的 、 和 属性来更新此方法中的菜单命令的状态。

4. 在 ChangeMenuText 构造函数中，将原始命令初始化和放置代码替换为代码，该代码<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>创建一个（`MenuCommand`而不是 ）表示菜单命令、添加<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>事件处理程序并将菜单命令授予菜单命令到菜单命令服务的代码。

    下面是它应该是什么样子：

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

5. 生成项目并启动调试。 视觉工作室的实验实例出现。

6. 在 **"工具"** 菜单上，您应该看到名为 **"调用更改菜单文本**"的命令。

7. 单击该命令。 您应该会看到消息框，宣布已调用**MenuItem 回调**。 当您关闭消息框时，您应该看到"工具"菜单上的命令的名称现在是 **"新文本**"。
