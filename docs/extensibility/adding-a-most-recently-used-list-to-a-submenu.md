---
title: 向子菜单添加最近使用过的列表 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MRU lists
- menus, creating MRU list
- most recently used
ms.assetid: 27d4bbcf-99b1-498f-8b66-40002e3db0f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5624fe4a4f3c9ba774313e862f9e84a6f6d70862
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84183270"
---
# <a name="add-a-most-recently-used-list-to-a-submenu"></a>向子菜单添加最近使用过的列表
本演练基于[向菜单添加子](../extensibility/adding-a-submenu-to-a-menu.md)菜单中的演示，并演示如何向子菜单添加动态列表。 动态列表构成了创建最近使用的（MRU）列表的基础。

动态菜单列表以菜单上的占位符开头。 每次显示菜单时，Visual Studio 集成开发环境（IDE）都向 VSPackage 请求应显示在占位符中的所有命令。 动态列表可以出现在菜单上的任何位置。 但是，动态列表通常存储在子菜单上或菜单底部。 通过使用这些设计模式，可以在不影响菜单上其他命令的位置的情况下，使命令的动态列表展开和收缩。 在本演练中，动态 MRU 列表显示在现有子菜单的底部，并与子菜单的其余部分分隔开。

从技术上讲，动态列表还可以应用于工具栏。 但是，我们会反对这种用法，因为工具栏应保持不变，除非用户执行特定步骤来更改它。

本演练将创建四个项的 MRU 列表，每次选择其中一项时，这些项都将更改顺序（选定项移至列表顶部）。

