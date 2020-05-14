---
title: 将最近使用的列表添加到子菜单 |微软文档
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
ms.openlocfilehash: cf389c0da7ec0aafb6e47dae8f09ffdc3b1d1e4d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740299"
---
# <a name="add-a-most-recently-used-list-to-a-submenu"></a>将最近使用的列表添加到子菜单
本演练基于[将子菜单添加到菜单](../extensibility/adding-a-submenu-to-a-menu.md)中的演示，并演示如何向子菜单添加动态列表。 动态列表构成创建最近使用 （MRU） 列表的基础。

动态菜单列表以菜单上的占位符开头。 每次显示菜单时，Visual Studio 集成开发环境 （IDE） 都会向 VSPackage 询问应在占位符处显示的所有命令。 动态列表可能发生在菜单上的任意位置。 但是，动态列表通常由自身存储在子菜单或菜单底部。 通过使用这些设计模式，您可以启用命令的动态列表来展开和收缩，而不会影响菜单上其他命令的位置。 在本演练中，动态 MRU 列表显示在现有子菜单的底部，由一行与子菜单的其余部分分开。

从技术上讲，动态列表也可以应用于工具栏。 但是，我们阻止使用该工具栏，因为工具栏应保持不变，除非用户采取特定步骤来更改它。

本演练创建一个 MRU 列表，其中四个项目在每次选择其中一个项目时都会更改其顺序（所选项移动到列表顶部）。

有关菜单和 *.vsct*文件的详细信息，请参阅[命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

## <a name="prerequisites"></a>先决条件
要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[可视化工作室 SDK](../extensibility/visual-studio-sdk.md)。

## <a name="create-an-extension"></a>创建一个扩展

- 按照将[子菜单添加到菜单](../extensibility/adding-a-submenu-to-a-menu.md)中的过程来创建在以下过程中修改的子菜单。

  本演练中的过程假定 VSPackage 的名称为`TopLevelMenu`，这是在[将菜单添加到 Visual Studio 菜单栏](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)中使用的名称。

## <a name="create-a-dynamic-item-list-command"></a>创建动态项列表命令

1. 打开*测试命令包.vsct*.

2. 在名为`Symbols`guidTestCommandPackageCmdSet 的`GuidSymbol`节点中，添加`MRUListGroup`组和命令的`cmdidMRUList`符号，如下所示。

    ```csharp
    <IDSymbol name="MRUListGroup" value="0x1200"/>
    <IDSymbol name="cmdidMRUList" value="0x0200"/>
    ```

3. 在节中`Groups`，在现有组条目之后添加声明的组。

    ```cpp
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"
            priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>

    ```

4. 在节中`Buttons`，在现有按钮条目之后添加一个节点以表示新声明的命令。

    ```csharp
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

    该`DynamicItemStart`标志允许动态生成命令。

5. 生成项目并开始调试以测试新命令的显示。

    在 **"测试菜单"** 菜单上，单击新的子菜单"**子菜单**"以显示新命令**MRU 占位符**。 在下一个过程中实现命令的动态 MRU 列表后，每次打开子菜单时，此命令标签都将替换为该列表。

## <a name="filling-the-mru-list"></a>填写 MRU 列表

1. 在*TestCommandPackageGuids.cs*中，在`TestCommandPackageGuids`类定义中的现有命令指示后添加以下行。

    ```csharp
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file
    public const uint cmdidMRUList = 0x200;
    ```

2. 在*TestCommand.cs*添加以下 using 语句。

    ```csharp
    using System.Collections;
    ```

3. 在上次 AddCommand 调用之后的 TestCommand 构造函数中添加以下代码。 稍后将`InitMRUMenu`定义

    ```csharp
    this.InitMRUMenu(commandService);
    ```

4. 在 TestCommand 类中添加以下代码。 此代码初始化表示要在 MRU 列表中显示的项的字符串列表。

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

5. 在`InitializeMRUList`方法之后，添加`InitMRUMenu`方法。 这将初始化 MRU 列表菜单命令。

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

    您必须为 MRU 列表中的每个可能项创建菜单命令对象。 IDE 调用`OnMRUQueryStatus`MRU 列表中每个项的方法，直到没有更多项。 在托管代码中，IDE 知道没有更多项的唯一方法是首先创建所有可能的项目。 如果需要，可以在创建菜单命令后使用`mc.Visible = false;`，将其他项标记为最初不可见。 然后，可以使用`mc.Visible = true;``OnMRUQueryStatus`方法稍后使这些项目可见。

6. 在`InitMRUMenu`方法之后，添加以下`OnMRUQueryStatus`方法。 这是为每个 MRU 项设置文本的处理程序。

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

7. 在`OnMRUQueryStatus`方法之后，添加以下`OnMRUExec`方法。 这是用于选择 MRU 项的处理程序。 此方法将所选项移动到列表顶部，然后在消息框中显示所选项。

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

2. 在 **"测试菜单"** 菜单上，单击 **"调用测试命令**"。 执行此操作将显示一个消息框，指示该命令已选定。

    > [!NOTE]
    > 此步骤需要强制 VSPackage 加载并正确显示 MRU 列表。 如果跳过此步骤，将不会显示 MRU 列表。

3. 在 **"测试菜单"菜单上**，单击 **"子菜单**"。 四个项目的列表显示在子菜单的末尾，位于分隔符下方。 单击项目**3**时，应显示一个消息框并显示文本 **"选定项目 3**"。 （如果未显示四个项目的列表，请确保已遵循前面的步骤中的说明。

4. 再次打开子菜单。 请注意，**项目 3**现在位于列表的顶部，其他项目已向下推一个位置。 再次单击**项目 3**并注意到消息框仍显示 **"选定项目 3"，** 表示文本与命令标签一起正确移动到新位置。

## <a name="see-also"></a>请参阅
- [动态添加菜单项](../extensibility/dynamically-adding-menu-items.md)
