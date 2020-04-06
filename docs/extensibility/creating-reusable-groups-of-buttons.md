---
title: 创建可重用的按钮组 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ddfba6701890f73ce6438ddc03a338912841a37d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739460"
---
# <a name="create-reusable-groups-of-buttons"></a>创建可重用的按钮组
命令组是始终一起出现在菜单或工具栏上的命令的集合。 任何命令组都可以通过将它分配给 *.vsct*文件的命令放置部分中的不同父菜单来重新使用。

 命令组通常包含按钮，但它们也可以包含其他菜单或组合框。

## <a name="to-create-a-reusable-group-of-buttons"></a>创建可重用的按钮组

1. 创建名为 的`ReusableButtons`VSIX 项目。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 打开项目时，添加名为 **"可重用命令"的**自定义命令项模板。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 在"**添加新项目"** 对话框中，转到**可视化 C#** > **扩展性**并选择 **"自定义命令**"。 在窗口底部的 **"名称"** 字段中，将命令文件名更改为*ReusableCommand.cs*。

3. 在 *.vsct*文件中，转到"符号"部分，并找到包含项目的组和命令的 GuidSymbol 元素。 它应该被命名为 guid 可重用命令包 CmdSet。

4. 为要添加到组的每个按钮添加 IDSymbol，如以下示例所示。

    ```xml
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">
        <IDSymbol name="MyMenuGroup" value="0x1020" />
        <IDSymbol name="ReusableCommandId" value="0x0100" />
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />
    </GuidSymbol>
    ```

     默认情况下，命令项模板将创建名为**MyMenuGroup 的**组和一个包含您提供的名称的按钮，以及每个项的 IDSymbol 条目。

5. 在"组"部分中，创建与"符号"部分中给出的属性相同的 GUID 和 ID 元素的组元素。 您还可以使用现有组，或使用命令模板提供的条目，如以下示例所示。 此组显示在 **"工具"** 菜单上

    ```xml
    <Groups>
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>
        </Group>
    </Groups>
    ```

## <a name="to-create-a-group-of-buttons-for-reuse"></a>创建一组按钮以供重用

1. 可以将命令或菜单放在组中，或者在命令或菜单的定义中将组作为父项，或者通过使用"命令放置"部分将命令或菜单放入组中。

     在"按钮"部分中，定义一个按钮，该按钮以组为父组，或使用包模板提供的按钮，如以下示例所示。

    ```xml
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ReusableCommand</ButtonText>
        </Strings>
    </Button>
    ```

2. 如果按钮必须出现在多个组中，请为其在"命令放置"部分创建一个条目，该条目必须放在"命令"部分之后。 将命令放置元素的 GUID 和 ID 属性设置为与要定位的按钮的属性匹配，然后将其父元素的 GUID 和 ID 设置为目标组的 GUID 和 ID，如以下示例所示。

    ```xml
    <CommandPlacements>
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        </CommandPlacement>
    </CommandPlacements>
    ```

    > [!NOTE]
    > "优先级"字段的值确定命令在新命令组中的位置。 在命令放置元素中设置的优先级将覆盖项定义中设置的优先级。 优先级较低的命令显示在具有较高优先级值的命令之前。 允许重复的优先级值，但无法保证具有相同优先级值的命令的相对位置，因为**devenv /setup**命令从注册表创建最终接口的顺序可能不一致。

## <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>在菜单上放置一组可重复使用的按钮

1. 在`CommandPlacements`节中创建条目。 将元素的`CommandPlacement`GUID 和 ID 设置为组的 GUID 和 ID，并将父 GUID 和 ID 设置为目标位置的 ID。

    命令放置部分应在"命令"部分之后放置：

   ```xml
   <CommandTable>
   ...
     <Commands>... </Commands>
     <CommandPlacements>... </CommandPlacements>
   ...
   </CommandTable>
   ```

    命令组可以包含在多个菜单上。 父菜单可以是您创建的菜单，由提供[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]（如*ShellCmdDef.vsct*或*SharedCmdDef.vsct*中所述），也可以是在另一个 VSPackage 中定义的菜单。 只要父菜单最终连接到[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]VSPackage 显示的快捷菜单或快捷菜单，父级图层的数量是无限的。

    下面的示例将组放在**解决方案资源管理器**工具栏上，位于其他按钮的右侧。

   ```xml
   <CommandPlacements>
       <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0xF00">
         <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
       </CommandPlacement>
   </CommandPlacements>
   ```

   ```xml
   <CommandPlacements>
     <CommandPlacement guid="guidButtonGroupCmdSet" id="MyMenuGroup"
         priority="0x605">
       <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS" />
     </CommandPlacement>
   </CommandPlacements>

   ```
