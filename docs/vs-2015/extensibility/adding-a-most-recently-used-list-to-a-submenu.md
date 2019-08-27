---
title: 添加最近使用过的子菜单上的列表 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- MRU lists
- menus, creating MRU list
- most recently used
ms.assetid: 27d4bbcf-99b1-498f-8b66-40002e3db0f8
caps.latest.revision: 47
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: caccf8923a8614ceedb7198e218ca2bb14bb7ec0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444873"
---
# <a name="adding-a-most-recently-used-list-to-a-submenu"></a>将最近使用的列表添加到子菜单
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练基于中的演示[将子菜单添加到菜单](../extensibility/adding-a-submenu-to-a-menu.md)，并演示如何将动态列表添加到子菜单。 动态列表窗体创建最近使用过的 (MRU) 列表的基础。  
  
 动态菜单列表开始菜单上的占位符。 每次显示菜单，Visual Studio 集成的开发环境 (IDE) 要求的所有命令都应显示在占位符都提供 VSPackage。 在菜单上，动态列表可以出现任意位置。 但是，动态列表将通常存储，并显示本身，位于子菜单或菜单的底部。 通过使用这些设计模式，可以使命令进行扩展和收缩而不会影响其他命令的菜单上的位置的动态列表。 在此演练中，动态 MRU 列表显示在现有子菜单，通过行分隔子菜单的其余部分的底部。  
  
 从技术上讲，动态列表还可以应用到工具栏。 但是，我们建议不要使用情况因为工具栏应保持不变，除非用户执行特定步骤，以便对其进行更改。  
  
 本演练创建的每次选择其中一个更改它们的顺序的四个项目的 MRU 列表 （选定的项将移至列表的顶部）。  
  
 有关菜单和.vsct 文件的详细信息，请参阅[命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。  
  
## <a name="prerequisites"></a>系统必备  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="creating-an-extension"></a>创建扩展  
  
- 按照中的过程[将子菜单添加到菜单](../extensibility/adding-a-submenu-to-a-menu.md)以下过程中创建修改的子菜单。  
  
  在本演练中的过程假定 VSPackage 的名称是`TopLevelMenu`，这是使用中的名称[将菜单添加到 Visual Studio 菜单栏](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)。  
  
## <a name="creating-a-dynamic-item-list-command"></a>创建动态项列表命令  
  
1. 打开 TestCommandPackage.vsct。  
  
2. 在`Symbols`部分中，在`GuidSymbol`节点中名为 guidTestCommandPackageCmdSet，添加的符号`MRUListGroup`组和`cmdidMRUList`命令时，按如下所示。  
  
    ```csharp  
    <IDSymbol name="MRUListGroup" value="0x1200"/>  
    <IDSymbol name="cmdidMRUList" value="0x0200"/>  
    ```  
  
3. 在`Groups`部分中，现有的组条目后添加声明的组。  
  
    ```cpp  
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"   
           priority="0x0100">  
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>  
    </Group>  
  
    ```  
  
4. 在`Buttons`部分中，添加节点来表示新声明的命令之后的现有按钮项。  
  
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
  
     `DynamicItemStart`标志可使要动态生成的命令。  
  
5. 生成项目并开始调试以测试新的命令的显示。  
  
     上**TestMenu**菜单上，单击新的子菜单**子菜单**，以显示新的命令**MRU 占位符**。 在下一个过程中实现动态的 MRU 列表的命令后，每当打开子菜单时，将替换此命令标签由该列表。  
  
## <a name="filling-the-mru-list"></a>填充 MRU 列表  
  
1. TestCommandPackageGuids.cs，在后面的现有命令 Id 中添加以下行`TestCommandPackageGuids`类定义。  
  
    ```csharp  
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file  
    public const uint cmdidMRUList = 0x200;  
    ```  
  
2. 在 TestCommand.cs 添加以下 using 语句。  
  
    ```csharp  
    using System.Collections;  
    ```  
  
3. 最后一个 AddCommand 调用后 TestCommand 构造函数中添加以下代码。 `InitMRUMenu`将在以后定义  
  
    ```csharp  
    this.InitMRUMenu(commandService);  
    ```  
  
4. TestCommand 类中添加以下代码。 此代码将初始化的字符串表示要在 MRU 列表上显示的项的列表。  
  
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
  
5. 之后`InitializeMRUList`方法中，添加`InitMRUMenu`方法。 此初始化 MRU 列表菜单命令。  
  
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
  
     MRU 列表中，必须创建每个可能的项的菜单命令对象。 IDE 调用`OnMRUQueryStatus`MRU 列表，直到没有更多的项中的每个项的方法。 在托管代码中，IDE 知道有没有其他项的唯一方法是先创建所有可能的项。 如果你想，您可以将附加项标记为不可见时首先通过使用`mc.Visible = false;`创建菜单命令之后。 这些项可以然后让用户看到更高版本使用`mc.Visible = true;`在`OnMRUQueryStatus`方法。  
  
6. 之后`InitMRUMenu`方法中，添加以下`OnMRUQueryStatus`方法。 这是设置每个 MRU 项的文本的处理程序。  
  
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
  
7. 之后`OnMRUQueryStatus`方法中，添加以下`OnMRUExec`方法。 这是用于选择 MRU 项的处理程序。 此方法将所选的项移动到列表的顶部，然后在消息框中显示所选的项。  
  
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
  
#### <a name="to-test-the-mru-menu-list"></a>若要测试 MRU 菜单列表  
  
1. 生成项目并启动调试  
  
2. 上**TestMenu**菜单上，单击**调用 TestCommand**。 执行此操作将显示一个消息框，指示已选择的命令。  
  
    > [!NOTE]
    > 此步骤需要强制 VSPackage 加载并正确显示 MRU 列表。 如果跳过此步骤中，不显示 MRU 列表。  
  
3. 上**测试菜单**菜单上，单击**子菜单**。 在子菜单，如下一个分隔符的结尾显示的四个项列表。 当您单击**项 3**，应会显示一个消息框，将其显示文本"所选的项目 3"。 （如果未显示的四个项的列表，请确保您已按照前面步骤中的说明进行操作。）  
  
4. 再次打开子菜单。 请注意，**项 3**现在位于列表的顶部和其他项已推送下移一个位置。 单击**项 3**再次并注意该消息框仍显示"所选的项目 3"，以指示文本已正确地移动到以及命令标签的新位置。  
  
## <a name="see-also"></a>请参阅  
 [动态添加菜单项](../extensibility/dynamically-adding-menu-items.md)