有关菜单和 *.vsct*文件的详细信息，请参阅[命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

## <a name="prerequisites"></a>先决条件
要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。

## <a name="create-an-extension"></a>创建一个扩展

- 按照[将子菜单添加到菜单](../extensibility/adding-a-submenu-to-a-menu.md)中的过程创建在以下过程中修改的子菜单。

  本演练中的过程假定 VSPackage 的名称是 `TestCommand` ，它是在[Visual Studio 菜单栏的 "添加" 菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)中使用的名称。

## <a name="create-a-dynamic-item-list-command"></a>创建动态项列表命令

1. 打开*TestCommandPackage. .vsct*。

2. 在 `Symbols` 部分中，在 `GuidSymbol` 名为 guidTestCommandPackageCmdSet 的节点中，添加 `MRUListGroup` 组和命令的符号 `cmdidMRUList` ，如下所示。

    ```xml
    <IDSymbol name="MRUListGroup" value="0x1200"/>
    <IDSymbol name="cmdidMRUList" value="0x0200"/>
    ```

3. 在 `Groups` 部分中，在现有组条目后面添加声明的组。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"
            priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

4. 在 `Buttons` 部分中，添加一个节点，用于表示新声明的命令，位于现有按钮项之后。

    ```xml
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidMRUList"
        type="Button" priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="MRUListGroup" />
        <CommandFlag>DynamicItemStart</CommandFlag>
        <Strings>
            <CommandName>cmdidMRUList</CommandName>
            <ButtonText>MRU Placeholder</ButtonText>
        </Strings>
    </Button>
    ```

    `DynamicItemStart`标志允许动态生成命令。

5. 生成项目并启动调试以测试新命令的显示。

    在 " **TestMenu** " 菜单上，单击 "新建" 子菜单，单击 "**子菜单**" 以显示 "新命令， **MRU 占位符**"。 在下一过程中实现了动态 MRU 命令列表后，每次打开子菜单时，此命令标签都将替换为该列表。

## <a name="filling-the-mru-list"></a>填充 MRU 列表

1. 在*TestCommandPackageGuids.cs*中，在类定义中的现有命令 id 后面添加以下行 `TestCommandPackageGuids` 。

    ```csharp
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file
    public const uint cmdidMRUList = 0x200;
    ```

2. 在*TestCommand.cs*中，添加以下 using 语句。

    ```csharp
    using System.Collections;
    ```

3. 在最后一次 AddCommand 调用之后，在 Testcommand (构造函数中添加以下代码。 `InitMRUMenu`稍后将定义

    ```csharp
    this.InitMRUMenu(commandService);
    ```

4. 在 Testcommand (类中添加以下代码。 此代码将初始化表示要在 MRU 列表中显示的项的字符串列表。

    ```csharp
    private int numMRUItems = 4;
    private int baseMRUID = (int)TestCommandPackageGuids.cmdidMRUList;
    private ArrayList mruList;

    private void InitializeMRUList()
    {
        if (null == this.mruList)
        {
            this.mruList = new ArrayList();
            if (null != this.mruList)
            {
                for (int i = 0; i < this.numMRUItems; i++)
                {
                    this.mruList.Add(string.Format(CultureInfo.CurrentCulture,
                        "Item {0}", i + 1));
                }
            }
        }
    }
    ```

5. 在 `InitializeMRUList` 方法之后，添加 `InitMRUMenu` 方法。 这会初始化 MRU list 菜单命令。

    ```csharp
    private void InitMRUMenu(OleMenuCommandService mcs)
    {
        InitializeMRUList();
        for (int i = 0; i < this.numMRUItems; i++)
        {
            var cmdID = new CommandID(
                new Guid(TestCommandPackageGuids.guidTestCommandPackageCmdSet), this.baseMRUID + i);
            var mc = new OleMenuCommand(
                new EventHandler(OnMRUExec), cmdID);
            mc.BeforeQueryStatus += new EventHandler(OnMRUQueryStatus);
            mcs.AddCommand(mc);
        }
    }
    ```

    必须为 MRU 列表中的每个可能项创建一个菜单命令对象。 IDE `OnMRUQueryStatus` 为 MRU 列表中的每个项调用方法，直到没有更多的项。 在托管代码中，IDE 知道没有更多的项是先创建所有可能的项。 如果需要，可以在 `mc.Visible = false;` 创建菜单命令后，使用将其他项标记为第一次为不可见。 以后可以使用方法中的使用这些项 `mc.Visible = true;` `OnMRUQueryStatus` 。

6. 在 `InitMRUMenu` 方法之后添加以下 `OnMRUQueryStatus` 方法。 这是为每个 MRU 项设置文本的处理程序。

    ```csharp
    private void OnMRUQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                menuCommand.Text = this.mruList[MRUItemIndex] as string;
            }
        }
    }
    ```

7. 在 `OnMRUQueryStatus` 方法之后添加以下 `OnMRUExec` 方法。 这是用于选择 MRU 项的处理程序。 此方法将选定的项移动到列表的顶部，然后在消息框中显示选定项。

    ```csharp
    private void OnMRUExec(object sender, EventArgs e)
    {
        var menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                string selection = this.mruList[MRUItemIndex] as string;
                for (int i = MRUItemIndex; i > 0; i--)
                {
                    this.mruList[i] = this.mruList[i - 1];
                }
                this.mruList[0] = selection;
                System.Windows.Forms.MessageBox.Show(
                    string.Format(CultureInfo.CurrentCulture,
                                  "Selected {0}", selection));
            }
        }
    }
    ```

## <a name="testing-the-mru-list"></a>测试 MRU 列表

1. 生成项目并启动调试。

2. 在 " **TestMenu** " 菜单上，单击 "**调用 testcommand (**"。 执行此操作将显示一个消息框，指示已选择此命令。

    > [!NOTE]
    > 若要强制 VSPackage 加载并正确显示 MRU 列表，需要执行此步骤。 如果跳过此步骤，则不会显示 MRU 列表。

3. 在 "**测试" 菜单**菜单上，单击 "**子菜单**"。 在子菜单的末尾，分隔符下显示了四个项的列表。 单击 "**项目 3**" 时，将出现一个消息框并显示文本 "已**选择项 3**"。 （如果未显示四项列表，请确保已按照前面步骤中的说明进行操作。）

4. 再次打开子菜单。 请注意，**项 3**现在位于列表的顶部，而其他项已向下推送一个位置。 再次单击**第3项**，请注意，消息框仍显示**选定的项 3**，这表示文本已正确地与命令标签一起移动到新位置。

## <a name="see-also"></a>请参阅
- [动态添加菜单项](../extensibility/dynamically-adding-menu-items.md)
