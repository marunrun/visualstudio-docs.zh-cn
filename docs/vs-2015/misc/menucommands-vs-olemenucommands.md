---
title: MenuCommands 与OleMenuCommands |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- commands, creating in VSPackages
- command buttons, creating and placing
- menus, creating commands
ms.assetid: 553d5e07-3e19-4aba-b490-6c7dd05fd82e
caps.latest.revision: 46
manager: jillfra
ms.openlocfilehash: 42c471ca924bfded62db32a956a26c07240459eb
ms.sourcegitcommit: 3cc73e74921a9ceb622542e0e263abeebc455c00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624455"
---
# <a name="menucommands-vs-olemenucommands"></a>MenuCommands 与OleMenuCommands
可以通过从派生来创建菜单命令<xref:System.ComponentModel.Design.MenuCommand>或从<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>对象，并实现相应的事件处理程序。 在大多数情况下可以使用 <xref:System.ComponentModel.Design.MenuCommand>，就和 VSPackage 项目模板工作方式一样，但有时你可能需要使用 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand>。  
  
 VSPackage 对 IED 可提供的命令在用户可以使用前必须处于可见和启用状态。 当通过使用 Visual Studio Package 项目模板在 .vsct 文件中创建命令时，命令默认为可见和启用状态。 设置某些命令标志，如 `DynamicItemStart`，可以更改默认行为。 还可以通过访问与命令相关联的 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 对象在运行时更改代码中命令的可见性、已启用的状态以及其他属性。  
  
## <a name="prerequisites"></a>系统必备  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="template-locations-for-the-visual-studio-package-template"></a>“Visual Studio 包模板”的模板位置  
 你可以在“Visual Basic / 扩展性”  ，“C# / 可扩展性”  或“其他项目类型 / 扩展性”  下的“新项目”  对话框中找到 Visual Studio 包模板。  
  
## <a name="creating-a-command"></a>创建命令  
 在 .vct 文件中定义所有命令、命令组、菜单、工具栏和工具窗口。 有关详细信息，请参阅 [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。  
  
 如果使用包模板创建 VSPackage，请选择“菜单命令”  创建 .vsct 文件和定义默认菜单命令。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
#### <a name="to-add-a-command-to-the-ide"></a>将命令添加到 IDE  
  
1. 打开 .vst 文件。  
  
2. 在 `Symbols` 部分中，找到包含组和命令的 [GuidSymbol](../extensibility/guidsymbol-element.md) 元素。  
  
3. 为你想要添加的每个菜单、组或命名创建 [IDSymbol](../extensibility/idsymbol-element.md) 元素，如下面的示例所示。  
  
   ```xml
   <GuidSymbol name="guidButtonGroupCmdSet" value="{f69209e9-975a-4543-821d-1f4a2c52d737}">
     <IDSymbol name="MyMenuGroup" value="0x1020" />
     <IDSymbol name="cmdidMyCommand" value="0x0100" />
   </GuidSymbol>
   ```
      
    `name` 和 `GuidSymbol` 元素的 `IDSymbol` 特性为每个新建的菜单、组或命令提供 GUID:ID 对。 `guid` 表示为你的 VSPackage 定义的命令集。 你可以定义多个命令集。 每个 GUID:ID 对必须是唯一的。  
  
4. 在 [“按钮”](../extensibility/buttons-element.md) 部分中，创建 [“按钮”](../extensibility/button-element.md) 元素来定义该命令，如下面的示例中所示。  
  
   ```xml
   <Button guid="guidButtonGroupCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
     <Parent guid="guidButtonGroupCmdSet" id="MyMenuGroup" />
     <Icon guid="guidImages" id="bmpPic1" />
     <Strings>
       <CommandName>cmdidMyCommand</CommandName>
       <ButtonText>My Command name</ButtonText>
     </Strings>
   </Button>
   ``` 
     
   1. 设置 `guid` 和 `id` 字段以匹配新命令的 GUID:ID。  
  
   2. 设置 `priority` 特性。  
  
        .Vsct 使用 `priority` 特性来确定按钮在其父组中其他对象中的位置。  
  
        以上显示了具有较低优先级值的命令，或者在其左侧显示了具有较高优先级值的命令。 允许使用重复的优先级值，但具有同等优先级的命令的相对位置由运行时 Vspackage 的处理顺序决定，而这一顺序是无法预先确定的。  
  
        省略 `priority` 特性会将其值设置为 0。  
  
   3. 设置 `type` 特性。 在大多数情况下，其值将为 `"Button"`。 有关其他有效按钮类型的说明，请参阅 [Button Element](../extensibility/button-element.md)。  
  
5. 在按钮定义中，创建一个包含 [ButtonText](../extensibility/strings-element.md) 元素的 [Strings](../extensibility/buttontext-element.md) 元素以包含菜单名称（菜单在 IDE 中显示时），并包含一个 [CommandName](../extensibility/commandname-element.md) 元素以包含用于访问“命令”  窗口中的菜单的命令名称。  
  
    如果按钮文本字符串包含“&”字符，则用户可通过按 ALT 加上紧跟“&”之后的字符打开菜单。  
  
    添加 `Tooltip` 元素将导致用户将鼠标指针悬停于按钮上时会出现所包含的文本。  
  
6. 添加 [Icon](../extensibility/icon-element.md) 元素以指定将使用命令显示的图标（如果有的话）。 图标是为工具栏上的按钮设置的，而不是为菜单项设置的。 `guid` 元素的 `id` 和 `Icon` 必须匹配 [部分中定义的](../extensibility/bitmap-element.md) Bitmap `Bitmaps` 元素的对等项。  
  
7. 根据需要添加命令标志，以更改按钮的外观和行为。 若要执行此操作，请在菜单定义中添加 [CommandFlag](../extensibility/command-flag-element.md) 元素。  
  
8. 设置命令的父组。 父组可以是你创建的组、来自另一个包的组或来自 IDE 的组。 例如，若要将你的命令添加到 Visual Studio 编辑工具栏上“注释”按钮  和“删除评论”  按钮旁边，则将父级设置为 guidStdEditor:IDG_VS_EDITTOOLBAR_COMMENT。 如果父级是用户定义的组，则它必须是菜单的子级、工具栏或显示在 IDE 中的工具窗口。  
  
    你可以根据你的设计选择两种方式之一执行此操作：  
  
   - 在 `Button` 元素中，创建 [Parent](../extensibility/parent-element.md) 元素，并将其 `guid` 和 `id` 字段设置为将承载命名的组的 Guid 和 ID，该组也称为 *主父组*。  
  
        下面的示例定义了一个将显示在用户定义的菜单上的命令。  
  
       ```xml
       <Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
         <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
         <Icon guid="guidImages" id="bmpPic1" />
         <Strings>
           <CommandName>cmdidTestCommand</CommandName>
           <ButtonText>Test Command</ButtonText>
             </Strings>
       </Button>
       ```
      
   - 如果命令通过使用命令放置来定位，则可以忽略 `Parent` 元素。 在 [部分前创建](../extensibility/commandplacements-element.md) CommandPlacements `Symbols` 元素，然后添加具有命令的 [和](../extensibility/commandplacement-element.md) 的 `guid` CommandPlacement `id` 元素、 `priority`和父级，如下面的示例中所示。  
  
   ```xml
   <CommandPlacements>
     <CommandPlacement guid="guidButtonGroupCmdSet" id="cmdidMyCommand" priority="0x105">
       <Parent guid="guidButtonGroupCmdSet" id="MyMenuGroup" />
     </CommandPlacement>
   </CommandPlacements>
   ```
      
      创建具有相同 GUID:ID 和不同父级的多个命令放置会导致菜单在多个位置显示。 有关详细信息，请参见 [CommandPlacements](../extensibility/commandplacements-element.md) 元素。  
  
    有关命令组和设置父级的详细信息，请参阅[按钮创建可重用组](../extensibility/creating-reusable-groups-of-buttons.md)。  
  
   此时，该命令将在 IDE 中可见，但不具有任何功能。 如果该命令由包模板创建，在默认情况下它会具有一个显示消息的单击处理程序。  
  
## <a name="handling-the-new-command"></a>处理新命令  
 托管代码中的大多数命令都可以由管理包框架 (MPF) 通过将该命令与 <xref:System.ComponentModel.Design.MenuCommand> 对象或 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 对象关联并实现其事件处理程序来进行处理。  
  
 对于直接将 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口用于命令处理的代码，必须实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口及其方法。 两个最重要的方法为 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 和 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>。  
  
1. 获取 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> 实例，如下面的示例所示。  
  
     [!code-csharp[ButtonGroup#21](../snippets/csharp/VS_Snippets_VSSDK/buttongroup/cs/buttongrouppackage.cs#21)]  
  
2. 创建一个 <xref:System.ComponentModel.Design.CommandID> 对象，该对象将命令的 GUID 和 ID 作为其参数进行处理，如下面的示例中所示。  
  
     [!code-csharp[ButtonGroup#22](../snippets/csharp/VS_Snippets_VSSDK/buttongroup/cs/buttongrouppackage.cs#22)]  
  
     Visual Studio 包模板提供了两个集合： `GuidList` 和 `PkgCmdIDList`，以保留命令的 GUID 和 ID。 对于由模板添加的命令，会将其自动填充，但对于你手动添加的命令，你还必须将 ID 条目添加到 `PkgCmdIdList` 类。  
  
     或者，你可以使用 GUID 的原始字符串值和 ID 的整数值来填充 <xref:System.ComponentModel.Design.CommandID> 对象。  
  
3. 将与 <xref:System.ComponentModel.Design.MenuCommand> 一起指定处理命令的方法的 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 或 <xref:System.ComponentModel.Design.CommandID>对象进行实例化，如下面的示例所示。  
  
     [!code-csharp[ButtonGroup#23](../snippets/csharp/VS_Snippets_VSSDK/buttongroup/cs/buttongrouppackage.cs#23)]  
  
     <xref:System.ComponentModel.Design.MenuCommand> 适用于静态命令。 动态菜单项显示需要 QueryStatus 事件处理程序。 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 添加会在命令的主机菜单打开时发生的 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> 事件以及某些其他属性，例如 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.Text%2A>。  
  
     由包模板创建的命令默认传递给包类的 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 方法中的 `Initialize()` 对象。  
  
4. <xref:System.ComponentModel.Design.MenuCommand> 适用于静态命令。 动态菜单项显示需要 QueryStatus 事件处理程序。 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 添加会在命令的主机菜单打开时发生的 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> 事件以及某些其他属性，例如 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.Text%2A>。  
  
     由包模板创建的命令默认传递给包类的 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 方法中的 `Initialize()` 对象。 Visual Studio 向导通过使用 `Initialize` 实现 `MenuCommand`方法。 对于动态菜单项显示，必须将此更改为 `OleMenuCommand`，如下一步所示。 此外，若要更改菜单项文本，必须将 TextChanges 命令标志添加到.vsct 文件中的菜单命令按钮，如下面的示例所示  
  
    ```xml
    <Button guid="guidMenuTextCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
      <Parent guid="guidMenuTextCmdSet" id="MyMenuGroup" />
      <Icon guid="guidImages" id="bmpPic1" />
      <CommandFlag>TextChanges</CommandFlag>
      <Strings>
        <CommandName>cmdidMyCommand</CommandName>
        <ButtonText>My Command name</ButtonText>
      </Strings>
    </Button>
    ```
      
5. 将新菜单命令传递到 <xref:System.ComponentModel.Design.IMenuCommandService.AddCommand%2A> 接口中的 <xref:System.ComponentModel.Design.IMenuCommandService> 方法。 对于由包模板创建的命令，将默认完成的此操作，如下面的示例中所示  
  
     [!code-csharp[ButtonGroup#24](../snippets/csharp/VS_Snippets_VSSDK/buttongroup/cs/buttongrouppackage.cs#24)]  
  
6. 实现处理命令的方法。  
  
#### <a name="to-implement-querystatus"></a>实现 QueryStatus  
  
1. QueryStatus 事件在命令显示前发生。 通过此操作，可在命令到达用户之前在事件处理程序中设置该命令的属性。 仅添加为 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 对象的命令可以访问此方法。  
  
    在为处理该命令而创建的 `EventHandler` 对象中将 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> 对象添加到 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 事件，如下面的示例中所示（`menuItem` 是 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 实例）。  
  
    [!code-csharp[MenuText#14](../snippets/csharp/VS_Snippets_VSSDK/menutext/cs/menutextpackage.cs#14)]
    [!code-vb[MenuText#14](../snippets/visualbasic/VS_Snippets_VSSDK/menutext/vb/menutextpackage.vb#14)]  
  
    `EventHandler` 对象命名为查询菜单命令状态时调用的方法的名称。  
  
2. 实现该命令的查询状态处理程序的方法。 `object` `sender` 参数可强制转换为 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 对象（此对象用于设置菜单命令的各种特性），包括文本。 下表显示对应于 <xref:System.ComponentModel.Design.MenuCommand> 标志的 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 类（MPF 类 <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> 的派生来源）上的属性。  
  
   |MenuCommand 属性|OLECMDF 标志|  
   |--------------------------|------------------|  
   |<xref:System.ComponentModel.Design.MenuCommand.Checked%2A> = `true`|<xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF>|  
   |<xref:System.ComponentModel.Design.MenuCommand.Visible%2A> = `false`|<xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF>|  
   |<xref:System.ComponentModel.Design.MenuCommand.Enabled%2A> = `true`|<xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF>|  
  
    若要更改菜单命令的文本，请使用 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.Text%2A> 对象上的 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 属性，如下面的示例所示。  
  
    [!code-csharp[MenuText#11](../snippets/csharp/VS_Snippets_VSSDK/menutext/cs/menutextpackage.cs#11)]
    [!code-vb[MenuText#11](../snippets/visualbasic/VS_Snippets_VSSDK/menutext/vb/menutextpackage.vb#11)]  
  
   MPF 自动处理不受支持的组或未知组的情况。 除非已使用 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> 方法将命令添加到 <xref:System.ComponentModel.Design.IMenuCommandService.AddCommand%2A> ，否则不支持该命令。  
  
### <a name="handling-commands-by-using-the-iolecommandtarget-interface"></a>通过使用 IOleCommandTarget 接口处理命令  
 对于直接使用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口的代码，VSPackage 必须同时实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 接口的方法 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 和 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。 如果 VSPackage 实现项目层次结构，则应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 接口的方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 。  
  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 和 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法旨在接收单一命令集 `GUID` 和命令 ID 的数组作为输入。 我们建议 VSPackage 完全支持此“单次调用，多个 ID”的概念。 但是，只要不从其他 Vspackage 调用 VSPackage，你可以认为该命令数组仅包含一个命令 ID，因为 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 和 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法以明确定义的顺序执行。 有关路由的详细信息，请参阅[Vspackage 中的命令路由](../extensibility/internals/command-routing-in-vspackages.md)。  
  
 对于直接使用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口进行命令处理的代码，必须如下面所示在 VSPackage 中实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法以处理命令。  
  
##### <a name="to-implement-the-querystatus-method"></a>实现 QueryStatus 方法  
  
1. 为有效命令返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 。  
  
2. 设置 `cmdf` 参数的 `prgCmds` 元素。  
  
    `cmdf` 元素的值是来源于 <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> 枚举的值的逻辑联合，这些值使用逻辑 OR (`|`) 运算符组合在一起。  
  
    基于命令的状态使用相应的枚举：  
  
   - 若不支持该命令：  
  
      `prgCmds[0].cmdf = OLECMDF_SUPPORTED;`  
  
   - 如果此时该命令应为不可见：  
  
      `prgCmds[0].cmdf |= OLECMDF_INVISIBLE;`  
  
   - 如果已切换为该命令且似乎已单击该命令：  
  
      `prgCmds[0].cmdf |= OLECMDF_LATCHED;`  
  
      在处理类型为 `MenuControllerLatched`的菜单上承载的命令时，标记为 `OLECMDF_LATCHED` 标志的第一个命令是启动时由菜单显示的默认命令。 有关 `MenuController` 菜单类型的详细信息，请参见 [Menu Element](../extensibility/menu-element.md)。  
  
   - 如果命令当前为启用状态：  
  
      `prgCmds[0].cmdf |= OLECMDF_ENABLED;`  
  
   - 如果该命令是快捷菜单的一部分，并默认处于隐藏状态：  
  
      `prgCmds[0] cmdf |= OLECMDF_DEFHIDEONCTXMENU`  
  
   - 如果该命令使用 `TEXTCHANGES` 标志，请将 `rgwz` 参数的 `pCmdText` 元素设置为命令的新文本并将 `cwActual` 参数的 `pCmdText` 元素设置为命令字符串的大小。  
  
     对于错误条件， <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法必须处理以下的错误情况：  
  
   - 如果 GUID 为未知或不受支持，则返回 `OLECMDERR_E_UNKNOWNGROUP`。  
  
   - 如果 GUID 为已知而命令 ID 为未知或不受支持，则返回 `OLECMDERR_E_NOTSUPPORTED`。  
  
   <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法的 VSPackage 的实现还必须返回特定错误代码，具体取决于是否支持该命令和令是否已成功处理该命。  
  
##### <a name="to-implement-the-exec-method"></a>实现 Exec 方法  
  
- 如果命令 `GUID` 未知，则返回 `OLECMDERR_E_UNKNOWNGROUP`。  
  
- 如果 `GUID` 已知，但命令 ID 是未知的，则返回 `OLECMDERR_E_NOTSUPPORTED`。  
  
- 如果 `GUID` 和命令 ID 匹配 .vsct 文件中该命令使用的 GUID:ID 对，则执行与该命令关联的代码并返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK>。  
  
## <a name="see-also"></a>请参阅  
 [VSCT XML 架构参考](../extensibility/vsct-xml-schema-reference.md)   
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
